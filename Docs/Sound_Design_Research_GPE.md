---
author: Valentijn Jacobs
title: Sound Design
date: 2025-03-5
<div style="display: flex; gap: 50px;">
  <img src="Images/Images_GPE/ResearchThumbnail.png" style="width: 100%;" />
</div>

---

This paper will conduct research on how sound is used in video games beyond just music and voice acting.
Researching how sounds/sound cues affect player behavior and decision making, player feedback, player immersion and identify the best way to implement sounds in games.

# Introduction

Sound is a crucial yet often overlooked element in game design, shaping the player’s experience. Without sound, games like horror movies lose much of their emotional impact. A terrifying monster encounter becomes far less effective without eerie ambient noise, jumpscares, or unsettling whispers. Sound serves for multiple functions beyond just player immersion. It provides cues and guidance, ensuring players stay engaged and informed about their tasks during their playthrough.

For example, audio cues can subtly direct players by signaling important events, such as an enemy approaching or an objective being nearby. When a player is stuck, sound can also serve as a navigational tool, triggering voice lines or ambient hints that helps players toward their next step. Additionally, background music plays a crucial role in intensity, shifting dynamically during boss fights or suspenseful moments to increase tension. By integrating sound effectively, games create a deeper immersion, improve player decision making and enhance the overall experience. Many iconic game moments would lose their power and impact without sound implementations.

## Problem statement

Sound design plays a crucial role in shaping player experience in video games, yet its impact is often underestimated. While visuals provide the foundation for a game’s world, it is sound that brings it to life—enhancing immersion, guiding players, and creating emotional depth. Without sound, a horror game loses its tension, a boss fight lacks urgency, and a puzzle game may fail to provide distinct feedback to the player [1] [2].

In-game sound serves multiple functions beyond just music and atmosphere. It provides cues that help players navigate environments, identify threats, and understand game mechanics [3]. For example, in stealth games, enemy footsteps or voice lines inform players of nearby dangers, while in adventure games, subtle audio hints can guide players when they are stuck. Additionally, background music dynamically shifts to reflect changes in intensity, such as in boss fights, where the soundtrack adapts to different battle phases to heighten tension and excitement [4] [5].

Despite its importance, the systematic study of sound implementation in games remains underexplored compared to visual design.  
How do sound cues capture the player's attention?  
Which sound techniques help players navigate without being overwhelming or repetitive?  
Which key elements of adaptive sound contribute most to player immersion?  
Addressing these questions can lead to a better understanding of how sound contributes to game design and can improve the way audio is used to create meaningful player experiences [6].

## Research question

How does sound affect player behavior and decision making, feedback to the player and player immersion?

# Research

## What are sound cues?

Sound cues are auditory signals used in various media, including video games, to provide information, enhance immersion, and guide player behavior. These cues can be anything from background music shifts to character voice lines, environmental sounds, or even UI feedback sounds. They help players understand the game world, make decisions, and react to events more intuitively [1] [3] [7].

Sound cues can be categorized into different types:

- Diegetic Sounds: Sounds that exist within the game world (footsteps, gunshots, NPC dialogue) [4] [6].

- Non-Diegetic Sounds: Sounds that do not originate from the game world but enhance the experience (background music, UI notifications) [2] [5].
  
- Interactive Sounds: Sounds that change dynamically based on player actions (adaptive music, sound variations based on movement) [3] [8].
  
- Feedback Sounds: Sounds that indicate actions or events (coin collection, level-up jingles, error buzzers) [1] [9].

## What are they used for?

Sounds are used for a variety of aspects when it comes to games.  
I've listed some down below in a table:

| **Function**              | **Description**                                    | **Examples in Games**                        |
|---------------------------|----------------------------------------------------|----------------------------------------------|
| **Navigation & Hints**    | Guides players toward objectives or paths         | Faint whispers in horror games, glowing sound cues in *Zelda: Breath of the Wild* |
| **Threat Indication**     | Alerts players of incoming danger                 | Enemy footsteps in *Fortnite* |
| **Emotional Immersion**   | Enhances tension, excitement, or fear             | Boss fight music increasing in tempo in *Hogwarts Legacy*, unsettling whispers in *Silent Hill* |
| **Reward Feedback**       | Confirms successful actions or achievements       | Level-up sound effects in *World of Warcraft*, item collection chime in *Super Mario Bros.* |
| **Puzzle Assistance**     | Provides subtle hints for solving puzzles         | Sound cues indicating a correct answer in *The Witness*, interactive sound shifts in *Portal* |
| **Environmental Context** | Creates a believable world with ambient sounds    | Wind howling in *Skyrim*, city ambiance in *Cyberpunk 2077* |
| **Player Health Indication** | Notifies players of low health or status changes | Screen heartbeat effect in *Call of Duty*, drowning sound cues in *Sonic the Hedgehog* |
| **Stealth Feedback**      | Tells players if they are being detected          | Alert sound in *Metal Gear Solid*, enemy awareness sound in *Assassin’s Creed* |
| **Inventory & UI Sounds** | Enhances interaction with game menus              | Click sounds when browsing inventory in *Diablo*, pause menu whoosh in *Horizon Zero Dawn* |
| **Multiplayer Awareness** | Informs players of teammate/enemy actions        | Kill confirmation sound in *Apex Legends*, voice cues in *Overwatch* |

## How does this apply to games?

In video games, sound cues are essential in creating an immersive experience and guiding player behavior. They enhance gameplay by making interactions more intuitive and engaging.  
For instance:

- **Horror Games**: Low, eerie sounds build tension before a jumpscare, while sudden loud noises shock the player.
<div style="display: flex; gap: 50px;">
  <img src="Images/Images_GPE/SilentHill.jpeg" style="width: 100%;" />
</div>

- **Action Games**: Adaptive music changes during combat sequences, creating urgency and excitement.
<div style="display: flex; gap: 50px;">
  <img src="Images/Images_GPE/BreathOfTheWild.jpeg" style="width: 100%;" />
</div>

- **Puzzle Games**: Audio clues help players solve puzzles by indicating correct or incorrect actions.
<div style="display: flex; gap: 50px;">
  <img src="Images/Images_GPE//CanyCrush.jpeg" style="width: 100%;" />
</div>

- **Open-World Games**: Environmental sounds like distant animal calls or changing weather conditions make the world feel alive.
<div style="display: flex; gap: 50px;">
  <img src="Images/Images_GPE/HogwartsLegacy.jpeg" style="width: 100%;" />
</div>

Sound cues also play a crucial role in accessibility, helping players with visual impairments navigate games through spatial audio cues.

By leveraging sound cues effectively, game designers can create richer and more engaging experiences that guide players seamlessly while enhancing the emotional impact of the game world.

## How do sound cues capture the player's attention?

### What are sound cues?

Sound cues are auditory signals used in various media, including video games, to provide information, enhance immersion, and guide player behavior. These cues serve as vital elements within game design, as they help players explore their environment, detect important actions, and react to events more intuitively. Sound cues can be categorized into four main types, each playing a distinct role in the gameplay experience.

- Diegetic Sounds: These are sounds that exist within the game world and are directly sensible by the player. They can include environmental sounds like footsteps, ambient noises, or NPC dialogues, all of which help the players connect with the in-game world [4] [6].

- Non-Diegetic Sounds: These sounds do not originate from the game world but are used to enhance the overall player experience. Examples include background music, UI notifications, or dramatic sound effects that inform players of critical in-game events [2] [5].

- Interactive Sounds: Sounds in this category change dynamically in response to player actions or game events. For example, adaptive music that shifts based on the player's progress/experience or sound variations based on movement are both essential in maintaining engagement and guiding behavior [3] [7].

- Feedback Sounds: These sounds indicate a result or an in-game event. Feedback sounds like level-up jingles, item collection cues, or error buzzers communicate success or failure, helping the player with decision and action making [1] [9].

### Sound cues in games

In the context of video games, sound cues are instrumental in guiding the player's experience by directing their attention, indicating threats, and enhancing emotional immersion. Different types of sound cues are used throughout games to provide context, reinforce gameplay mechanics, and offer the player valuable information. Games like Silent Hill utilize eerie environmental sounds to induce fear, while action games like Hogwarts Legacy employ adaptive music to heighten the excitement during combat [4] [6].

Sound cues also serve as navigational tools. For example, whispers in horror games may indicate hidden secrets, while footsteps or doors creaking may hint at nearby dangers. These types of cues help players make informed decisions and avoid potential traps [1] [8]. Additionally, feedback sounds like item collection or reward cues help players feel a sense of progression and satisfaction [9].

### Sound on player immersion

Sound plays a crucial role in emotional immersion within video games. By using dynamic and adaptive soundscapes, developers can create experiences that respond to players actions, thus increasing engagement and emotional involvement. For instance, in games like The Legend of Zelda: Breath of the Wild, environmental sounds such as wind howling or distant animal calls immerse players in the world and provide subtle hints about their surroundings [5]. Furthermore, in multiplayer environments, spatial audio cues ensure players can be aware of both teammate and enemy movements, providing an additional layer of tactical awareness (Fortnite) [7].

### Impact of sound on player behavior

Sound cues significantly influence player behavior, especially in terms of decision-making and emotional response. Research has shown that effective use of audio can enhance visual attention, guide player actions, and help solve puzzles more efficiently [3] [7]. In horror games, for example, subtle changes in background audio can intensify fear, leading players to make more cautious movements or engage in defensive behaviors when encountering threats [6]. Similarly, sound feedback in action games motivates players to complete objectives more quickly, knowing their actions are being acknowledged by sound cues [9].

By integrating sound effectively into gameplay, developers can ensure a more engaging, responsive, and immersive experience that not only guides players but also amplifies emotional and cognitive responses to in-game events.

## Which sound techniques help players navigate without being overwhelming or repetitive?

Effective sound design is essential in guiding players through a game, especially when trying to avoid overwhelming or repetitive audio cues. The challenge is in finding the balance where sounds enhances the player's experience without distracting them or causing irritation during their playthrough.  
There are several techniques that can be used to ensure sound cues are beneficial to player navigation and gameplay.

| **Sound cue type**        | **Description**                                                       |
|---------------------------|-----------------------------------------------------------------------|
| **Diegetic sounds**        | Sounds originating from the game world (footsteps, gunshots, dialogues). |
| **Non-diegetic sounds**    | Sounds that enhance the experience but do not exist in the game world (background music, UI notifications). |
| **Interactive sounds**     | Sounds that change based on player actions (adaptive music, sound variations in response to player movement). |
| **Feedback sounds**        | Sounds indicating actions or events (level-up sounds, item collection jingles, error buzzers). |
| **Threat indicators**      | Sounds that alert players to danger (enemy footsteps, alarm sounds, enemy sighting alerts). |
| **Environmental sounds**   | Background sounds that help build the world (wind, rain, animal calls). |
| **Reward sounds**          | Sounds indicating achievement or progress (completing objectives, collecting items, level-up spendable points). |
| **Puzzle assistance sounds** | Audio cues that help players progress through puzzles (correct solution sounds, voice over hints). |
| **Health/Status sounds**   | Sounds indicating the player’s health or status (heartbeat sound when health is low, damage sounds, heavy breathing). |
| **Stealth feedback sounds** | Sounds indicating if the player is detected or hidden in stealth games (alert sounds in *Assassin's Creed*, such as escalating whistles or tension music when detected). |

### Dynamic adjustment based on context

- How: Sound cues should change depending on the player’s progress or situation in the game. For example, enemy footsteps should become louder or more distinct as they approach, while ambient music should shift dynamically to reflect changes in the game’s emotional tone (moving from peaceful exploration to tense combat). This dynamic adjustment is essential for keeping the player engaged and immersed, as it adapts to the evolving game scenario [1] [5].
  
- Why: This prevents sound from becoming monotonous by ensuring that players’ ears are constantly attentive to evolving auditory signals. The change in intensity also helps indicate significance, like alerting the player to danger without overwhelming them, as highlighted by Gate’s research on audio’s impact on atmosphere during events [2].
  
### Layering and spacing out cues

- How: By layering different sound cues across the gameplay and spacing them out, designers can provide subtle guidance without constant bombardment of audio parts. For example, a faint environmental sound might indicate a nearby location, while a more clear cue (like a chime or a vocal hint) could follow when the player is close to interacting with a key item. This layered approach allows the cues to remain meaningful and prevents auditory fatigue [4].
  
- Why: This ensures that the player’s attention isn’t constantly diverted from the gameplay itself. It also prevents the repetition of cues, which can lead to irritation or fatigue, as described in Walker and Lindsay’s study on the effectiveness of spatial audio cues [9]. Spacing out the cues lets them build anticipation and allows the player to absorb them in manageable doses.

### Adaptive feedback systems

- How: Using interactive sounds that adapt to player actions helps prevent repetitiveness. For example, if a player is near a solution to a puzzle, a subtle audio cue might change in frequency or pitch. If the player takes a wrong turn, a non-intrusive sound could gently guide them back to the correct path. This technique is supported by Pitstop’s exploration of sound design’s importance in creating immersive experiences [4].
  
- Why: This technique balances providing necessary guidance while avoiding disruption. It encourages players to experiment and think critically, without overwhelming them with constant reinforcement. The adaptability of feedback sound plays a key role in this balance [5].

### Sounds for stealth and threat indicators

- How: In stealth games, sound cues should indicate awareness without constantly reminding players of danger. A soft sound, such as a distant creaking or rustling, could signal nearby threats. A sudden, sharp change in pitch or intensity (like a fast heartbeat or warning alarm) can indicate immediate danger. The subtle nature of these cues contributes to building tension while maintaining player focus, as emphasized by Jørgensen’s discussion of fear and sound [8].
  
- Why: Using subtle but important cues in stealth contexts ensures the player feels engaged and aware without constant distractions. This also helps build suspense without making the threat feel repetitive, a concept that’s central to sound design’s role in generating fear and tension [6].

### Emotions through music and sound

- How: Music can shift subtly based on the player’s actions, making it an excellent tool for immersion. For instance, the intensity of background music could gradually increase as a boss fight nears its climax, or the environmental sounds could shift with changing weather or time of day. This alignment of sound and gameplay emotions strengthens the player’s connection to the narrative [1].
  
- Why: Music and sound need to complement the emotional arc of the game. By adapting these cues to the narrative and player actions, developers can create moments of tension, excitement, or relief without overwhelming players with excessive audio stimuli. This enhances emotional investment and immersion, which has been demonstrated in numerous studies on game audio [5] [4].

### Utilizing spatial audio

- How: Spatial audio cues (3D audio) can provide contextual hints based on the player’s surroundings. For example, a sound of footsteps could change based on whether the player is upstairs or downstairs, providing a natural sense of direction. This type of cue relies on the player’s ability to localize sounds, which has been extensively studied in the context of multi-channel audio systems [7] [9].
  
- Why: This approach helps players understand their environment without needing constant visual feedback. It also ensures the player can differentiate between similar cues by assigning a spatial element to each sound, reducing repetition and increasing immersion. The effectiveness of spatial cues is well-documented in research by Walker and Lindsay [9].

### Frequency of reward cues

- How: Reward sounds should be used sparingly, only when a significant achievement occurs (such as completing a puzzle or discovering a hidden room). Overuse of rewarding cues (like constant jingles or celebratory sounds) can diminish their impact. The design of reward cues has to be balanced to avoid auditory fatigue and maintain excitement over time [1].
  
- Why: This keeps the sense of reward meaningful and impactful, preventing it from becoming distracting or irritating. Players are more likely to appreciate and internalize these cues when they’re not constantly bombarded with them, as noted by the analysis of effective sound design in games [4].

### Player control over sound

- How: Providing players with the ability to adjust sound levels or toggle specific sound categories (ambient music, combat sounds, environmental cues) gives them greater control over their experience. This flexibility in sound customization enhances player satisfaction and accessibility [2].

- Why: This prevents the player from feeling too overwhelmed by sound if it’s becoming intense or repetitive for them. Offering sound options can also help players with different preferences, allowing them to fine tune the experience to their liking. Research on user control over audio has shown that it can increase enjoyment and immersion [5].

## Builds and tests

In order to gather data, I want to implement the following:

> ### 1 Scene design & setup

- Third person game.
  
- A maze where sounds guide the player if they're stuck.
  
- Sound cues that reveal hidden passages.
  
- Objects that trigger sound cues when interacted with (buttons, doors, unlocking hidden paths).

> ### 2 Sound types to include

- **Navigational sound cues:**  
Subtle beeping or directional sounds that guide players toward a goal.

- **Reward sounds:**
Audio feedback when the player collects items, reveals hidden rooms and/or wins.

> ### 3 Experimental variables

- **No sound**  
Players navigate and explore without any sound cues.

- **Basic sound cues**  
Players receive minimal hints (chimes, object interaction sounds, indicating specific direction/solutions).

- **Full audio feedback**  
Players experience immersive sound cues guiding decisions.

> ### How to implement?

I am going to implement and create the audio/scene in Unity using AudioSource, AudioListener, Spatial Audio and Trigger Colliders. All of this being present in a maze while the player's objective is to explore and find their way out of the maze.

> ### Expected results & hypothesis

- Players with sound cues will navigate faster and explore more hidden aspects.

- Lack of sound feedback may cause confusion or frustration or long playthroughs or no hidden things found.

## First iteration

> A/B Test data analysis ideas

- **Completion time:**  
We will note and compare how long each group takes to finish the maze on average.

- **Exploring rate:**  
We check if the audio group found more hidden areas and has explored more aspects.

- **Player emotion** Measure player's difficulty and frustration between both groups.

## Survey

Upon testers playing around in the maze scene, trying to unravel hidden clues, secret passage ways or trying to simply find their way out of the maze as quickly as possible, I want to gather useful information from our testers.

To be able to gather useful information and make it efficient to gather this data, I will create a survey which players can fill-out after their playthrough.

We scraped the online survey, due to wanting verbal questions/answers. We chose this approach since we wanted to gather as much information as possible and we do not want the feeling of lack of typing to influence our results.

### Survey questions

> General questions

- **Did you notice any hidden rooms?**  
If yes, how did you find them?

- **Did you feel guided toward important locations?**  
Why or why not?

> Specific sound questions (audio group)

- **Did the sounds help you understand where to go?**  
(Yes/No)

- **Which sounds did you find most helpful?**  
(Button triggers, hidden room cues, rewarded sounds, spatial audio)

- **Were there any moments where the sound cues confused you instead of helping?**  
(Yes/No, please explain)

- **How immersive did the audio make the experience feel?**  
(Scale: 1 = Not immersive at all, 5 = Extremely immersive) **(voor 2e test?)**

- **Did any sound effects feel unnecessary or distracting?**  
(Yes/No, please specify)

> Open end questions

- **What would you change about the sounds in the game to make them more effective?**
  
- **Did you encounter any frustrating moments? How do you think sound could have improved those situations?**

## Playtest

The first play test was entertaining to conduct. Many testers were surprised about the maze and did not know what to expect.  
We mentioned at the beginning of the test that the player's objective was to find their way out of the maze and to keep a close ear whenever sounds are triggered.

> **Noticeable aspects:**

- We noticed many players were immediately alerted and concentrated whenever sound cues were played.
  
- We noticed some sounds overlaped, causing confusment to the player since they could not correctly pin point the thing they were trying to find.
  
- We noticed spacial audio worked best, especially on the hidden coin objects. This resulted in quick findings and was easy to understand/locate.
  
- We noticed players had a harder time finding the first "E" prompt (used for entering secret rooms), since they had to be in range. Once players understood, they tended to walk against the wall more often to not skip/oversee any hidden rooms.
  
- Spatial audio really healped players pin point the object they were trying to find. Resulting in less time spend trying to unravel where the hidden object was located at.
  
- Many players stated the need of extra spatial audio implementation on the hidden rooms, since there's only a voice prompted now which does not pin point the location of the hidden room.
  
- We mentioned that the implemented sound was immersive to players, however not as much as we'd hoped. This might be scored lower due to no ambient noise. (Will be tested seperatly)
  
- We noticed one tester locating the exit, but turned around because of an activated audio cue that wasn't even in reach. This shouldn't have been the case with the non audio test group.
  
- We noticed testers would also want a bit more variation in sound: different voice overs, other sound indicators that would excite them more.
  
- We noticed that the secret rooms were hard to locate, because of their appearance range. This was a good thing, since the no audio group walked right passed them. Sound could've stated there was something hidden nearby.
  
- One of the testers stated they needed more sound cues with a faster interval, since it was too hard to find the hidden rooms in their opinion.

- Not all rooms were discovered, while most of the coins were.
  
- One tester stated that they wanted to hear the voice over one time instead of it resetting when out and in range. This made them feel dumb and would much rather hear a constant sound instead of a voice over.
  
- Some players were too busy finding the hidden aspects of the maze that they walked right out of the entrance and fell of the map.

## Playtest 1 reflection

> **Sound Group:**

- We noticed players initially had difficulty finding the secret rooms. It would be helpful to provide an extra audio cue when they get closer, similar to the hidden coin. The addition of spatial sound would help tremendously I suppose.

- Some sounds overlapped, causing two to play simultaneously, making it difficult to pinpoint their location. However, it did give the impression that there were multiple rooms. (Using box colliders here could have worked better instead of range)

- We had to reduce the range of some sounds to avoid confusion, as certain cues were coming from behind walls. However, it was good to see that players actively searched for them. This indicates that sound serves as a directional cue, altering perception and guiding the player's movement even when they can taste the exit/victory.

> **No-Sound Group:**

The no-sound group had the UI displayd just like the audio group whilst being instructed to find the end of the maze.

- One of the testers was actually an explorer type of gamer and unraveled a couple of rooms and coins as he was trying to find the exit. A factor that could've helped him was placement of hidden rooms and coins. Although we did not want to make certain areas indicating a coin or hidden room would be near. Dead ends or a weird wall part were definitely giving away their location. Not relying on audio to find them.

- Other testers mostly found the first 2 rooms and haven't found more than 3 coins. Even though someone walked past them (not triggering E), but would've definitely heard them emitting sound if audio was turned on.

- It was still good to see players having the feeling of find hidden rooms and coins but just couldn't since there was no extra audio aid.
  
- We asked this group what we could implement to make discovering the hidden aspects of the maze easier. One of the testers came up with a radar idea. A beeping sound that would beep faster/slower depending on how far the player would be from the hidden object.

More testers have found hidden rooms and coins than imagined/written in the hyphothesis. This could've been the case because some doors/coins were too easy to find and weren't somewhat away from the path. Comparing this to bigger games where everything is more spread out. We take this aspect into consideration for future work.  
However, we did notice the non-audio group collecting and exploring less coins and hidden rooms. They were less direct than the audio group in locating these hidden aspects once in range which is valuable to notice.

## Second Playtest

For this second iteration we want to test the immersiveness by implementing ambient sounds and spatial audio to give life to specific scenes. We want to create several different environments and navigate the player through the different scenes by providing a lerp track for the camera to follow. Whilst the player has to do nothing other than look around (by mouse) and listen to the several environments' sounds and try to feel immersed.

For this second test, we want to let testers initially navigate through the different scenes without any audio. Once they completed the non-audio loop, we start the scenes again and provide audio cues/ambient sound in each different environments.

<div style="display: flex; gap: 50px;">
  <img src="Images/Images_GPE/Japan.png" style="width: 100%;" />
</div>

> #### Expected results & hypothesis

- Players will be more immersed with audio turned on.
- Players will notice more objects once sounds are turned on.
- Players are drawn more to certain aspects in scenes emitting sounds (birds, market, treasure chest).
- Players might recognize new 'things' because of audio.

> **General Questions**

- Did you feel more immersed per scene with audio compared to no audio, why?
  
- Did you have the urge to explore for yourself instead of being put on a track whenever sounds were heard?
  
- To which scene were you most drawn/immersive to, why?
  
- Were there sounds that felt accesive/annoying?
  
- Were there visuals that you didn't notice at first, but later did with sound?
  
- Felt the loop faster compared with non-audio?

> **Scene Specific Questions**

These next questions were asked to gain knowledge about the tester's fantasy.

- How did the ship sank?
  
- What's happening in Egypt?
  
- What kind of feeling aroused in the Japanese environment?
  
- If wild west would have motion, what would happen?

> **Noticeable aspects**

Every tester so far stated that scenes with audio made much more impact and felt entirely different than non-audio. Many players felt much more immersed whilst the loop felt quicker too during their second play through.  
This is quite the funny aspect, since repeating aspects could become boring or could feel as waiting at one point, especially with the amount of time it took for some environments to navigate through.

Apart from the general questions, we wanted to get more specific answers and test if people would fantasize when navigating through the scenes.  
These questions required more imagination from testers. We for instance asked how certain parts played out in the Abandoned Island scene. With many testers answering how the ship sank due to a battle against another ship. One tester even took this to a greater level and told us it was almost hystorical to him when imagining how this island has acknowledges a great battle between two ships and how it gained peace once again by hearing seagulls and all of the sounds of an abandoned island he could hear, with the treasure still left behind, emitting a shiny sound coming from within.

The majority of testers found Egypt had a mysterious tone and noticed a market. One tester thought the market was a battle field with soldiers dying left and right (not intended). One thing was certain for all testers: the sound from the market drew every tester's attention, which is funny to see. It's funny since a tester thought something else of the sound, while still being interested by the origin/location of the sound, further looking and inspecting it.

Testers stated the Japanese environment was very calm/tranquil to travel through. One tester stated this could be the case because there are not a lot of sounds emmiting at once, rather as you go through the scene, which seemed to be relaxing to testers. Implemented audio included animal sounds, even though no visual representation of animals were visible, caused testers to fantasize where they would be located (with the help of 3D audio). Testers fantatized birds perched in the tree and frogs being present near water.

At the train station scene some testers noticed the horses located behind the station. Not every testers noticed them, but at least the majority recognized/indicated a sound emmiting from behind the station. This let to them visually acknowledging the horses whilst no differences was made visually.

Lastly, a noticeable aspect that must not be forgotten is specific placement of audio. Gathered answers from testers indicate sounds helped them be more immersed. We noticed spatial audio helped draw the tester's attention much more while ambient music was just static (2D). We noticed testers being drawn due to seeing them locate the emitting of audio. During this process, we noticed people listened closely once the spatial audio was in range and once it faded out, testers were less focused to a specific point.

## Playtest 2 reflection

We tested the different environments (audio & non-audio) with 10 players in total. The majority of these testers were familiar with gaming and have been playing games for quite some time now. Some of the testers had actually no experience at all with video games. The specific restriction of movement was implemented to make sure audio in these diverse scenes can be tested on gamers and non-gamers, solely relying on their hearing sense and how audio contributes to their visual image.

We were happy to see our hypotheses are correct with ambient noise and spatial audio highly contributing to player immersion.

We expected another outcome when playing no audio during the loop. And that is that the scenes were boring to lots of players with audio and felt excessively long. This became clear once multiple testers stated the audio version went by much quicker in their opinion.

When conducting the test, we stumpled upon a different idea of testing which did not include any visual representation of what the person should be hearing. This test would allow players to close their eyes and solely rely on the hearing sense, asking them what they image with different parts that are heard. This kind of playtest would've been fun and probably helpful. However, due to lack of time, this idea will be moved to future work.

### Different environments & audio used

*Japanese Environment*
<div style="display: flex; gap: 50px;">
  <img src="Images/Images_GPE/Japan.png" style="width: 100%;" />
</div>

#### Diverse audio present in this scene

``` cs
<audio controls>
  <source src="/themes/blist/static/ValentijnJacobs/Audio/JapaneseScene/harp-japanese-80bpm-85660.mp3" type="audio/mpeg">
  Your browser does not support the audio element.
</audio>
<audio controls>
  <source src="/themes/blist/static/ValentijnJacobs/Audio/JapaneseScene/frogs1-26828.mp3" type="audio/mpeg">
  Your browser does not support the audio element.
</audio>
<audio controls>
  <source src="/themes/blist/static/ValentijnJacobs/Audio/JapaneseScene/chirping-birds-ambience-217410.mp3" type="audio/mpeg">
  Your browser does not support the audio element.
</audio>
<audio controls>
  <source src="/themes/blist/static/ValentijnJacobs/Audio/JapaneseScene/bell-towerisolated-35572.mp3" type="audio/mpeg">
  Your browser does not support the audio element.
</audio>
```

*Egyptian Environment*
<div style="display: flex; gap: 50px;">
  <img src="Images/Images_GPE/MysteriousEgypt.png" style="width: 100%;" />
</div>

#### Diverse audio present in this scene

```cs
<audio controls>
  <source src="/themes/blist/static/ValentijnJacobs/Audio/EgyptScene/EgyptSound.mp3" type="audio/mpeg">
  Your browser does not support the audio element.
</audio>
<audio controls>
  <source src="/themes/blist/static/ValentijnJacobs/Audio/EgyptScene/Market sound.mp3" type="audio/mpeg">
  Your browser does not support the audio element.
</audio>
```

*Abandoned Island Environment*
<div style="display: flex; gap: 50px;">
  <img src="Images/Images_GPE/AbandonedIsland.png" style="width: 100%;" />
</div>

#### Diverse audio present in this scene

```cs
<audio controls>
  <source src="/themes/blist/static/ValentijnJacobs/Audio/IslandScene/brittany-island-seacost-23077.mp3" type="audio/mpeg">
  Your browser does not support the audio element.
</audio>
<audio controls>
  <source src="/themes/blist/static/ValentijnJacobs/Audio/IslandScene/049228_pirat-battlewav-62056.mp3" type="audio/mpeg">
  Your browser does not support the audio element.
</audio>
<audio controls>
  <source src="/themes/blist/static/ValentijnJacobs/Audio/IslandScene/Seagulls.mp3" type="audio/mpeg">
  Your browser does not support the audio element.
</audio>
<audio controls>
  <source src="/themes/blist/static/ValentijnJacobs/Audio/IslandScene/mystical-chime-196405.mp3" type="audio/mpeg">
  Your browser does not support the audio element.
</audio>
```

*Train Station Environment*
<div style="display: flex; gap: 50px;">
  <img src="Images/Images_GPE/WestTrainstation.png" style="width: 100%;" />
</div>

#### Diverse audio present in this scene

```cs
<audio controls>
  <source src="/themes/blist/static/ValentijnJacobs/Audio/TrainStationScene/SteamTrain.mp3" type="audio/mpeg">
  Your browser does not support the audio element.
</audio>
<audio controls>
  <source src="/themes/blist/static/ValentijnJacobs/Audio/TrainStationScene/horse-neigh-261131.mp3" type="audio/mpeg">
  Your browser does not support the audio element.
</audio>
<audio controls>
  <source src="/themes/blist/static/ValentijnJacobs/Audio/TrainStationScene/horse-snort-95874.mp3" type="audio/mpeg">
  Your browser does not support the audio element.
</audio>
```

# Conclusion

Throughout this research, we looked into how sound design can shape the player’s experience, specifically in video games when it comes to ambient sounds, spatial audio and all small environmental details that can bring a scene further to life. By diving into both academic sources and real world game practices, it became clear that sound isn’t just there to make things feel nice. Audio actually plays an enormous role in helping players make decisions during their playthrough, noticing aspects that wouldn't have been noticed otherwise and to help players stay focused during their gameplay.

When conducting the two seperate playtests, this became even more clear. Players mentioned how the spatial audio and ambient sounds made them feel more present in the environment compared to no audio at all. A lot of them were drawn to certain areas just because of the sounds they heard, which confirms how useful audio can be in guiding player's attention. Some players even noticed things they hadn’t seen before, simply because the audio laid their eyes on a direction.

All in all, this project shows that sound is much more than only background noise. It is a key part of gameplay that supports both the environment and how the player interacts with the world around them. The playtests really highlighted how impactful and intentional audio design can enhance immersion and even help shape how players move through a game.

## Sources

- [1] J. Studio, “Sound design in games,” Juego Studio, 2023. Available: <https://www.juegostudio.com/blog/sound-design-in-games>

- [2] R. Gate, “Audio influence on game atmosphere during various game events,” ResearchGate, 2021. Available: <https://www.researchgate.net/publication/349492251>

- [3] ACM Digital Library, “Game audio impacts on players’ visual attention,” ACM Transactions on Multimedia Computing, Communications, and Applications, 2022. Available: <https://dl.acm.org/doi/fullHtml/10.1145/3517031.3529621>

- [4] G. Pitstop, “The importance of sound design in video games,” Gaming Pitstop, 2023. Available: <https://www.gamingpitstop.com/post/the-importance-of-sound-design-in-video-games>

- [5] L. Geek, “The critical role of sound design in crafting immersive video games,” Land of Geek, 2023. Available: <https://www.landofgeek.com/posts/sound-design-in-video-games>

- [6] P. Toprac and A. Abdel-Meguid, “Causing fear, suspense, and anxiety using sound design in computer games,” IGI Global, 2010. Available: <https://www.igi-global.com/chapter/causing-fear-suspense-anxiety-using/46792>

- [7] P. Grimshaw, “The role of multi-channel audio in game sound,” IEEE Transactions on Consumer Electronics, vol. 56, no. 3, pp. 1834-1842, 2010. Available: <https://ieeexplore.ieee.org/document/5569853>

- [8] A. Jørgensen, “Fear and sound in video games,” Proceedings of the Audio Mostly Conference, ACM/IEEE, 2012. Available: <https://ieeexplore.ieee.org/document/6307672>
  
- [9] B. N. Walker and J. Lindsay, “Effectiveness of spatial audio cues in virtual environments,” IEEE Transactions on Human-Machine Systems, vol. 34, no. 2, pp. 152-159, 2004. Available: <https://ieeexplore.ieee.org/document/1287218>
