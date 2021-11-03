# Logisim Snake
Simulation of a Snake game using an educational tool for designing and simulating digital logic circuits - [Logisim](http://www.cburch.com/logisim/).

This project shows how a simple game like *Snake*🐍 can be designed with logic circuits using only necessary and minimal components.

![This is an image](https://raw.githubusercontent.com/stevomitric/Logisim-Snake/main/docs/sample1.png)


## Project structure
Main file contains 4 base components:
- LED Matrix
- CONTR (UI Controller)
- KONT_IZLAZ (Drawing unit)
- Control buttons
Basic components such as registers, multiplexers and decoders are used from ETF library included in the project.
Adjusting clock speed, which by default is set to 1 KHz, can alter the game speed (higher frequencies require more CPU power to simulate).

#### LED Matrix
Contains 32x32 LEDs that act as a screen on which the game plays. Each row is controlled by a 32 bit value connected to it, and all rows are connected to KONT_IZLAZ component which draws the game.

#### CONTR
Takes in signals from UI buttons and adjusts snake's movement accordingly. This component also has two 5 bit registers for positioning the snake on the screen. These values are sent to the KONT_IZLAZ component for drawing.

#### KONT_IZALZ
Draws the snake on the screen by using head position coordinates and outputting them to LED matrix. Consists of 2 components:
- KONT_MEM
- REG1024_LD

###### KONT_MEM
Position values are saved with 3 RAMs, one for X values, one for Y values and one that counts how many ticks will the saved position last on the screen. Each iteration, third RAM will decrease all of its positive values so it gives an illusion of a moving snake (animation).

![This is an image](https://raw.githubusercontent.com/stevomitric/Logisim-Snake/main/docs/sample2.png)

To iterate and decrease all values within one tick, KONT_MEM runs on a faster clock value.

###### REG1024_LD
A very small memory module composed of 32 registers that hold 32 bit values. This memory component can set/clear each individual bit and it outputs all its contents in the form of a 32x32 bit value for the LED Matrix.
