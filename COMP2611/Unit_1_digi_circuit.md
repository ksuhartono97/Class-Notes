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

####Programmable Logic Arrays (PLAs)
 A programmable logic array (PLA) is a gate-level implementation
of the two-level representation for any set of logic functions,
which corresponds to a truth table with multiple output columns.

![PLA](http://www.cs.nyu.edu/courses/fall07/V22.0436-001/lectures/diagrams/pla3.png)






