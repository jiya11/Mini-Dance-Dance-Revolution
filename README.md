# Mini Dance Dance Revolution 

This project is a two-player, hardware recreation of the classic Dance Dance Revolution (DDR) arcade game, built entirely in Verilog HDL on a DE1-SoC FPGA board. This project blends digital design, real-time input handling, VGA graphics, synthesized audio, and system-level integration on custom logic.

## 🎮 Game Overview
Mini DDR reimagines the arcade experience: arrows scroll up a split VGA display, and two players compete to match their button presses to the on-screen prompts. The FPGA processes physical inputs in real time, evaluates player accuracy with cycle-level precision, and updates scores instantly, all while delivering synchronized music and visual feedback.

The game is structured as five core subsystems, each implemented as a separate Verilog module:

1. 🕹️ Input Processing
   Each player uses four dedicated push-buttons (up, down, left, right), connected via GPIO pins. Dual-stage synchronizers and robust debouncing circuits filter out noise and ensure accurate hit detection. The debouncing implementation begins with a dual-flip-flop synchronizer to prevent metastability, followed by a 20ms stability counter implemented as a 500,000 cycle counter at 50MHz. The counter only increments when input remains stable and resets on any transition, with separate counters maintained for each button to ensure independent processing. Debounced states are mirrored on onboard LEDs for both players.
   <img src="https://github.com/user-attachments/assets/1ac4781a-c991-48f7-b4eb-6479be1f5edc" alt="Pushbuttons" width="500"/>

2. ⬆️ Arrow Generation and Timing
   Pseudo-random pattern generators launch arrows at precise intervals, moving them smoothly toward the target zone. Dedicated timing logic ensures all arrow movement and event checking are precisely synchronized.

3. 🏆 Scoring System
   Scores are updated instantly by matching player inputs to arrow positions in the target zone. Hits and misses are tracked, with real-time scores displayed on the 7-segment displays.

4. 🖥️ Video Display (VGA Output)
   The VGA controller renders all game visuals in real time (no frame buffers or external memory required). The screen is split for two-player mode at 160x120 resolution and 3-bit color depth, with layered graphics for backgrounds, target zones and color-coded arrows. Arrow sprites are generated through precise boolean equations that define each pixel position, eliminating the need for sprite storage in memory.

5. 🎶 Audio Output (Music and Effects)
   The audio system generates fully synthesized game music at 90 BPM using an A minor pentatonic scale with real-time sound effect integration and multi-channel mixing. The frequency values for each note have been carefully calculated to ensure perfect pitch.

## Watch the Demo below!
[![Watch the demo](https://github.com/user-attachments/assets/2cb2ca87-02c3-4d75-bc42-774e0cdba3b0)](https://youtu.be/lD32fzIGciU?feature=shared)

# Academic Integrity Notice
This project was created as coursework for ECE241 at the University of Toronto. The code and documentation are provided for reference only and are not licensed for use, modification, or distribution. All rights reserved.
