# cs2400-arm-3
CS2400 ARM assembly programming assignment #3

## Instructions
This assignment deals with floating-point numbers. The instructions are in the files themselves.

## Support materials
You might find the following materials useful:
1. [IEEE 754 single-precision floating-point format](https://en.wikipedia.org/wiki/Single-precision_floating-point_format).
2. [IEEE 754 single-precision converter](https://www.h-schmidt.net/FloatConverter/IEEE754.html).
3. [Excess (aka offset) signed integer representation](https://en.wikipedia.org/wiki/Signed_number_representations#Offset_binary).
4. [Low-level floating-point marshalling between different instruction-level architectures](http://ecet.ecs.uni-ruse.bg/cst06/Docs/cp/SII/II.4.pdf).

## Tandem Non-stop Series (TNS) Format
The Tandem Non-Stop Series (TNS) are very reliable supercomputers widely used as servers in banks, financial institutions, the military, etc. 
The TNS word (2 bytes) is placed in memory at a two-byte memory boundary. Any two consecutive TNS words, aligned on a four-byte boundary, constitute a TNS doubleword.
```
|----------------|----------------| 
|                |                |
|----------------|----------------| 
 0             15 16            31
```
A single-precision floating-point number is represented by a TNS doubleword. (Note that this is a word in VisUAL.)
```
|-|----------------------|---------| 
| | significand (22 bits)| exponent|
|-|----------------------|---------|
 0 1                   23 24     31
```
The single precision floating-point number consists of a one-bit sign, a 22-bit significand (fraction) and a 9-bit exponent. The TNS number format predates and is different from the IEEE 754 standard. 
The fraction of a TNS-format floating-point number is always normalized, i.e. greater than 1 and less than 2. For example, `1.1001`. The high order integer bit (the whole part) is dropped and assumed to be 1 (hidden integer part 1.xx). This is the same as in IEEE 754. During calculations, the sign is temporarily removed and the assumed integer bit reinserted. The integer plus the 22 fraction bits are equivalent to 6.9 decimal digits; the 55 bits of an extended number (double precision) are equivalent to 16.5 decimal digits. If the value of the number to be represented is zero, the sign is zero, the fraction is 0, and the exponent is zero.
The exponent part of the number, bits 24 through 31 of the doubleword indicates the power of 2 multiplied by 1 plus the fraction. This field can contain values 0 through 511. To express numbers of both large and small absolute magnitude, the exponent is expressed as an excess-256 value; that is, 256 is added to the actual exponent of the number before it is stored. The exponent range is therefore -256 through +255.
The sign is explicitly given in the high-order bit; a 0 is positive, and a 1 is negative. Unlike integers, which use two’s compliment, negating a floating-point number affects the only high-order bit and not the fraction or exponent fields. This is a typical sigh-magnitude code. 
The absolute-value range of 32-bit floating-point numbers, in base-2 and base-10 (approximately) is
```
 +  -256                 +       -23     256 
 - 2              ----   - (1 - 2   ) * 2    
 
 +          -78         +          77
 - 8.64 * 10      ----  - 1.15 * 10  
```

## Submission
1. Fork this repository.
2. Clone to your development environment.
3. Open files in VisUAL from the local repository.
4. Commit your changes when you are done.
5. Push your commits to the remote.
6. Submit on [Google Classroom](https://classroom.google.com/u/0/c/Mjc5MjgxMTQ2NzZa/a/MzUwNTU4MjM5ODFa/details) and enter the URL of your remote in a comment.


