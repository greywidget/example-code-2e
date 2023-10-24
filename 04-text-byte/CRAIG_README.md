# Chapter 04

I was confused by the following example, mainly because I wasn't sure of the integer representations:

```
>>> import array
>>> numbers = array.array('h', [-2, -1, 0, 1, 2])
>>> octets = bytes(numbers)
>>> octets
b'\xfe\xff\xff\xff\x00\x00\x01\x00\x02\x00'
```

Type 'h' in an array is 16 bit integers so you end up with:
```
-2 = 0xFFFE = 11111111 11111110
-1 = 0xFFFF = 11111111 11111111
 0 = 0x0000 = 00000000 00000000
 1 = 0x0001 = 00000000 00000001
 2 = 0x0002 = 00000000 00000010
```
I found the following site [signed short](https://www.binaryconvert.com/convert_signed_short.html?decimal=050) useful for seeing the integer representations.

