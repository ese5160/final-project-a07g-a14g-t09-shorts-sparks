# a07g-exploring-the-CLI

* Team Number: 9
* Team Name: Shorts & Sparks
* Team Members: James Steeman and Timothy Zhang
* GitHub Repository URL: [https://github.com/ese5160/final-project-a07g-a14g-t09-shorts-sparks](https://github.com/ese5160/final-project-a07g-a14g-t09-shorts-sparks)
* Description of test hardware: Macbook pro m2 (macOS) and lab desktops (windows) (development boards, sensors, actuators, laptop + OS, etc)

## 0 Install Percepio

## 1 Software Architecture

1. Revisit your Hardware and Software Requirements Specification (HRS & SRS) in A00G.
   Update the requirements based on the latest modifications to your project, and place the updated HRS & SRS in A07G_README.md.
2. Submit a block diagram outlining the different tasks into which you are dividing your software; below is an example:
3. Submit flowcharts or state machine diagrams briefly illustrating how each task operates; go to L10 Embedded I - Concurrency.pdf for an example.

Update the above as ### headings rather than a numbered list?

## 2 Understanding the Starter Code

1. What does “InitializeSerialConsole()” do? In said function, what is “cbufRx” and “cbufTx”? What type of data structure is it?
2. How are “cbufRx” and “cbufTx” initialized? Where is the library that defines them (please list the *C file they come from).
3. Where are the character arrays where the RX and TX characters are being stored at the end? Please mention their name and size.
Tip: Please note cBufRx and cBufTx are structures.
4. Where are the interrupts for UART character received and UART character sent defined?
5. What are the callback functions that are called when:
   1. A character is received? (RX)
   2. A character has been sent? (TX)
6. Explain what is being done on each of these two callbacks and how they relate to the cbufRx and cbufTx buffers.
7. Draw a diagram that explains the program flow for UART receive – starting with the user typing a character and ending with how that characters ends up in the circular buffer “cbufRx”. Please make reference to specific functions in the starter code.
8. Draw a diagram that explains the program flow for the UART transmission – starting from a string added by the program to the circular buffer “cbufTx” and ending on characters being shown on the screen of a PC (On Teraterm, for example). Please make reference to specific functions in the starter code.
9. What is done on the function “startStasks()” in main.c? How many threads are started?

## 3 Debug Logger Module

Commit your functioning Debug Logger Module to your GitHub repo, and make comments that are in Doxygen style.

## 4 Wiretap the convo

### Questions

1. What nets must you attach the logic analyzer to? (Check how the firmware sets up the UART in SerialConsole.c!)
2. Where on the circuit board can you attach / solder to?
3. What are critical settings for the logic analyzer?

### Hardware Photo

Submit a photo of your hardware connections between the SAMW25 Xplained dev board and the logic analyzer.

### Decoded Screenshot

Submit a screenshot of the decoded message.

### Small Capture .sal file

Submit a small capture file (i.e., the .sal file) of a wiretapped conversation (you don’t need to log 30 minutes worth of UART messages 🙂)

## 5 Complete the CLI

Commit your functioning CLI code to your GitHub repo, and make comments that are in Doxygen style.

## 6 Add CLI commands

### Code

Commit your functioning CLI code to your GitHub repo, and make comments that are in Doxygen style.

### Video Link

Submit a link to a video of this functionality in your README.md

## 7 Using Percepio

Submit a screenshot of your Percepio trace in your README file.
