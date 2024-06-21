### Challenge 1:

#### Challenge Files:

1. [source.enc](Writeup_files/source.enc)
2. [output.txt](Writeup_files/output.txt)

#### Writeup:

There is a long string in source file it looks like a base64 string.
Decode this string using `base64.b64decode()` function.

```python
#!/usr/bin/env python3
import base64
bytes_string = "d2l0aCBvcGVuKCdmbGFnLnR4dCcsICdyJykgYXMgZjoKICAgIGZsYWcgPSBmLnJlYWQoKQoKcyA9ICcnLmpvaW4oZm9ybWF0KG9yZChpKSwgJzAyeCcpIGZvciBpIGluIGZsYWcpCmUgPSAiIgoKZm9yIGkgaW4gcmFuZ2UoMCxsZW4ocyksNCk6CiAgICBlICs9IGZvcm1hdChpbnQoc1tpOmkrMl0sMTYpXmludChzW2k6aSs0XSwxNiksICcwMngnKQoKd2l0aCBvcGVuKCdvdXRwdXQudHh0JywgJ3cnKSBhcyBmOgogICAgZi53cml0ZShlKQ=="
final_string = base64.b64decode(bytes_string)

print (final_string)

```

```shell
┌──(rinshu㉿kali)-[~]
└─$ ./challenge1.py   
b'with open(\'flag.txt\', \'r\') as f:\n    flag = f.read()\n\ns = \'\'.join(format(ord(i), \'02x\') for i in flag)\ne = ""\n\nfor i in range(0,len(s),4):\n    e += format(int(s[i:i+2],16)^int(s[i:i+4],16), \'02x\')\n\nwith open(\'output.txt\', \'w\') as f:\n    f.write(e)'
```

It gives us this output.
If we arrange this statements we got to know that it is a python code.

```python

#!/usr/bin/env python3
with open('flag.txt', 'r') as f:
 flag = f.read()

s =''.join(format(ord(i),'02x') for i in flag)
e = ""

for i in range(0,len(s),4):
  e += format(int(s[i:i+2],16)^int(s[i:i+4],16), '02x')

with open('output.txt', 'w') as f:
 f.write(e)

```
It is a python code which gives us info about the flag that how it is encrypted and write the encrypted text in output.txt file.

We have to decrypt the text from output file to get the flag.

To decrpyting the text we have to reverse the process of encryption.

We have to reverse the XOR operation to retrieve the original bytes and then convert the resulting hexadecimal string back to characters to obtain the original flag.

```python

#!/usr/bin/env python3
o = "43104f0c32017b48340179266203350636025f6b6e0a5f2730423f42"
a =""
for i in range(0,len(o),4):
 a += format(int(o[i:i+2],16)^int(o[i:i+4],16),'02x')
flag = bytes.fromhex(a)
print (flag)

```

```shell
┌──(rinshu㉿kali)-[~]
└─$ ./reverse.py 
b'CSOC23{345y_ba5364_4nd_x0r?}'
```

Hence we get our flag as **`CSOC23{345y_ba5364_4nd_x0r?}`**

### Challenge 2:

### Challenge Files:
  
  [Encoded.txt](Writeup_files/encoded.txt)

### Writeup:

As we can see the there is a long string.

This string contains different formats which require different ways of encoding like binary,hexa,etc.

Split each format and decode one by one.

a = "01000011 01010011 01001111 01000011 00110010" --> This is written in binary.

b = "33 7b 6a 75 35 37 5f" --> This is a hexadecimal string.

c = "ZDFmZjNyM243XzNuYw==" --> This is a base64 text.

d = "60 144 61 156 66 65 137 154 60 154 175" --> This is octal representation,at first it looks like a binary but then it contains non printable characters so it concludes that it is a octal representation of ascii characters.

python script to decode all this one by one
```python
#!/usr/bin/env python3
import base64
a = "01000011 01010011 01001111 01000011 00110010"
b = "33 7b 6a 75 35 37 5f"
c = "ZDFmZjNyM243XzNuYw=="
d = "60 144 61 156 66 65 137 154 60 154 175"
binary_decode = ''.join(chr(int(a[i:i+8],2)) for i in range(0,len(a),9))

print (binary_decode)

hexa_decode = ''.join(chr(int(b[i:i+2],16)) for i in range (0,len(b),3))

print (hexa_decode)

base64_decode = base64.b64decode(c)

print (base64_decode)

octal_decode =''.join(chr(int(i,8)) for i in d.split())
print (octal_decode)
```

```shell
┌──(rinshu㉿kali)-[~]
└─$ ./challenge2.py
CSOC2
3{ju57_
b'd1ff3r3n7_3nc'
0d1n65_l0l}

```

The flag is **`CSOC23{ju57_d1ff3r3n7_3nc0d1n65_l0l}`**
