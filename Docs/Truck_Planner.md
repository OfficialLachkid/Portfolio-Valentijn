[Truck Planner Prototype](https://officiallachkid.github.io/truck-planner/)

<div style="display: flex; gap: 50px;">
  <img src="Images/Experiments/Truck_Planner/Truck_Overview.png" style="width: 100%;" />
</div>

# Why We Built This App

I built this application with a clear purpose: to help a business transition into a modern, digital way of working. For many companies that rely on logistics, daily planning often involves paper maps, magnets and handwritten routes. Over time this becomes unmanageable, unclear for employees and nearly impossible to scale whilst relying on a single employee. This app is designed to solve that problem.

## Modernizing Daily Planning

Instead of drawing routes manually on a physical map, the entire workflow is now placed in an online environment. Every truck, route and order is visible for all employees. I can plan ahead, verify orders and adjust schedules from anywhere — even from home on the couch. New orders appear directly inside the system, ready to be scheduled instantly.

The goal is simple: create clarity, efficiency and future‑proof planning without relying on one person to draw and track everything manually. In a growing company this is no longer sustainable. The need for overview is essential, not only for that single employee, but for coworkers as well. To tackle the issues surrounding this problem, a prototype was made to visualize the efficienty of converting to a digital overview area.

## Order Placement Inside the Truck

An important feature of this application is the ability to place orders directly into the layout of a truck. Each slot represents pallet‑space, and I can decide how many pallets an order consumes. Orders can be assigned to a specific location inside the truck which gives complete visual insight into available space.

Multiple trips can be created per truck per day, enabling efficient scheduling for drivers who perform several deliveries during one shift. If more capacity is required, I can simply add another trip with a single action (and delete one of course if necessary).

<div style="display: flex; gap: 50px;">
  <img src="Images/Experiments/Truck_Planner/Detailed_Truck_Overview.png" style="width: 30%;" />
  <img src="Images/Experiments/Truck_Planner/Palletsize_Menu.png" style="width: 60%;" />
</div>

## Truck Overview and Calendar Navigation

The app provides an overview of all trucks scheduled on a particular day. I can easily look ahead into future dates or review previous planning. The truck overview acts as a calendar that helps the entire company stay organized and aware of active transport capacity.

This prevents confusion, reduces communication friction and eliminates mistakes that are common when using whiteboards, paper or spreadsheets. All information stays in one location, accessible to everyone who needs it.

<div style="display: flex; gap: 50px;">
  <img src="Images/Experiments/Truck_Planner/Kaart_Rit1.png" style="width: 50%;" />
</div>

## Built‑In AI Route Planning

To further improve workflow, the application contains automated route planning intelligence. The system collects all orders and calculates an efficient route based on location and travel sequence. This generates a default route that ensures logical delivery order and optimized driving distance.

AI removes guesswork, speeds up the assignment process and ensures that no one has to manually determine the route every day. It is a supporting tool that increases productivity while maintaining clarity.

<div style="display: flex; gap: 50px;">
  <img src="Images/Experiments/Truck_Planner/Kaart_Default_Route.png" style="width: 50%;" />
</div>

## Why This System Matters

A growing business needs scalable logistics. Manual planning limits efficiency, introduces mistakes and hides information from employees who need insight. This app ensures continuity, digital transparency and accessible planning for everyone.

Instead of magnets on a board or routes drawn by hand, planning now lives inside a structured, intelligent and fully controllable system. It is built so the company can move forward, handle more orders and give employees the tools they need to work clearly and confidently.

## Early Designs

---

<div style="display: flex; gap: 50px;">
  <img src="Images/Experiments/Truck_Planner/Design/Design1.png" style="width: 50%;" />
</div>

---

<div style="display:flex; gap:50px; align-items:flex-start;">
  <img src="Images/Experiments/Truck_Planner/Design/Design2.png"
       style="width:45%; height:400px; object-fit:contain;" />

  <img src="Images/Experiments/Truck_Planner/Design/Design3.png"
       style="width:45%; height:400px; object-fit:contain;" />
</div>

---

## Roadmap

- Fetch incoming orders from company's database
- Show corresponding date orders
- Filter orders by postal code (1000-2000. 2000-3000 etc)
- Dark mode
- Realtime truck location display
- Order info upon placed order
- Delivered order interactble menu