#Introduction to Digital Circuit:

##Logic operations and logic gates:
Draw circuits using cascading design (commonly used for large circuit)

Example:
Half bit adder

![Half- BitAdder](https://github.com/ksuhartono97/Class-Notes/blob/COMP2611/COMP2611/resources/unit1/halfbitadder.png)

In circuits  a filled dot (.) in the lines signify a split in the circuit (it carries the same signal).
Meanwhile an unfilled dot(0) signify the input signal or output signal.
For **representation** only.

Electronic signal is digital, thus can be represented with binaries (0 = deasserted, 1 = asserted)
>Typical voltage: 
>**1** : 2.4V-2.9 V | 
>**0** : 0 V-0.5 V

Truth table : Diagram in rows or columns that shows how the truth
or falsity of a proposition (output) varies with that of its
components

Logic function : function on binary variables whose output is
also binary

**Fundamental** operations :
- AND (.)
- OR (+)
- NOT (<img src="https://www.sciweavers.org/tex2img.php?eq=%20%5Cbar%7Ba%7D%20&bc=White&fc=Black&im=jpg&fs=12&ff=arev&edit=0" align="center" border="0" alt=" \bar{a} " width="15" height="15" />) (line on top of the operation) (here we will denote
NOT with !)

![Fundamental gates](https://sub.allaboutcircuits.com/images/quiz/01249x02.png)

### Simplifying Logic Equations
Methods: 
- Boolean Algebra
- Karnaugh maps (K-maps)

####Boolean Algebra

Basic laws of boolean algebra:

Main operations of boolean algebra:
- Conjunction, denoted as ∧
- Disjunction, denoted as ∨
- Negation, denoted as ¬

![Basic Laws](https://www.kullabs.com/uploads/symmetries-in-boolean-algebra-html-m64e32966.gif)

####Karnaugh Maps(K-maps)

Constructed in the form of a table whose ends are connected. All K-maps
must be written following the constraints of the **gray code**

>Gray Code: During the writing of bits on a K-map you may only have one variable difference.

K-map property: It is toroid ( rightmost cells are adjacent to the leftmost cells
and topmost cells are adjacent to bottom cells)

Example

| A\BC | 00 | 01 | 11 | 10 |
|------|----|----|----|----|
|   0  |    |    |    |    |
|   1  |    |    |    |    |

Notice how as the columns shift, only one bit on either B or C are changed at a time.
This is a K-map that fulfills the gray code.

The process of simplification in K-maps:
1. Construct the K-map from your truth table outputs.
2. Circle together all the 1 values until all 1s are circled. Rule of making the circle: the number of 1s inside one circle
 must be the power of 2, e.g.: 2, 4, 8, .... and also, the 1s have to be adjacent. PRIORITIZE LARGER GROUPS OVER SMALLER GROUPS
3. Observe the circles, the bits that don't change (meaning that it influences the output) are taken as an AND statement, and the ones
that change are left behind.
4. All circles must be observed, the ANDed result are joined together with OR operators.

Example K-map:

| A\B  | 0 | 1 |
|------|---|---|
|   0  | 0 | 1 | 
|   1  | 1 | 1 |

First circle on r2: c1 and c2. Second circle : r1 and r2 : c2

First circle result: A

Second circle result: B

K-map output: A + B

Sample K-map layouts:

| A\BC | 00 | 01 | 11 | 10 |
|------|----|----|----|----|
|   0  |  m0 | m1   | m3   | m2   |
|   1  |  m4  | m5   | m7  | m6   |

| AB\CD | 00 | 01 | 11 | 10 |
|------|----|----|----|----|
|   00  | m0   |  m1 |  m3  | m2   |
|   01  |  m4  | m5   | m7   | m6   |
|   11  |  m12  |  m13  | m15   |  m14  |
|   10  |  m8  | m9   | m11   | m10   |

Another K-map example:

| A\BC | 00 | 01 | 11 | 10 |
|------|----|----|----|----|
|   0  |  0 | 0  | 1  | 0   |
|   1  |  0 | 1  | 1  | 1   |

3 circles:
- r1 and r2 : c3
- r2 : c2 and c3
- r2 : c3 and c4

Observing the circles, we can discern:
- BC
- AC
- AB

Thus output of K-map is : BC + AC + AB

##Digital Logic Circuits

Two types of digital logic circuits in a computer:
- Combinational Logic Circuit:
    - **No** memory
    - Output depends on **circuit** and **input**
    - Can be specified with an equation or truth table
- Sequential Logic Circuit:
    - **Has** memory
    - Output depends on input and value in memory(state)
    
####Combinational Logic Circuits:
Examples: 
- Multiplexers
- Encoders and Decoders
- Two-level logic and PLAs (Programmable Logic Array)

Can be implemented with AND, OR, NOT gates only.

#####Multiplexer: 
Selects one of the data inputs as output by a control input value.
Can have an arbitrary number of inputs.
> Two data inputs require one selector input.
> N data inputs require log<sub>2</sub>n selector inputs.

Example:

![2 input multiplexer](http://np6.nfshost.com/uploads/cycle0_2inputMux.png)

Truth Table:

| S | A | B | C |
|---|---|---|---|
| 0 | 0 | 0 | 0 |
| 0 | 0 | 1 | 0 |
| 0 | 1 | 0 | 1 |
| 0 | 1 | 1 | 1 |
| 1 | 0 | 0 | 0 |
| 1 | 0 | 1 | 1 |
| 1 | 1 | 0 | 0 |
| 1 | 1 | 1 | 1 |

####Decoder:
Logical block with a n-bit input and 2<sup>n</sup> 1-bit outputs.
Output that corresponds to input bit is true when everything else is false

Ex:
2-4 decoder

![2-4 decoder](http://sub.allaboutcircuits.com/images/04462.png)

| A<sub>1</sub> | A<sub>0</sub> | D<sub>3</sub> | D<sub>2</sub> | D<sub>1</sub> | D<sub>0</sub> |
|---|---|---|---|---|---|
| 0 | 0 | 0 | 0 | 0 | 1 |
| 0 | 1 | 0 | 0 | 1 | 0 |
| 1 | 0 | 0 | 1 | 0 | 0 |
| 1 | 1 | 1 | 0 | 0 | 0 |

Encoders works in the **opposite** way!

####Two-level Representation:
_**Any**_ logic function can be expressed as a two-level representation:
- Every input is either variable or its negated form
- One level consists of **AND** gates only
- The other consists of **OR** gates

#####Sum of Products Representation: 
<img src="http://www.sciweavers.org/tex2img.php?eq=%28A%20%20%5Cbullet%20B%20%5Cbullet%20%5Cbar%7BC%7D%29%20%20%2B%20%28A%20%5Cbullet%20C%20%5Cbullet%20%20%5Cbar%7BB%7D%29%20%2B%20%28B%20%5Cbullet%20C%20%5Cbullet%20%5Cbar%7BA%7D%29&bc=White&fc=Black&im=jpg&fs=12&ff=arev&edit=0" align="center" border="0" alt="(A  \bullet B \bullet \bar{C})  + (A \bullet C \bullet  \bar{B}) + (B \bullet C \bullet \bar{A})" width="285" height="21" />

More commonly used than product of sums.

#####Product of Sums Representation:
<img src="http://www.sciweavers.org/tex2img.php?eq=%28A%20%20%2B%20B%20%2B%20%5Cbar%7BC%7D%29%20%20%5Cbullet%20%28A%20%2BC%20%2B%20%5Cbar%7BB%7D%29%20%5Cbullet%20%28B%20%2B%20C%20%2B%20%5Cbar%7BA%7D%29&bc=White&fc=Black&im=jpg&fs=12&ff=arev&edit=0" align="center" border="0" alt="(A  + B + \bar{C})  \bullet (A +C + \bar{B}) \bullet (B + C + \bar{A})" width="303" height="21" />

**Minterm** : a group of variables **AND**ed where either the variable
or its negation is represented. Any logic function can be represented as a SUM of minterms.

#####Programmable Logic Arrays (PLAs)
 A programmable logic array (PLA) is a gate-level implementation
of the two-level representation for any set of logic functions,
which corresponds to a truth table with multiple output columns.

![PLA](http://www.cs.nyu.edu/courses/fall07/V22.0436-001/lectures/diagrams/pla3.png)

####Sequential Logic circuits:
Sequential logic circuits are circuits that can demonstrate a memory ability

They are:
- S-R latch
- D latch (Gated D-latch)

#####S-R latch

![S-R latch](http://i.stack.imgur.com/Zel68.png)

![S-R latch2](http://sub.allaboutcircuits.com/images/04177.png)

Points:
- Known as set-reset latches
- An **unclocked** memory element (not controlled by clock)
- S for setting the element(output)
- R for resetting the element(output)
- If both S and R are false, output will *"latch"* to previous state
- Built from cross coupled NOR or NAND gates (difference is on which bit means activated
, for NOR it is 1, for NAND it is 0)

Note: S and R bit can never be both 1, this is an invalid case and should never happen.

#####D-latch

D-latch with two inputs: D (data) and WE (write enable)
- When WE = 1, latch is set to value of D
    - R = NOT(D), S = D
- When WE = 0, latch holds previous value
    - R = S = 0

![D latch](http://sub.allaboutcircuits.com/images/04181.png)

![D-latch2](http://3.bp.blogspot.com/_ULAhHns4EIE/TOK10CmcLYI/AAAAAAAAAHI/9pKBQslDLEQ/s1600/gated%2BD%2Blatch%2Btiming%2Bdiagram.jpg)

As shown in the image above, the WE can be manipulated with the clock
thus resulting in the timing diagram supplied above.

Timing diagram is simply available to help visualize the behaviour of the circuit

##### Register
A register stores a multi-bit value.

It is simply a collection of D latches that are controlled by the same WE 

![Register](http://kkhsou.in/main/EVidya2/computer_science/comscience/447.gif)

For multiple registers, if there are many bits, e.g.: Q<sub>3</sub>, 
Q<sub>2</sub>, Q<sub>1</sub>, Q<sub>0</sub>. They can be written as
Q<sub>[3-0]</sub> to specify the register's bit range. **Rightmost** bit is always
**bit[0]**. And **leftmost** bit is **bit[n-1]** (for n-bit sized register).

#####Memory
Simply a logical k x  m array of stored bits. Each memory location is 
identified with an address. This location can store values. And the number of bits
per location is called addressability of the memory.

#####Clocks
A free running signal with a fixed cycle time(clock period). Or equivalently
a fixed clock frequence (inverse of cycle time).

Clocks are usually used as triggers. There are two methods of triggering depending on 
which edge of the clock output is used:
- Rising edge triggering: Clock value change from LOW to HIGH = trigger
- Falling edge triggering: Clock value change from HIGH to LOW = trigger

#####Master - slave D flip-flops
Is built by a pair of clock gated D flip-flops
- When clock is asserted, outputs can change
- Flip Flop : output can only change on the clock edge (rising or falling)

Example: Falling edge triggered master-slave d flip-flop

![falling edge trigg](https://upload.wikimedia.org/wikipedia/commons/thumb/5/52/Negative-edge_triggered_master_slave_D_flip-flop.svg/512px-Negative-edge_triggered_master_slave_D_flip-flop.svg.png)

![timing diagram](http://sub.allaboutcircuits.com/images/04187.png)

Important notes:
- Update only happens at **the edge**, which is when the clock value changes, anywhere else,
output value remains unchanged.