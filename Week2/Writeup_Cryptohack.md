# CSOC Week 2 Crytography

## Cryptohack Challenges

### INTRODUCTION 

### Finding flags

##### Challenge Description:

Each challenge is designed to help introduce you to a new piece of cryptography. Solving a challenge will require you to find a "flag".

These flags will usually be in the format crypto{y0ur_f1rst_fl4g}. The flag format helps you verify that you found the correct solution.

Try submitting this flag into the form below to solve your first challenge.

##### Writeup:

The flag is given in the challenge itself.

The flag is **`crypto{y0ur_f1rst_fl4g}`**

---

### Great Snakes

##### Challenge Description:

Modern cryptography involves code, and code involves coding. CryptoHack provides a good opportunity to sharpen your skills.

Of all modern programming languages, Python 3 stands out as ideal for quickly writing cryptographic scripts and attacks. For more information about why we think Python is so great for this, please see the FAQ.

Run the attached Python script and it will output your flag.

Challenge files:
  - [great_snakes.py](https://github.com/Divyanshukumar20/CSOC24/blob/main/Week2/Writeup_files/great_snakes_35381fca29d68d8f3f25c9fa0a9026fb.py)

##### Writeup:

The file is a python code.Simply,we have to run this program to get our flag.

To run this on terminal first we have to give it a permission to run.

```shell
┌──(rinshu㉿kali)-[~/Downloads]
└─$ chmod +x great_snakes_35381fca29d68d8f3f25c9fa0a9026fb.py        
     
┌──(rinshu㉿kali)-[~/Downloads]
└─$ ./great_snakes_35381fca29d68d8f3f25c9fa0a9026fb.py 
Here is your flag:
crypto{z3n_0f_pyth0n}

```
Here we get our flag as **`crypto{z3n_0f_pyth0n}`**

---

### Network Attacks

##### Challenge Description:

Several of the challenges are dynamic and require you to talk to our challenge servers over the network. This allows you to perform man-in-the-middle attacks on people trying to communicate, or directly attack a vulnerable service. To keep things consistent, our interactive servers always send and receive JSON objects.

Such network communication can be made easy in Python with the pwntools module. This is not part of the Python standard library, so needs to be installed with pip using the command line pip install pwntools.

For this challenge, connect to socket.cryptohack.org on port 11112. Send a JSON object with the key buy and value flag.

The example script below contains the beginnings of a solution for you to modify, and you can reuse it for later challenges.

Connect at `socket.cryptohack.org 11112`

Challenge files:
  - [pwntools_example.py](https://github.com/Divyanshukumar20/CSOC24/blob/main/Week2/Writeup_files/pwntools_example_72a60ff13df200692898bb14a316ee0b.py)

##### Writeup:

The challenge says we have to communicate with the challenge server using python code with the help of pwntools to get the flag.

The challenge file contain the example python code to communicate.
But we have to modify this code.

As challenge said the we have to send a JSON object with the key *buy* and value *flag*.

But in the file the vlaue of the key is *clothes*. Change it to *flag*.

Modified python code
```python
#!/usr/bin/env python3

from pwn import * # pip install pwntools
import json

HOST = "socket.cryptohack.org"
PORT = 11112

r = remote(HOST, PORT)


def json_recv():
    line = r.readline()
    return json.loads(line.decode())

def json_send(hsh):
    request = json.dumps(hsh).encode()
    r.sendline(request)


print(r.readline())
print(r.readline())
print(r.readline())
print(r.readline())

request = {
    "buy": "flag"
}
json_send(request)

response = json_recv()

print(response)
```
```shell
┌──(rinshu㉿kali)-[~/Downloads]
└─$ ./pwntools_example_72a60ff13df200692898bb14a316ee0b.py   
[+] Opening connection to socket.cryptohack.org on port 11112: Done
b"Welcome to netcat's flag shop!\n"
b'What would you like to buy?\n'
b"I only speak JSON, I hope that's ok.\n"
b'\n'
{'flag': 'crypto{sh0pp1ng_f0r_fl4g5}'}
[*] Closed connection to socket.cryptohack.org port 11112

```
After running this code we get our flag as **`crypto{sh0pp1ng_f0r_fl4g5}`**

---

### ENCODING

### ASCII

##### Challenge Description:

ASCII is a 7-bit encoding standard which allows the representation of text using the integers 0-127.

Using the below integer array, convert the numbers to their corresponding ASCII characters to obtain a flag.

[99, 114, 121, 112, 116, 111, 123, 65, 83, 67, 73, 73, 95, 112, 114, 49, 110, 116, 52, 98, 108, 51, 125]

##### Writeup:

To get the flag we have to write a script in python that change all this numbers to their corresponding ASCII characters.

We use chr() function to do this.

This is a script
```python
!/usr/bin/env python3
op = [99, 114, 121, 112, 116, 111, 123, 65, 83, 67, 73, 73, 95, 112, 114, 49, 110, 116, 52, 98, 108, 51, 125]
for i in op:
 print (chr(i),end="")
```
```shell
──(rinshu㉿kali)-[~]
└─$ ./chr_function.py   
crypto{ASCII_pr1nt4bl3}  
```
We get our flag as **`crypto{ASCII_pr1nt4bl3} `** 

---

### Hex

##### Challenge Desccription:

When we encrypt something the resulting ciphertext commonly has bytes which are not printable ASCII characters. If we want to share our encrypted data, it's common to encode it into something more user-friendly and portable across different systems.

Hexadecimal can be used in such a way to represent ASCII strings. First each letter is converted to an ordinal number according to the ASCII table (as in the previous challenge). Then the decimal numbers are converted to base-16 numbers, otherwise known as hexadecimal. The numbers can be combined together, into one long hex string.

Included below is a flag encoded as a hex string. Decode this back into bytes to get the flag.

63727970746f7b596f755f77696c6c5f62655f776f726b696e675f776974685f6865785f737472696e67735f615f6c6f747d

##### Writeup:

We have given a hex string.To decode this into bytes we use python script.

`bytes.fromhex` is a function in python which convert hex to bytes.

Python script
```python
#!/usr/bin/env python3
given_string = "63727970746f7b596f755f77696c6c5f62655f776f726b696e675f776974685f6865785f737472696e67735f615f6c6f747d"
required_string = bytes.fromhex(given_string)
print (required_string)
```
Run this script in shell.
```shell
┌──(rinshu㉿kali)-[~]
└─$ ./hex_to_bytes.py   
b'crypto{You_will_be_working_with_hex_strings_a_lot}'
```

We get the flag as **`crypto{You_will_be_working_with_hex_strings_a_lot}`**

---

### Base64

##### Challenge Description:

Another common encoding scheme is Base64, which allows us to represent binary data as an ASCII string using an alphabet of 64 characters. One character of a Base64 string encodes 6 binary digits (bits), and so 4 characters of Base64 encode three 8-bit bytes.

Base64 is most commonly used online, so binary data such as images can be easily included into HTML or CSS files.

Take the below hex string, decode it into bytes and then encode it into Base64.

72bca9b68fc16ac7beeb8f849dca1d8a783e8acf9679bf9269f7bf

##### Writeup:

In this challenge first we have to decode this hex string as we done previously and then we encode those bytes into base 64 to get our flag.

We use `base64.b64encode()` function from base64 library of a python to encode the strings into base64.

Python script
```python
#!/usr/bin/env python3
import base64

hex_string = "72bca9b68fc16ac7beeb8f849dca1d8a783e8acf9679bf9269f7bf"

bytes_string = bytes.fromhex(hex_string)
final_string = base64.b64encode(bytes_string)

print (final_string)

```
```shell
┌──(rinshu㉿kali)-[~]
└─$ ./hex_to_string_to_base64.py 
b'crypto/Base+64+Encoding+is+Web+Safe/'
```
We get our flag as **`crypto/Base+64+Encoding+is+Web+Safe/`**

---

### Bytes and Big Integers

##### Challenge Description:

Cryptosystems like RSA works on numbers, but messages are made up of characters. How should we convert our messages into numbers so that mathematical operations can be applied?

The most common way is to take the ordinal bytes of the message, convert them into hexadecimal, and concatenate. This can be interpreted as a base-16/hexadecimal number, and also represented in base-10/decimal.

Convert the following integer back into a message:

11515195063862318899931685488813747395775516287289682636499965282714637259206269

##### Writeup:

In this challenge we have to convert the long integer to bytes.

To do this in python we have `long_to_bytes()` function in Crypto.Util.number.

We import it from there.

Python Script
```python
#!/usr/bin/env python3
from Crypto.Util.number import long_to_bytes

long_integer = 11515195063862318899931685488813747395775516287289682636499965282714637259206269

string = long_to_bytes(long_integer)

print (string)

```
```shell
┌──(rinshu㉿kali)-[~]
└─$ ./long_to_bytes.py          
b'crypto{3nc0d1n6_4ll_7h3_w4y_d0wn}'
```

We get our flag as **`crypto{3nc0d1n6_4ll_7h3_w4y_d0wn}`**

---

### XOR

### XOR Starter

##### Challenge Description:
XOR is a bitwise operator which returns 0 if the bits are the same, and 1 otherwise. In textbooks the XOR operator is denoted by ⊕, but in most challenges and programming languages you will see the caret ^ used instead.

A	B	Output
0	0	0
0	1	1
1	0	1
1	1	0
For longer binary numbers we XOR bit by bit: 0110 ^ 1010 = 1100. We can XOR integers by first converting the integer from decimal to binary. We can XOR strings by first converting each character to the integer representing the Unicode character.

Given the string label, XOR each character with the integer 13. Convert these integers back to a string and submit the flag as crypto{new_string}.

##### Writeup:

In this challenge we have to XOR'd a string with a integer values.To do this in python,first we convert each character of the string *label* to their ASCII values and XOR'd each ASCII values with the integer 13 one by one.

After XOR'ing we get integers which when again change it to their corresponding ASCII characters gives us a flag.

Python Script
```python
#!/usr/bin/env python3
string = "label"
unicode_values = [ord(i) for i in string]

xor = [unicode_values[i] ^ 13 for i in range(0,5)]

for i in range(0,5):
  print (chr(xor[i]),end="")

```
```shell
┌──(rinshu㉿kali)-[~]
└─$ ./xor_finder.py   
aloha
```
So we the strings as `aloha`.
Hence our flag is **`crypto{aloha}`**

---

### XOR Properties

##### Challenge Description:

In the last challenge, you saw how XOR worked at the level of bits. In this one, we're going to cover the properties of the XOR operation and then use them to undo a chain of operations that have encrypted a flag. Gaining an intuition for how this works will help greatly when you come to attacking real cryptosystems later, especially in the block ciphers category.

There are four main properties we should consider when we solve challenges using the XOR operator

Commutative: A ⊕ B = B ⊕ A
Associative: A ⊕ (B ⊕ C) = (A ⊕ B) ⊕ C
Identity: A ⊕ 0 = A
Self-Inverse: A ⊕ A = 0

Let's break this down. Commutative means that the order of the XOR operations is not important. Associative means that a chain of operations can be carried out without order (we do not need to worry about brackets). The identity is 0, so XOR with 0 "does nothing", and lastly something XOR'd with itself returns zero.

Let's put this into practice! Below is a series of outputs where three random keys have been XOR'd together and with the flag. Use the above properties to undo the encryption in the final line to obtain the flag.

KEY1 = a6c8b6733c9b22de7bc0253266a3867df55acde8635e19c73313
KEY2 ^ KEY1 = 37dcb292030faa90d07eec17e3b1c6d8daf94c35d4c9191a5e1e
KEY2 ^ KEY3 = c1545756687e7573db23aa1c3452a098b71a7fbf0fddddde5fc1
FLAG ^ KEY1 ^ KEY3 ^ KEY2 = 04ee9855208a2cd59091d04767ae47963170d1660df7f56f5faf

##### Writeup:

So we have given some hex strings and using XOR properties we have to find the flag.

To do this with a python script,first we change hex strings to bytes,then we XOR'd these bytes to get the key2,key3 and finally flag.

Python Script
```python
#!/usr/bin/env python3

key_1 = bytes.fromhex('a6c8b6733c9b22de7bc0253266a3867df55acde8635e19c73313')

xor1 = "37dcb292030faa90d07eec17e3b1c6d8daf94c35d4c9191a5e1e"

xor_1 = bytes.fromhex(xor1)

key2 = bytes([b1 ^ b2 for b1,b2 in zip(key_1,xor_1)])

xor2 = "c1545756687e7573db23aa1c3452a098b71a7fbf0fddddde5fc1"
xor_2 = bytes.fromhex(xor2)

key3 = bytes([b1 ^ b2 for b1,b2 in zip(key2,xor_2)])

xor3 = "04ee9855208a2cd59091d04767ae47963170d1660df7f56f5faf"
xor_3 = bytes.fromhex(xor3)

flag = bytes([b1^b2^b3^b4 for b1,b2,b3,b4 in zip(key_1,key2,key3,xor_3)])

print (flag)

```
```shell
┌──(rinshu㉿kali)-[~]
└─$ ./tough.py     
b'crypto{x0r_i5_ass0c1at1v3}'
```
We get our flag as **`crypto{x0r_i5_ass0c1at1v3}`**

---

### Favourite byte

##### Challenge Description:

For the next few challenges, you'll use what you've just learned to solve some more XOR puzzles.

I've hidden some data using XOR with a single byte, but that byte is a secret. Don't forget to decode from hex first.

73626960647f6b206821204f21254f7d694f7624662065622127234f726927756d

##### Writeup:
As challenge said there is a secret key i.e. single byte with which this string xor'd to create the flag.

First we change this hex string to bytes.

To retrieve the flag we have to find the key and xor'd with the string given.

Now as challenge said the key contains only one byte.If we think about this we got to know that if this single byte is xor'd with the first byte of string then it must give the ASCII of "c" as the name of flag starts with crypto{..

So we get the key by xor'ing the first character of given string and ASCII of "c".

We use pwntools for xor'ings.

Now we use this key to get the flag by xor'ing it with string

Python script
```python
#!/usr/bin/env python3
from pwn import xor
text = bytes.fromhex("73626960647f6b206821204f21254f7d694f7624662065622127234f726927756d")

key = xor(text[0],ord("c"))
output = xor(text,key)
print (output)
```
```shell
┌──(rinshu㉿kali)-[~]
└─$ ./more_xor.py                               
b'crypto{0x10_15_my_f4v0ur173_by7e}'
```
We get our flag as **`crypto{0x10_15_my_f4v0ur173_by7e}`**

---

### You either know, XOR you don't

##### Challenge Description:
I've encrypted the flag with my secret key, you'll never be able to guess it.

0e0b213f26041e480b26217f27342e175d0e070a3c5b103e2526217f27342e175d0e077e263451150104

##### Writeup:

As done in previous challenge,here also we have to find the key but here the key is not a single byte.

But using the format of flag we can identify the key.

The first few known characters of the flag is *crypto{* .So we xor'd this characters with the first 8 characters of the string.
```python
#!/usr/bin/env python3
from pwn import xor

text = bytes.fromhex("0e0b213f26041e480b26217f27342e175d0e070a3c5b103e2526217f27342e175d0e077e263451150104")

key = xor (text[:7],b'crypto{') 
print (key)

```
```shell
┌──(rinshu㉿kali)-[~]
└─$ ./easy_one.py   
b'myXORke'
```
It gives us the output *myXORke* .If we guess the next character it must be *y* Let's check it.
```python
#!/usr/bin/env python3
from pwn import xor

text = bytes.fromhex("0e0b213f26041e480b26217f27342e175d0e070a3c5b103e2526217f27342e175d0e077e263451150104")

key = xor (text[:7],b'crypto{') + b'y'

output = xor(text,key)

print (output)
```
```shell
┌──(rinshu㉿kali)-[~]
└─$ ./easy_one.py   
b'crypto{1f_y0u_Kn0w_En0uGH_y0u_Kn0w_1t_4ll}'

```
Yes, We are correct Here we get our flag as **`crypto{1f_y0u_Kn0w_En0uGH_y0u_Kn0w_1t_4ll}`**
