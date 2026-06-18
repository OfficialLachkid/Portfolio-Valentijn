# Direct Booking Website at Domits

<div style="text-align: center; margin: 0.25rem 0 1.75rem;">
  <img
    src="Images/Domits_Internship/Images/Platform_Showcase/image.png"
    alt="Direct Booking Website platform showcase"
    style="display: inline-block; width: 760px; max-width: 100%; height: auto; border-radius: 18px;"
  />
</div>

## Project Overview
During my internship at [Domits](https://www.domits.com/), I worked on the Direct Booking Website feature: a host-facing product that allows a host to publish a professional website for one property without starting a separate web project from scratch. The goal was to give hosts an owned online channel while keeping the underlying operational data aligned with the Domits platform.

This feature was not only about presentation. It had to fit into an existing hospitality product where listings, availability, pricing, and bookings already lived inside a Property Management System (PMS). That meant the website experience had to feel independent for the visitor, while still respecting the central source of truth behind the scenes.

## Why This Feature Exists
Domits wanted to give hosts a stronger direct-booking position. Instead of relying only on external channels, a host should be able to publish a clean branded website for a property and use it as an owned acquisition channel.

The feature exists for four main reasons:

- to help hosts present their property professionally through a dedicated public page
- to reduce friction for going live by using templates instead of custom development per host
- to keep business-critical data, such as availability and pricing, connected to the existing PMS
- to create a foundation for later direct-booking flows without first needing a completely separate platform

In practice, this meant building a system that was fast to publish, structured enough to maintain, and flexible enough to support future expansion.

## What The Feature Consists Of
The Direct Booking Website feature is made up of several connected parts.

### 1. Builder Workspace
The first part is the host-side builder flow inside the Domits dashboard. Here a host can:

- choose one of their own listings
- select a website template
- generate a first preview from listing data
- save that result as a website draft

This lowers the barrier to entry. A host does not begin with an empty page, but with a website structure that is already mapped from existing property information.

<div style="text-align: center; margin: 1.2rem 0 1.8rem;">
  <img
    src="Images/Domits_Internship/Images/Direct_Booking_Website/Builder.png"
    alt="Direct Booking Website builder workspace"
    style="display: inline-block; width: 820px; max-width: 100%; height: auto; border-radius: 18px;"
  />
</div>

### 2. Draft Editor
After the first build, the website can be refined in a dedicated editor. The editor is not a free-form page builder. It is a structured editing surface with section-based controls for content, visibility, images, and styling.

Examples of editable areas include:

- hero and title content
- residence and gallery sections
- amenities and icons
- contact section content
- image-slot selection and ordering behavior
- visibility and layout settings for supported sections

This structure keeps the experience manageable for hosts while also keeping the codebase maintainable for engineering.

<div style="text-align: center; margin: 1.2rem 0 1.8rem;">
  <img
    src="Images/Domits_Internship/Images/Direct_Booking_Website/Editor2.png"
    alt="Direct Booking Website draft editor"
    style="display: inline-block; width: 820px; max-width: 100%; height: auto; border-radius: 18px;"
  />
</div>

### 3. Internal Preview And Published Live Site
A major part of the feature is the separation between draft work and the published website. Draft changes can be previewed internally first, while the public website has its own published state.

That separation matters because it allows a host to keep editing safely without changing the live site immediately. In other words:

- saving draft changes does not automatically update the public site
- publishing and unpublishing are explicit actions
- the live website uses its own published snapshot and domain state

This is one of the most important architectural decisions in the feature.

A website in preview state stays on an internal preview route intended for review and iteration. Once a website is published, it receives a separate public-facing link instead of that preview-state route. One example of a published Direct Booking Website URL is [22-geneva-villa-6b6f0936.direct.domits.com](https://22-geneva-villa-6b6f0936.direct.domits.com/).

<div style="text-align: center; margin: 1.2rem 0 1.8rem;">
  <img
    src="Images/Domits_Internship/Images/Direct_Booking_Website/live_site.png"
    alt="Direct Booking Website live site preview"
    style="display: inline-block; width: 820px; max-width: 100%; height: auto; border-radius: 18px;"
  />
</div>

### 4. Public Website Runtime
The public side of the feature is a multi-tenant website runtime. Instead of generating a separate frontend deployment for every host or every template, Domits uses one shared runtime that can resolve and render different sites based on stored website data.

This runtime is responsible for:

- loading the correct published website
- rendering the chosen template
- showing published property content and media
- exposing contact and availability information on the public surface
- supporting a fallback Domits subdomain for the live site

### 5. Analytics And KPI Tracking
The feature also includes an analytics and KPI layer. That makes it possible to measure how the builder and published websites are being used, and whether the product is performing as intended.

Examples of tracked areas include:

- build attempts and successful builds
- preview and live-site opens
- live-site updates
- performance measurements such as Largest Contentful Paint
- research-aligned metrics for publish speed, cost and domain readiness

<div style="text-align: center; margin: 1.2rem 0 1.8rem;">
  <img
    src="Images/Domits_Internship/Images/KPIs/KPIs.png"
    alt="Direct Booking Website KPI dashboard"
    style="display: inline-block; width: 820px; max-width: 100%; height: auto; border-radius: 18px;"
  />
</div>

#### KPI Perspective From The Thesis
The KPI set in my thesis was used to explain not only which metrics the feature should expose, but also why each metric matters in practice. That gave the feature a stronger evaluation framework than a simple usage counter.

| Criterion | KPI / Metric | Why It Exists |
| --- | --- | --- |
| Scalability | `time_to_publish_p95` | Measures how quickly a website can be published in 95% of cases. |
| Costs | `cost_per_active_site_per_month` | Gives an indication of the average operational cost per active website per month. |
| Performance | `site_lcp_p75` (mobile, tablet, desktop) | Measures how quickly the most important visible content is loaded. |
| Reliability | `fallback_subdomain_availability` | Shows whether fallback domains remain available and reachable. |
| Correctness | `quote_to_charge_mismatch_rate` | Shows how often a gap appears between expected pricing information and final price handling. |
| Future reliability (v2) | `booking_api_error_rate` | Measures how often errors occur during booking API flows once booking is enabled. |
| User experience (v2) | `booking_funnel_completion_rate` | Shows what share of users complete the booking flow. |
| Domain management (v2) | `custom_domain_setup_success_rate` | Measures how often connecting a custom domain succeeds. |

This helped frame the feature as a measurable product foundation: not only something that works visually, but also something that can be evaluated on speed, reliability, cost, correctness, and eventual booking behavior.

## How It Was Built
The Direct Booking Website was built as an extension of the existing Domits platform rather than as a separate product stack.

### Frontend Approach
On the frontend, the feature lives inside the existing Domits React environment. The implementation uses dedicated surfaces for:

- the builder workspace
- the editor page
- the internal preview route
- the published website runtime
- the KPI dashboard

A shared website model sits underneath those surfaces. Listing data is normalized into a template-friendly structure so different templates can render from the same content contract. This avoids each template inventing its own data shape.

At the time of this work, Panorama Landing had the deepest editor and rendering support. Other templates already existed to different degrees, but Panorama was the most complete reference path for real editing, previewing, and publishing behavior.

### Backend And Persistence
On the backend, the feature was integrated into the existing `PropertyHandler` area. Dedicated website routes handle draft storage, publication, public rendering, preview loading, event collection, and KPI retrieval.

The persistence model is split into four main tables:

- `main.standalone_site_draft` for working draft data
- `main.standalone_site` for the published live-site snapshot
- `main.standalone_site_domain` for fallback-domain and later domain state
- `main.standalone_site_event` for analytics and KPI event storage

This split is deliberate. It prevents draft editing, live-site state, domain state, and event data from being mixed together in one record.

### PMS Integration And Data Ownership
One of the central design decisions was deciding what should stay PMS-owned and what should become website-owned.

| Layer | Responsibility |
| --- | --- |
| PMS | property details, operational availability truth, pricing truth, booking truth |
| Direct Booking Website | template selection, branding, content overrides, published site state, domain mapping, analytics |

The descriptive property content is imported into a published snapshot for the website. That means the public page can render quickly from stored website data instead of reading full descriptive PMS content live on every request.

Availability still stays connected to the PMS domain. In the current foundation, the website already shows a read-only availability view based on imported and enriched calendar data. More advanced quote and booking behavior is designed to happen server-side in later phases, not in the browser.

### Publish Model
Another important part of the build is the publish model itself. The feature distinguishes clearly between:

- working draft state
- published live-site state
- domain state
- analytics event state

That separation supports safer editing, clearer behavior, and a cleaner path for future expansion such as custom domains, quote APIs, checkout and booking creation.

## End Product
The resulting product is a foundation release for a direct-booking channel inside Domits.

By the end of this feature phase, Domits had:

- a host-side builder flow
- a saved-draft and editor workflow
- an internal preview route
- a published public website runtime
- fallback-domain support
- a shared template model
- analytics and KPI tracking for the website lifecycle

What it did not yet fully include was just as important to communicate clearly. The feature was intentionally scoped as a solid foundation first. Public checkout, payment, booking creation, custom domains, and a full booking funnel were later-phase work.

## Why This Work Matters
This project is a good example of product engineering inside an existing platform. The challenge was not only to make a website look good, but to fit a new product surface into existing architecture, shared data ownership, and long-term platform constraints.

For me, this feature was valuable because it combined several types of work in one project:

- product thinking about what a host actually needs
- frontend work on templates, editing flows, and preview behavior
- backend thinking around persistence, publication, and public rendering
- architectural decisions about source of truth, safety, and future scalability

That combination is also what makes the Direct Booking Website one of the strongest examples of my internship work at Domits.

