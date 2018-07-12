---
layout: post
title: Bit Tricks
---

Some usefull bit operations tricks

#### Clearing the rightmost set bit

`int x = x & (x - 1);`

This can be used to find number of set bits.

#### Extract the lowest set bit
`x & ~(x-1)` 

Pretty patterns when applied to a linear sequence.

#### Clearing run of set bits starting n

`x & (x + (1 << n))` 

#### Run of set bits starting n
`x & ~(x + (1 << n))`

#### Setting the lowest cleared bit
`x | (x + 1)` 

#### Run of cleared bit starting at bit 'n' 
`x | (x - (1 << n))`

### References
