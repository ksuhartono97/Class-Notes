# Data Representation

1101.11 = (1 x 2<sup>3</sup>) + ( 1 x 2<sup>2</sup> ) + ( 0 x 2<sup>1</sup>) +
( 1 x 2<sup>0</sup>) + ( 1 x 2<sup>-1</sup> ) + ( 1 x 2<sup>-2</sup> )10= 13.75

1101 is the integer part

. signifies the binary point (the divider between the integer and floating part)

11 is the fraction part (the part after binary point)

The calculation part is how you convert from a base 2 number, which is binary
to base 10 number (decimal)

### Unsigned binary integers
Given k bits, representable range : [0, 2<sup>k</sup> -1]

Represented in powers of 2.

Examples:
1. 15 = 1111 = 2<sup>3</sup> + 2<sup>2</sup> + 2<sup>1</sup> + 2<sup>0</sup>
2. 10 = 1010 = 2<sup>3</sup> + 2<sup>1</sup>

### Signed binary integers:
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

Overflow: value is bigger than largest integer that can be represented
Underflow: value is smaller than smallest integer that can be represented

Zero extension: fills missing bits with 0

Sign extension: extending signed integer to more bits. (just put more 0 or 1)

### Floating Point Numbers
Scientific Notation: A single digit to the left of the decimal point

Normalized Scientific Notation: Scientific notation with no leading 0's

Binary numbers can be represented with scientific notation. All normalized
binary numbers always start with 1

1.xxxxxxxxxx

Such numbers are called floating point in computer arithmetic. (because the point
is not fixed)

Representation:

1.xxxxxxxxxxx * 2<sup>yyyyyyyyyyyy</sup>

x = significand
y = exponent

#### Single precision floating point
Uses 32 bits, 8 bits for exponent, 23 for significand, 1 for sign

Order:
(+/-) eeee eeee sss ssss ssss ssss ssss

Exponent bias : 127

#### Double precision floating point
Uses 64 bits, 11 bits for exponent, 52 bits for significand, 1 for sign

Order:
(+/-) eeee eeee eee ssss ssss ssss ssss ssss ....

Exponent bias : 1023

Standard representation of an IEEE floating-point format:

Let x be a number:

x = (-1)<sup>s</sup> * (1 + significand) * 2<sup>exponent - bias</sup

- S = sign bit = 0 for pos, 1 for neg
- Normalized significand : 1.0 < significand < 2.0
- The 1 in (1 + significand) is an implicit 1. The represented significand there is all the numbers
after the binary point
- Exponent: when converting from decimal to binary, the exponent will always be added with the bias,
thus when converting back we need to subtract it back.

Example:
Give the IEEE754 representation of -0.75 in single precision
1. Convert to binary: -0.75 = -0.11 x 2<sup>0</sup>
2. Normalize it = -1.1 x 2<sup>-1</sup>
3. Sign = 1, exponent = -1
4. Significand = 1000000...(23 bits)
5. Biased exponent = -1 + 127 = 126 = 0111 1110
6. Represent: 1 0111 1110 100 0000 0000 0000 0000

For double precision, the steps differ starting from 4:
4. Significand = 10000... (52 bits)
5. Biased exponent = -1 + 1023 = 011 1111 1110
6. Represent: 1 011 1111 1110 1000 0000 ....000

Why use implicit 1 and biased exponent? :
- Implicit 1 allows adding more bits to the significand, thus resulting in higher precision in representing the numbers (as the floating
point representation ina  computer is merely an approximation)
- Biased exponent: For faster comparisons, such that the computer will immediately compare the value, as if we add
the bias, all the values will always be positive, however without bias, the values will be positive and negative,
meaning that the computer will have to convert it to compare the value

Reserved Exponents:
- 0000 0000
- 1111 1111

|Exponent | Significand| Usage|
|---------|------------|------|
|111...111| 000...00| +/- infinity|
|111...111| != 000....00| NaN |
|000...000| 000...00 | +- 0.0|
|000...000| != 000.000 | Hidden bit is not 0 (implicit 1 does not exist) |

Overflow: positive exponent too large to fit in the exponent field
Underflow: negative exponent is too large to fit in the exponent field

Normalized exponent range (+ bias) : 0000 0001 ~ 1111 1110

### Characters

Represented using 8 bits per character, follows the ASCII standard

![ASCII](http://www.asciitable.com/index/asciifull.gif)

Writing down ASCII in hexadecimal values:

0x : represents a positive hexadecimal value, if it is a letter, then 2 hex characters represent 1 ASCII letter

Example: 0x32363131

Possible representations:
- 2's complement integer
- Unsigned number : same as above
- **ASCII encoded bytes**:
    - 0x32 : 2
    - 0x36 : 6
    - 0x31 : 1
    - 0x31 : 1
- 32 bit IEEE floating point number   
