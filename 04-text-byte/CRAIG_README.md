# Chapter 04

## Integer Representations
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

## Normalising Unicode
In the following code:
```
def shave_marks(txt):
    """Remove all diacritic marks"""
    norm_txt = unicodedata.normalize('NFD', txt)  # <1>
    shaved = ''.join(c for c in norm_txt
                     if not unicodedata.combining(c))  # <2>
    return unicodedata.normalize('NFC', shaved)  # <3>
```
I was confused about the return as I couldn't see there was anything to combine back, which is to say that I think `shaved == unicodedata.normalize('NFC', shaved)` which was certainly the case for the given doctests.  
I think that perhaps the normalize using "NFC" was simply done as a "good practice" as he mentions on pdf page 252:
*However, to be safe, it may be good to normalize strings with normalize('NFC' user_text) before saving*  
That said, if you look at the *ohm example* on page 252 you can see that `normalize("NFC", ohm)` does actually change the character from `OHM SIGN` to `GREEK CAPITAL LETTER OMEGA` and so it's not all about combining diacritics.

I was also a bit confused by the following example:
```
def shave_marks_latin(txt):
    """Remove all diacritic marks from Latin base characters"""
    norm_txt = unicodedata.normalize('NFD', txt)  # <1>
    latin_base = False
    preserve = []
    for c in norm_txt:
        if unicodedata.combining(c) and latin_base:   # <2>
            continue  # ignore diacritic on Latin base char
        preserve.append(c)                            # <3>
        # if it isn't a combining char, it's a new base char
        if not unicodedata.combining(c):              # <4>
            latin_base = c in string.ascii_letters
    shaved = ''.join(preserve)
    return unicodedata.normalize('NFC', shaved)   # <5>
```
as at first look it looks odd that `latin_base` is tested before it is evaluated. However debugging made me see that when you hit a *combining* character, you want to know if the *preceeding non-combining* character was latin or not. So the code is good.