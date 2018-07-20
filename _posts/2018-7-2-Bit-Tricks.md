---
layout: post
title: Bit Tricks
---

Some usefull bit operations tricks

#### Clearing the rightmost set bit

`int x = x & (x - 1);`

This can be used to find number of set bits. Also if a number is power of 2, as it will be zero after this operation.

#### Extract the lowest set bit
`x & ~(x-1)`

For signed numbers you can use the following method also
`x & -x` 

Pretty patterns when applied to a linear sequence.

#### Clearing run of set bits starting n

`x & (x + (1 << n))` 

#### Run of set bits starting n
`x & ~(x + (1 << n))`

#### Setting the lowest cleared bit
`x | (x + 1)` 

#### Run of cleared bit starting at bit 'n' 
`x | (x - (1 << n))`

#### Count the trailing number of zeros
One can run a loop over the integer and find this but following is interesting way using bit operations. One can think of this as a binary search over the bits.

```C
int c = 32;
x &= -x;
if(x) c -= 1;
if (x & 0x0000FFFF) c -= 16;
if (x & 0x00FF00FF) c -= 8;
if (x & 0x00F0F0F0F) c -= 4;
if (x & 0x33333333) c -= 2;
if (x & 0x55555555) c -= 1;
```

### References
