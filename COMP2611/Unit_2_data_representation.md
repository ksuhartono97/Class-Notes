#Data Representation

1101.11 = (1 x 2<sup>3</sup>) + ( 1 x 2<sup>2</sup> ) + ( 0 x 2<sup>1</sup>) + 
( 1 x 2<sup>0</sup>) + ( 1 x 2<sup>-1</sup> ) + ( 1 x 2<sup>-2</sup> )10= 13.75

1101 is the integer part

. signifies the binary point (the divider between the integer and floating part)

11 is the fraction part (the part after binary point)

The calculation part is how you convert from a base 2 number, which is binary
to base 10 number (decimal)

###Unsigned binary integers
Given k bits, representable range : [0, 2<sup>k</sup> -1]

Represented in powers of 2.

Examples:
1. 15 = 1111 = 2<sup>3</sup> + 2<sup>2</sup> + 2<sup>1</sup> + 2<sup>0</sup> 
2. 10 = 1010 = 2<sup>3</sup> + 2<sup>1</sup>

###Signed binary integers:
Possible method:

Signed magnitude : Using the most significant bit to represent the sign, however with this mode a bit is wasted as there are two
representations of zero. 0 means positive, 1 means negative

Example: 3 bit signed integer

|Bit | Result |
|----|----|
|000 | +0 |
|001 | +1 |
|010 | +2 |
|011 | +3 |
|100 | -0 |
|101 | -1 |
|110 | -2 |
|111 | -3 |

As we can see there are two representations of zero meaning that in signed magnitude, there is a wasted bit.

A more used method is **2's complement** which is used by all computer systems to represent
signed integers in the system.

The same as signed magnitude, it uses the most significant bit to signify the sign of number. The difference, the negative values are always added by 1 bit.

Steps to represent a negative value:
Let the number that we want to represent be 6,
1. Get binary form of + 6 = 0110
2. Invert it = 1001 = -7 = 1 - 8
3. Add 1 bit = 1010 = -6 = 2 - 8

The 1 bit in the front most basically means that if it exists, then the value of the 
binary number next to it gets subtracted by 2<sup>bits next to it</sup>

To conclude,
Given k bits, representable range [-2<sup>k</sup>, 2<sup>k</sup> -1]

>Word : the number of bits (in computer architecture)

