# Software-Engineer

#### Technical Skills: Python, SQL, AWS, Snowflake, MATLAB

## Education
- Game Development Bootcamp | Playback Studio (_2023_)								       		
- UE5 C++ Developer course | Udemy/Epic Games (_2022_)	 			        		
- CS50x Computer Science course | Harvard University (_2022_)
- Bachelor of Engineering | University of Portsmouth (_2020_)

## Work Experience
**Gameplay Software Engineer Intern • Nerd Monkeys (_January 2024 - May 2024_)**
- Excellent reasoning and complex problem-solving ability when presented with challenging scripting tasks showing tenacity and taking ownership of my work.
- Showed initiative through debugging and expanding on existing code.
- Tested and improved gameplay features.
- Improved teamwork ability by brainstorming with others how to implement game design ideas into code/gameplay mechanics.

**Founder/Developer/Designer • Bloqi (_February 2023 - Present_)**
- Social platform bringing a Twitter-like experience to the TikTok generation in university.
- Managed the product development process from design to beta testing, showcasing strong team spirit and project management skills.
- Designed the UI using Figma. Developed first version of app in Flutter in less than a month.
- Built front-end app infrastructure using GetX state-management, later refactoring to BloC.
- Iterating rapidly on product and associated media enabled progression through multiple stages of King’s College’s Idea Factory Incubator and sustained interest in potential investors and a judge at the finals, achieved through sheer drive and determination.

## Projects
### 2D Box-Pushing Puzzle Game
[Publication](https://www.mdpi.com/1424-8220/22/8/3048)

While working as gameplay programmer at Nerd Monkeys I worked on several projects, one being So Cold Barn. During this time I was introduced to many gameplay programming concepts such as how C# events give more control and allow multiple functions to be called from different scripts. I was also able to improve my teamwork skills and brainstorm with other programmers (some more experienced than me) how we can turn requested features into fruition, mainly via scripting. Along the way, I improved my debugging skills within code and game engine integration. This required a deep understanding of the scripts (including ones I did not work on previously) in order to find the issue and implement a solution. I enjoyed the creativity from working on gameplay features as well finding creative solutions to bugs. Below is a script I made to spawn a number of consumables (pills, in this case) into a level based on the previous level's completion percentage.



![EEG Band Discovery](/assets/img/eeg_band_discovery.jpeg)

### 2D Side-Scrolling Platform Game
[Publication](https://www.mdpi.com/1424-8220/22/11/4240)

During the Game Development Bootcamp with Playback Studio, we were tasked with making our own complete game. Through trial and error and researching specific features I wanted for my game, I became very comfortable with Unity and C# and I believe this method of learning was much more valuable than doing a course or traditional learning. Such features I explored in this game were: AI enemies, cliff detection, player attack detection, parallax background, particle system, health and damage for characters, player movement, character animations and rigging characters. Below is the C# code for my "damageable" script, which enables my player and enemies to take damage to their health when hit.

### Bloqi - Text-Based Social Media App
[Publication](https://www.mdpi.com/1424-8220/22/11/4240)

Figma/Flutter/Dart: UI development of a social platform bringing a Twitter-like experience to the TikTok generation in university. Designed the UI within Figma, to be simple and easy to use. The goal was to be as minimalistic as
possible without losing function. I then integrated the UI into a working version of the app using Flutter/Dart with BloC state-management, while stil maintaining the look and feel of the UI/UX and easy navigation with swipe and 
drag gestures.

### 3D Simple Shooter Game
[Publication](https://www.mdpi.com/1424-8220/22/11/4240)

The clip above shows a short shooter game where the objective is to kill all the enemies. Developing this game helped me better understand shooting mechanics, AI characters, player and character movement and animation. Using the 
animation event graph and syncing animation to character movement proved to be challenging, however after experimentation and reseach I am much more comfortable using these functions of Unreal Engine. Below is the C++ "ShooterCharacter" class I used for movement, damage to health and aiming.

### First Person Puzzle Game
[Publication](https://www.mdpi.com/1424-8220/22/11/4240)

I created this game to improve my skills using modular level design. Using the asset pack I designed a dungeon and crypt where the objective of the game is to venture into the dungeon and retrieve a valuable statue. During the process of making this game I became competent in use line traces and collisions as well as debug tools such as a debug sphere (as seen in the video above). Such tools improved my debugging and problem-solving skills. I came across an issue where the item grabbed and dropped into the secret wall wouldnt trigger the wall to move down. I solved this by turning off physics to that particular item when it enters a certain area and "sticks" to the bottom surface. I found that even simple issues like this were satisfying to solve and maintained my excitement to make more games. Below is the script for the "Grabber" component, where I used tags for when an item is grabbed and debug lines and spheres to see when something is picked up and released and to show the grabbable distance.

### 3D Third Person Obstacle Course Game
[Publication](https://www.mdpi.com/1424-8220/22/11/4240)

Near the beginning of my game development journey I learnt the basics of developing a game using blueprints and C++. I practiced functions, variables, branches in C++ and creating C++ Actors. I also, learnt how to link Blueprint to C++. I thoroughly enjoyed the level design aspect of this game which was designing the obstacle course for my character. Below is the script for a moving platform.

### 3D Tank Shooter Game
[Publication](https://www.mdpi.com/1424-8220/22/11/4240)

In this game, you control a small toon-like tank and move around with tank-like movement to shoot turrets, once all the turrets are destroyed you win the game, however the turrents lock onto you and shoot back when you come within range. While developing this game I learnt how to use a "fire" functionality with projectiles, add special effects like smoke, explosions and SFX and add enemy AI controlled turrets to the game. With various issues I encountered while making this game, one of them was the projectile getting stuck on the actor when clicking to fire. I found that it is common practice to spawn projectiles with a bit of distance from the actor so they do not collide with the actor and get stuck. I find that experiencing and learning these kind of things helps me become a better game developer. Below is the script for a projectile.
