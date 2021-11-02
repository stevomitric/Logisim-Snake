# Logisim Snake
A simulation of Snake game using educational tool for designing and simulating digital logic circuits.

This project shows how a simple game like Snake can be designed with logic circutes using only necessary components 🐍.

![This is an image](https://raw.githubusercontent.com/stevomitric/Logisim-Snake/main/docs/sample1.png)


## Project structure
Main file contains 4 base components: LED Matrix, CONTR, KONT_IZLAZ, Control buttons. Basic components such as registors, multiplexers and decoders are used from ETF library included in the project.
Clock speed is set to 1 KHz.

#### LED Matrix
Contains 32x32 LEDs that act as a screen on which the game plays. Each row is controled by a 32bit value connected to it, and all rows are connected to KONT_IZLAZ component which draws the game.

#### CONTR
Takes in signals from UI buttons and adjusts snakes movement accordingly. This component also has base registors for positioning the snake. These values are are sent to the KONT_IZLAZ component for drawing.

#### KONT_IZALZ
Draws the snake on screen by using head position coordinates and outputing values for LED matrix. Consists of 2 components: KONT_MEM, REG1024_LD

###### KONT_MEM
Position values are saved with 3 RAMs, one for X values, one for Y values and one that counts how many ticks will the saved position last on screen. Each iteration, third RAM will decrease all of its values so it gives an ilusion of a moving snake (animation).

![This is an image](https://raw.githubusercontent.com/stevomitric/Logisim-Snake/main/docs/sample2.png)

To iterate all values within one tick, KONT_MEM runs on a faster clock value.

###### REG1024_LD
A very small memory module composed of 32 registers that hold 32 bit values. This memory component can set/clear each individual bit and it outputs all its contents in form of a 32x32 bit value for the LED Matrix.
