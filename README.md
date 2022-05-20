# ⚡ A Ripple Carry Adder on a breadboard!

This was a mini project done over the course of a weekend after having had my interest in computer 
hardware spiked due to a course in computer system architecture that I was taking.

Let's do a quick rundown on how to create a basic 4-bit Ripple Carry Adder (RCA).

Construction of a half adder
============================

Let's start from the beginning by adding two 1-bit binary numbers
and then draw and fill in a function table.

![Addition av 1-bit tal och funktionstabellen för
additionen](https://user-images.githubusercontent.com/85518265/169586791-245b17a9-6a69-4501-a48c-152cacfc484b.png) ![Addition av 1-bit
tal och funktionstabellen för
additionen](https://user-images.githubusercontent.com/85518265/169586794-b3eef940-3a37-457a-a68c-33e2ecfedda0.png)

Notice how we can express the sum $s_{0}$ and
the carry $c_{1}$ algebraically as follows:

$$s_{0}\ =\ x_{0}\ \oplus\ y_{0}$$ 

$$c_{1}\ =\ xy$$

We can now easily construct a circuit that adds two 1-bit numbers:

![circuit for a half adder](https://user-images.githubusercontent.com/85518265/169586796-ef6a682d-7996-4337-8f4c-04ace48fcf06.png)

The circuit in the above figure is called a *half adder* A half adder does not do the job though because it can't take into account potential carry in bits, that's not good!

Construction of a full adder
===========================

So let us improve our half adder by complementing the circuit with what is missing. To do what we must first find out what's missing and how to add it. Let's investigate by creating a truth table and a Karnaugh map.

![function table and karnaugh map of a full adder](https://user-images.githubusercontent.com/85518265/169586795-a696fa6b-631a-4d31-8377-2737f5920b70.png)

After having generated a boolean expression in disjunctive minimal form we obtain the following expressions for the sum and the carry:

$$s_{0}\ =\ x_{0}\ \oplus\ y_{0}\ \oplus\ C_{in}$$

$$c_{out}\ =\ x_{0}y_{0}\ +\ C_{in}(x_{0}\ \oplus\ y_{0}) $$

We can now easily construct a circuit to add two 1-bit numbers where we can also take into account a potential carry in bit.

![circuit for a full adder](https://user-images.githubusercontent.com/85518265/169586792-0b652493-3cca-4571-9ba7-c6d2a68f5d57.png)

Construction of a 4-bit Ripple Carry Adder (RCA)
==============================

Okay, we know how to construct a circuit that adds two 1-bit
binary numbers where we also take into account any incoming
carry. The cool thing about a full adder is that once you know 
how to build one you can just copy it several times to construct an n-bit adder.
In the case of a 4-bit adder we just have to replicate it three more times!

![box diagram of a 4-bit ripple carry adder](https://user-images.githubusercontent.com/85518265/169586788-a9b2e402-7541-4be0-891c-1e8e80305d9b.png)

In the below figure we can see the actual circuit. It may at first glance seem advanced but if you just spend a 
little bit of time with it, it'll become easy to understand. The basic component of the adder is the *full adder* which generates a
sum bit and a carry bit. The only thing we're doing in the 4-bit RCA is to connect four full adders. The carry from the result of one full adder 
gets fed right into the next full adder in line. In the end we end up with four
sum bits $\{s_{3},\ s_{2},\ s_{1},\ s_{0}\}$ and one carry bit $\{c_{4}\}$ that together define a binary number.

![Nätet för en 4-bit adderare](https://user-images.githubusercontent.com/85518265/169586786-99c45695-48a0-4932-8865-bba42a4d3f99.png)

The 4-bit adder on a breadboard
===============================
Now that we know how a Ripple Carry Adder works and is built, let's actually build it on a breadboard!

The left most switch in the below wiring diagram represents the four bits ${x_{3},\ x_{2},\ x_{1},\ x_{0}}$ for the first 4-bit binary number. The switch to the 
right of it represents the four bits ${y_{3},\ y_{2},\ y_{1},\ y_{0}}$ for the other 4-bit binary number. The two numbers get added and 
the output is shown on the LEDs to the right as a binary number.

Wiring diagram
---------------

![Kopplingsschemat](https://user-images.githubusercontent.com/85518265/169586780-3a40cdd2-edea-41ed-a997-ade928f0a9de.png)

The actual thing on a breadboard
---------------
On the image below we can see the final product in real life.
The first number (right-most switch) is $x=1010_{2}=10_{10}$ and the second number is $y=0101_{2}=5_{10}$ and the sum ($11110_{2}=15_{10}$) is shown on the LEDs on the left.

![The final product on a real life breadboard](https://user-images.githubusercontent.com/85518265/169590740-a3081a05-6ff5-47c9-95b0-8b81d2949ed9.jpg)

Components
-----------

-   2x 74HC86 **Quad two-input XOR-gate** (CMOS)

-   2x 74HC08 **Quad two-input AND-gate** (CMOS)

-   1x 74HC32 **Quad two-input OR-gate** (CMOS)

-   2x 4-position DIP-switch (SPST)

-   5x LEDs

-   5x 1k$\Omega$ resistor (for LEDs)

-   5x 10k$\Omega$ resistor (pull-up resistors for IC inputs)

-   1x Breadboard

-   24 gauge wire

-   5v power source
