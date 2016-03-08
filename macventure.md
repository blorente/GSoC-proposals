- **Name:** Borja Lorente
- **Email:** blorente@ucm.es
- **Handle (IRC and wiki):** blorente
- **Phone:** (+34) 722 747 898

# Add support for MacVenture games via WebVenture engine.

_by Borja Lorente (blorente), 2016_

## Goals

The ScummVM project currently does not support the original MacVenture games developed for the Macintosh 128k. However, there is already a modern implementation of these games that supports the original game files, the WebVenture engine. 

Most of the reverse engineering work for the MacVenture games is already done in the WebVenture engine, but since it is written in JavaScript, a direct port is necessary for it's integration with ScummVM. In addition, the WebVenture engine already supports the Apple II versions of the games, making it possible for them to be added to the same engine in the respective ScummVM implementation.

Therefore, the goals of this project are:

- To write an engine in C++ to support these games, with a base in the existing JavaScript implementation.
- To integrate the engine with the existing ScummVM framework, so that it can support MacVenture games in the many platforms that ScummVM supports.

Most of the MacVenture games were pioneers in their respective genres (1), so the ScummVM community would benefit greatly from having access to these games as classics of their genres, for academic and nostalgic value.

## Implementation notes

The project will follow the structure of WebVenture to support both versions of the games. 

WebVenture implements abstractions for the main subsystems of the engine ([engine][2], [graphics][3], [controls][4], [sound][5], [text][6] etc. subsystems) and then specializations for each of the engines ([Mac][7], [AppleII][8]). This structure complies with the current structure of ScummVM engines, and therefore it can be directly adapted.

The project will follow a test-driven development model in which tests are written first as a form of specification and code is written later. This model offers the advantages of fast iterability, support for heavy refactoring (to handle the abstractions, as described later in the planning section) and ensure a certain level of quality within the product. Thus, the aim is to have fast (weekly or shorter) development cycles.

## Deliverables

- Core abstractions, for both versions (Macintosh 128k and Apple II):
    - Main loop of the game, representation of victory conditions.    
    - Internal representation of graphics (sprites) and game objects.
    - Windowing system (Drag and drop, window resizing), based upon the current Tinsel implementation.
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

The development will focus on Shadowgate support as a main goal, and then add support for the other games.

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
    - Extend the interface to allow Apple II ports. 
    - Extend dialogue system to allow Apple II games.

- **July 25th - July 31st**: 
    - Implement Apple II sound system.

- **August 1st - August 7th**:  
    - Implement Apple II savegame system. 
    - Milestone 3 reached.

- **August 8th - August 14th**: 
    - Add support and test the other Apple II games.
    
- **August 15th - August 22nd**:
    - Clean code to comply with ScummVM standards.
    - Write Doxygen documentation.
    - Achieve Milestone 5.

- **August 23rd - August 29th**:
    - Final evaluation.

## Availability and constraints

Currently, and until May 30th, I'll be taking classes at university. During this period, the number of hours I will be able to dedicate to the project is about 30, weekly. 

## Technical background

## [Pull Request](https://github.com/scummvm/scummvm/pull/688)

## References

[1]: Shadowgate was the first "first person RPG", http://www.zojoi.com/shadowgate_macventure/ (description, second paragraph).
[2]: https://github.com/blorente/webventure/blob/master/engine.js
[3]: https://github.com/blorente/webventure/blob/master/graphics.js
[4]: https://github.com/blorente/webventure/blob/master/controls.js
[5]: https://github.com/blorente/webventure/blob/master/sound.js
[6]: https://github.com/blorente/webventure/blob/master/text.js
[7]: https://github.com/blorente/webventure/tree/master/mac
[8]: https://github.com/blorente/webventure/tree/master/gs

