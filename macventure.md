- **Name:** Borja Lorente
- **Email:** blorente@ucm.es
- **Handle (IRC and wiki):** blorente
- **Phone:** (+34) 722 747 898
- **Possible Mentors:** [John Willis](http://wiki.scummvm.org/index.php/User:DJWillis), [Filippos Karapetis](http://wiki.scummvm.org/index.php/User:Md5)

# Add support for MacVenture games by reimplementing the WebVenture engine

*by Borja Lorente (blorente), 2016*

## Problem Statement and Goals

The ScummVM project currently does not support the original MacVenture games developed for the Macintosh 128k. However, there is already a modern implementation of these games that supports the original game files, the WebVenture engine. 

Most of the reverse engineering work for the games is [already done][2] in the WebVenture engine, but since it is written in JavaScript, a direct reimplementation is necessary for it's integration with ScummVM. In addition, the WebVenture engine already supports the Apple II versions of the games, making it possible for them to be added to the same engine in the respective ScummVM implementation.

Therefore, the goals of this project are:

- To write an engine in C++ to support these games, with a base in the existing JavaScript implementation.
- To integrate the engine with the existing ScummVM framework, so that it can support MacVenture games in the many platforms that ScummVM supports.

Most of the MacVenture games were pioneers in their respective genres (1), so the ScummVM community would benefit greatly from having access to these games as classics of their genres, for academic and nostalgic value.

## Implementation notes

The project will follow the structure of WebVenture to support both versions of the games, and it will take example of the WAGE engine already implemented in ScummVM, since it bears many similarities (both were for GUI-based games in the Macintosh). As happens with WebVenture, the engine will be only compatible with the original Macintosh and Apple II disk images, and will require them to play the games.

WebVenture implements abstractions for the main subsystems of the engine ([engine][3], [graphics][4], [controls][5], [sound][6], [text][7], etc.), and then specializations for each of the engines ([Macintosh][8], [AppleII][9]). This structure complies with the current structure of ScummVM engines, and therefore it can be directly adapted to a single engine that supports both versions.

Whenever possible, the project will follow a test-driven development model in which tests are written first as a form of specification and code is written later. This model offers the advantages of fast iterability and support for heavy refactoring (to handle the abstractions, as described later in the planning section) and ensures a certain level of quality within the product. Thus, the aim is to have fast (weekly or shorter) development cycles.

## Deliverables

- Core abstractions, for both versions (Macintosh 128k and Apple II):
    - Main loop of the game, representation of victory conditions.    
    - Internal representation of graphics (sprites) and game objects.
    - Script interpreter.
    - Windowing system (Drag and drop, window resizing)
    - Menu-based point-and-click controls.
    - Text and dialogue system.
    - Sound system.
    - Generic savefile handling.
    - Game detection.
 
- Macintosh 128k version:
    - Disk data and resource loading.
    - Graphics and sound specializations (e.g. color inversion).
    
- Apple II version:
    - Disk data and resource loading.
    - Graphics specializations (e.g. RGB colors, color inversion).

- Nice to have:
    - Debugger tool.
    
## Milestones

- **1.- Shadowgate** is winnable in the Macintosh version.
- **2.- All MacVenture games** are winnable in the Macintosh version.
- **3.- Shadowgate** is winnable in the Apple II version.
- **4.- All MacVenture games** are winnable in the Apple II version.
- **5.- The source code** is mergeable with the ScummVM repository.

## Plan

Taking advantage of the test-driven model described above, I will implement the Macintosh engine first, then aggresively refactor to abstract the subsystems mentioned above, and lastly implement the Apple II port support.

The development will focus on Shadowgate support as a main goal, and then add support for the other games as a separate milestone. 

- **May 23rd - May 29th**: 
    - Implement main loop of the game, and successfully add a new engine project to ScummVM.
    - Define an internal representation for game objects and graphics.

- **May 30th - June 5th**:
    - Implement game file data loading.
    - Implement windowing system.
    
- **June 6th - June 12th**:
    - Implement menus and menu-based controls.
    - Implement dialogue system.

- **June 13th - June 19th**: 
    - Implement sound system.
    - Implement script interpreter.  
    - Achieve Milestone 1.
    
- **June 20th - June 26th**:
    - Mid-term evaluation.
    - Add support and test the other MacVenture games.
    
- **June 27th - July 3rd**: 
    - Implement savegame support.      
    - Achieve Milestone 2.
    
- **July 4th - July 10th**:
    - Refactor the current code to abstract common components.
 
- **July 11th - July 17th**: 
    - Implement Apple II game data loading.
    - Implement Apple II graphics system.

- **July 18th - July 24th**:      
    - Extend the game interface to allow Apple II ports. 
    - Extend dialogue system to allow Apple II games.

- **July 25th - July 31st**: 
    - Implement Apple II sound system.

- **August 1st - August 7th**:  
    - Implement Apple II savegame system. 
    - Achieve Milestone 3.

- **August 8th - August 14th**: 
    - Add support and test the other Apple II games.
    - Achieve Milestone 4.
    
- **August 15th - August 22nd**:
    - Clean code to comply with ScummVM standards.
    - Write Doxygen documentation.
    - Achieve Milestone 5.

- **August 23rd - August 29th**:
    - Final evaluation.

## Availability and constraints

Currently, and until May 30th, I'll be taking classes at university. During this period, the number of hours I will be able to dedicate to the project is about 30, weekly. 

After that, and until June 30th, my exam period will take place. Despite the appearances, this is quite a relaxed period, since this semester most of the subjects are projects-based, and thus will be over before this date. I will be able to dedicate 40 weekly hours to the project.

From June 30th until the end of the program, I don't have any other significative commitment, so I'll be able to dedicate most of my time to the project, about 60 weekly hours. This is notably more time than in the other periods, so this period will be also reserved as a contingency period, should any important roadblock arise during development.

I will spend my time in Spain, so my timezone will be GMT + 1.

## Technical background

I am currently in my third year of college, at Universidad Complutense de Madrid, in Spain. The main languages used there are Java and C, but I have also taken classes taught in ARM7 assembly, C++ and JavaScript, among others. The highly theoretical approach my university takes ensures that the principles of good software design are prioritized over teaching particular languages. Therefore, I am able to pick up new languages really quickly.

In addition to that, I have done several side-projects, which I believe fit exactly with the profile needed for this project. Among others, these are:

- A [CHIP-8 emulator][10] in C++, which I made because I love working with old machines and languages, and thus I have the tools to understand and figure out the nuances of these games, and the systems they run on.
- Some [games and engines][11] in JavaScript, for one of my ongoing courses at university, which shows that I can understand game engines in general, and the WebVenture engine in particular.

A more complete list of projects can be found in [my portfolio][12]. 

I don't have mastery over C++, but the side-projects I've done and the fluency on C and Java that I aquired at University allow me to understand most of the complicated concepts with ease.

## Past Contributions to ScummVM
- Draft of  the MinGW64 compile guide for [the wiki.](http://wiki.scummvm.org/index.php/Compiling_ScummVM/MinGW-w64)
- [Pull Request (688)](https://github.com/scummvm/scummvm/pull/688)

## References

[1]: Shadowgate was the first "first person RPG" of it's kind. http://www.zojoi.com/shadowgate_macventure/ (description, second paragraph).
[2]: http://seancode.com/webventure/formats.html
[3]: https://github.com/blorente/webventure/blob/master/engine.js
[4]: https://github.com/blorente/webventure/blob/master/graphics.js
[5]: https://github.com/blorente/webventure/blob/master/controls.js
[6]: https://github.com/blorente/webventure/blob/master/sound.js
[7]: https://github.com/blorente/webventure/blob/master/text.js
[8]: https://github.com/blorente/webventure/tree/master/mac
[9]: https://github.com/blorente/webventure/tree/master/gs
[10]: https://bitbucket.org/Kerith/chip-towers
[11]: https://bitbucket.org/Kerith/dvi-labs
[12]: http://blorente.github.io

