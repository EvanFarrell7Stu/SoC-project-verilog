---
layout: home
title: FPGA VGA Driver Project
tags: fpga vga verilog
categories: demo
---

This is a small college project where we were required to modify sample code to produce a VGA graphic using a Basys3 FPGA board as a VGA controller.

## **Template VGA Design**
### **Project Set-Up**

Project used a Basys3 dev board with a Artix-7 xc7a35tcpg236-1 FPGA.

The design flow is as follows: 
- Simulation-Use simulation of Verilog code to see if code outputs as expected.
- RTL Analysis-Analyses code and produces a schematic of the modules
- Synthesis-Produces a logic diagram with registers, logic gates, etc.
- Implementation-Plots how the program will be implemented on the physical FPGA
- Program-Generate bitstream and program FPGA


The templates provided include a VGASync module, which controls the scanning of the display. It sets parameters for the display dimensions and the horizontal and vertical counting limits. It also generates and assigns the row and column output values, which represent the current pixel position on the display. Also it controls the hsync, vsync and vid_on variables which control synchronisation and blanking time of the output.  

There are also two sample modules provided. The one my project is based on is the VGAColourStripes module. This module uses combinational logic to assign values to the red, green and blue net variable. It also contains sequential logic which, at each positive clock edge, assigns the next red, green and blue values to their respective registers.

The VGA top module then instantiates the VGASync module, the ColourStripes module and the clock wizard(configured to 25MHz in the Vivado software). It connects these modules together and outputs the red, green and blue colour signals, along with the horizontal and vertical synchronisation signals (HSYNC and VSYNC). Also the binary vid_on signal fron the VGASync module determines whether assigned colour values are displayed or a value of 000(black) is displayed. 
<img width="691" height="384" alt="Screenshot 2026-11-16 172520" src="https://github.com/user-attachments/assets/f23a0743-77a0-4bdd-a546-bb3445d50124" />

Here we see vid_on=0 meaning nothing displayed as we are outside the display range(0-639) on the first row(000). The column number is 0x2D4(724) which puts it beyond the display+front porch range of 0-655. This means hsync is brought low for one pulse to signal to monitor the row has ended for syncing.


Basically, the VGA draws an image one pixel at a time, scanning from left to right and top to bottom. The HSYNC signal indicates the end of each horizontal line, while the VSYNC signal indicates the end of a complete frame. The vid_on signal controls the blanking intervals, allowing the monitor to synchronise its output with the appropriate lines and frames.
### **Simulation**
The simulation process uses a testbench file to instantiate modules and provide a clock signal all in the application. It displays a simulated waveform allowing you to test the program without having to program the physical FPGA. This allows you to check the values of counters, signals and your registers at different times(image displays values at 7.235 us) and see if they work as expected.

<img width="691" height="384" alt="Screenshot 2026-11-16 172520" src="https://github.com/user-attachments/assets/f23a0743-77a0-4bdd-a546-bb3445d50124" />

The simulation waveform here shows the column counter incrementing on each clock cycle. And then after 800 clock cycles it resets to zero and row counter increments to the next row. It demonstrates that the hsync goes low and the vid_on goes low when they are outside the display range+front porch and the display range respectively. 

The waveform also displays the register values, with different colours used to distinguish the signals and make their values easier to follow. This makes it possible to examine **how the signals change over time** and identify any unexpected behaviour.
### **Synthesis and Implementation**
- Synthesis-Takes the Verilog RTL design and converts it into a logic diagram with registers, logic gates, etc.
- Implementation-Plots how the program will be implemented on the physical FPGA. Allows you to generate a bitstream.


## **My VGA Design Edit**
My VGA design idea was to replicate the old analogue Tv Test Cards. Initially, I considered a simplified version inspired by original cards, but after discussion with my lecturer I realised a high fidelity replication was practically achievable with the use of AI tools. For my research I used google image search to find an reference image I liked [Test Card image](https://i0.wp.com/rewind.thetvroom.com/wp-rwnd/wp-content/uploads/2022/12/2rn-test-card-20181027-002-01.png?w=1850&ssl=1)

### **Code Adaptation**
Sample code

<img width="567" height="600" alt="image" src="https://github.com/user-attachments/assets/f64888d4-af1f-44a8-b5c0-723f9ba945d9" />

Output of sample code
<img width="1214" height="914" alt="image" src="https://github.com/user-attachments/assets/9d326b37-2c38-42bb-b863-63c2ab5946b4" />
<img width="438" height="105" alt="image" src="https://github.com/user-attachments/assets/552333ed-d527-4d0b-b732-46f965d40cd1" />

<img width="678" height="494" alt="image" src="https://github.com/user-attachments/assets/2e8210b5-8bac-48d3-9ad3-bebdf59ba22e" />

Added if statements to add a horizontal striped circle. These if statements were placed at the end of the combinational logic to overwrite to early vertical stripes values for those pixels. Added Pythagorean theorem to get a radius squared value to determine circle size. 
<img width="1214" height="914" alt="image" src="https://github.com/user-attachments/assets/d4caa7e3-1b97-479a-9c25-7e37496ad9e2" />

Using an AI tool I generated a series of if statements based off the reference image of the tv test card. Here is a sample
<img width="572" height="366" alt="image" src="https://github.com/user-attachments/assets/a3e9c627-c8eb-40ea-9670-df49a1624e5b" />








Briefly show how you changed the template code to display a different image. Demonstrate your understanding. Guideline: 1-2 short paragraphs.
### **Simulation**
<img width="691" height="384" alt="Screenshot 2026-11-16 172520" src="https://github.com/user-attachments/assets/a4239d30-7a62-48fb-9dd6-9fa66c25af2f" />

Here the simulation shows the hsync and vid_on outputs are low at column 0x2d4(724). The hsync goes low for a period to signal the end of one horizontal line for the monitor to synchronie with the next line. The colour values are RGB FFF which outputs as white. This show the row signal increment(000 -> 001) at column 800( ie horizontal limit). 
<img width="934" height="230" alt="image" src="https://github.com/user-attachments/assets/ba85e56b-4860-4b77-b615-5df065a74a33" />

You can see here the columns increment every clock cycle. It is hard to see here but it increments on the positive clock edge.


Show how you simulated your own design. Are there any things to note? Demonstrate your understanding. Add a screenshot. Guideline: 1-2 short paragraphs.
### **Synthesis**
Describe the synthesis & implementation outputs for your design, are there any differences to that of the original design? Guideline 1-2 short paragraphs.
### **Demonstration**
<img width="1214" height="914" alt="image" src="https://github.com/user-attachments/assets/ddbea7f1-c12b-4d64-b49a-22c2b7c79cfe" />

This is the finished product. It is displayed in 4:3 aspect ratio to have the correct representation of a 640x480 image.

## **More Markdown Basics**
This is a paragraph. Add an empty line to start a new paragraph.

Font can be emphasised as *Italic* or **Bold**.

Code can be highlighted by using `backticks`.

Hyperlinks look like this: [GitHub Help](https://help.github.com/).

A bullet list can be rendered as follows:
- vectors
- algorithms
- iterators


