---
layout: home
title: FPGA VGA Driver Project
tags: fpga vga verilog
categories: demo
---

This is a small college project where we were required to modify sample code to produce an image through using a Basys3 FPGA board.

## **Template VGA Design**
### **Project Set-Up**
Summarise the project set-up and design flow. Include a screenshot of your own set-up, for example see the image of my Project Summary window below. Guideline 1 short paragraph.

<img src="https://raw.githubusercontent.com/melgineer/fpga-vga-verilog/main/docs/assets/images/VGAPrjSum.png">
### **Template Code**
Outline the structure and design of the Verilog code templates you were given. What do they do? Include reference to how a VGA interface works. Guideline: 2/3 short paragraphs, consider including screenshot(s).
### **Simulation**
Explain the simulation process. Reference any important details, include a well-selected screenshot of the simulation. Guideline: 1/2 short paragraphs.
### **Synthesis**
Describe the synthesis and implementation processes. Consider including 1/2 useful screenshot(s). Guideline: 1/2 short paragraphs.
### **Demonstration**
Perhaps add a picture of your demo. Guideline: 1/2 sentences.

## **My VGA Design Edit**
My VGA design idea was to replicate the old analogue Tv Test Cards. Initially, I considered a simplified version inspired by original cards, but after discussion with my lecturer I realised a high fidelity replication was practically achievable with the use of AI tools. For my research I used google image search to find an reference image I liked [Test Card image](https://i0.wp.com/rewind.thetvroom.com/wp-rwnd/wp-content/uploads/2022/12/2rn-test-card-20181027-002-01.png?w=1850&ssl=1)

### **Code Adaptation**
Sample code

<img width="567" height="600" alt="image" src="https://github.com/user-attachments/assets/f64888d4-af1f-44a8-b5c0-723f9ba945d9" />

Output of sample code
<img width="1214" height="914" alt="image" src="https://github.com/user-attachments/assets/9d326b37-2c38-42bb-b863-63c2ab5946b4" />
<img width="438" height="105" alt="image" src="https://github.com/user-attachments/assets/552333ed-d527-4d0b-b732-46f965d40cd1" />

<img width="678" height="494" alt="image" src="https://github.com/user-attachments/assets/2e8210b5-8bac-48d3-9ad3-bebdf59ba22e" />

Added if statements to add a horizontal striped circle. Added Pythagorean theorem to get a distance from centre for my radius. 
<img width="1214" height="914" alt="image" src="https://github.com/user-attachments/assets/d4caa7e3-1b97-479a-9c25-7e37496ad9e2" />







Briefly show how you changed the template code to display a different image. Demonstrate your understanding. Guideline: 1-2 short paragraphs.
### **Simulation**
<img width="691" height="384" alt="Screenshot 2026-11-16 172520" src="https://github.com/user-attachments/assets/a4239d30-7a62-48fb-9dd6-9fa66c25af2f" />

Here the simulation shows the hsync and vid_on outputs are low at column 0x2d4(724). The hsync goes low to signal the end of one horizontal line in VGA standard. The colour values are FFF which outputs as white. This show the row signal increment at column 800( ie horizontal limit).     
<img width="934" height="230" alt="image" src="https://github.com/user-attachments/assets/ba85e56b-4860-4b77-b615-5df065a74a33" />

You can see here the columns increment every clock cycle.


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


