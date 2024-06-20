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

---

 ### MATHEMATICS

 ### Greatest Common Divisor

 ##### Challenge Description:

 34 Solves · 90 Solutions
The Greatest Common Divisor (GCD), sometimes known as the highest common factor, is the largest number which divides two positive integers (a,b).

For a = 12, b = 8 we can calculate the divisors of a: {1,2,3,4,6,12} and the divisors of b: {1,2,4,8}. Comparing these two, we see that gcd(a,b) = 4.

Now imagine we take a = 11, b = 17. Both a and b are prime numbers. As a prime number has only itself and 1 as divisors, gcd(a,b) = 1.

We say that for any two integers a,b, if gcd(a,b) = 1 then a and b are coprime integers.

If a and b are prime, they are also coprime. If a is prime and b < a then a and b are coprime.

There are many tools to calculate the GCD of two integers, but for this task we recommend looking up Euclid's Algorithm.

Try coding it up; it's only a couple of lines. Use a = 12, b = 8 to test it.

Now calculate gcd(a,b) for a = 66528, b = 52920 and enter it below.

##### Writeup:

This challenge tells us to write a python script to calculate gcd using Euclid's Algorithm.

In Euclid's Algorithm we find greatest common divisor of two numbers.

In this algorithm we first divide the greatest number with smallest one and get the remainder.After that we divide the smaller number by remainder and get the new remainder.Continuing this process until we got remainder 0.
When we got our remainder 0 the number which we divide recently is the our gcd.

Here is the python script for this.

```python
#!/usr/bin/env python3
def gcd(a,b):
 while b != 0:
  a,b = b,a%b
 return a

a =66528
b =52920

print (gcd(a,b))
```
```shell
┌──(rinshu㉿kali)-[~]
└─$ ./euclidean_algorithm.py   
1512
```
Answer:- ***1512***

---

### Extended GCD

##### Challenge Description:

Let a and b be positive integers.

The extended Euclidean algorithm is an efficient way to find integers u,v such that

a * u + b * v = gcd(a,b)

Using the two primes p = 26513, q = 32321, find the integers u,v such that

p * u + q * v = gcd(p,q)

Enter whichever of u and v is the lower number as the flag.

##### Writeup:

Now this challenge suggests us about extended Euclidean algorithm
computes the greatest common divisor (GCD) of two integers 
The Extended Euclidean Algorithm is an extension of the Euclidean Algorithm that not only computes the greatest common divisor (GCD) of two integers a and b but also finds the coefficients x and y such that:
  ax+by=gcd(a,b)

This is the python script to find the coefficient x and y
```python
#!/usr/bin/env python3
def extended(a, b):
 x0,x1,y0,y1 = 1,0,0,1

 while b != 0:
  q , a , b = a//b , b , a%b
  x0 , x1 = x1 , x0 - q*x1
  y0 , y1 = y1 , y0 - q*y1
 return x0,y0
a = 32321
b = 26513
x, y = extended(a, b)
print (x,y)
```
```shell
┌──(rinshu㉿kali)-[~]
└─$ ./extended_euclidean_theorem   
-8404 10245
```
Smallest one is the answer
Answer:- ***-8404***

---

### Modular Arithmetic 1

##### Challenge Description:

Imagine you lean over and look at a cryptographer's notebook. You see some notes in the margin:

4 + 9 = 1
5 - 7 = 10
2 + 3 = 5

At first you might think they've gone mad. Maybe this is why there are so many data leaks nowadays you'd think, but this is nothing more than modular arithmetic modulo 12 (albeit with some sloppy notation).

You may not have been calling it modular arithmetic, but you've been doing these kinds of calculations since you learnt to tell the time (look again at those equations and think about adding hours).

Formally, "calculating time" is described by the theory of congruences. We say that two integers are congruent modulo m if a ≡ b mod m.

Another way of saying this, is that when we divide the integer a by m, the remainder is b. This tells you that if m divides a (this can be written as m | a) then a ≡ 0 mod m.

Calculate the following integers:

11 ≡ x mod 6
8146798528947 ≡ y mod 17

The solution is the smaller of the two integers.

##### Writeup:

As mentioned in the challenge a ≡ b mod m means when a is divided by m we get the remainder b.

To do this..
```python
#!/usr/bin/env python3
x = 11%6
y = 8146798528947%17
print (x,y)

```

```shell
┌──(rinshu㉿kali)-[~]
└─$ ./mod.py                    
5 4
```
Smallest number is our answer.

Answer :- ***4***

---

### Modular Arithmetic 2

##### Challenge Description:

We'll pick up from the last challenge and imagine we've picked a modulus p, and we will restrict ourselves to the case when p is prime.

The integers modulo p define a field, denoted F<sub>p</sub>.

A finite field Fp is the set of integers {0,1,...,p-1}, and under both addition and multiplication there is an inverse element b for every element a in the set, such that a + b = 0 and a * b = 1.

Lets say we pick p = 17. Calculate 3<sup>17</sup> mod 17. Now do the same but with 5<sup>17</sup> mod 17.

What would you expect to get for 7<sup>16</sup> mod 17? Try calculating that.

This interesting fact is known as Fermat's little theorem. We'll be needing this (and its generalisations) when we look at RSA cryptography.

Now take the prime p = 65537. Calculate 273246787654<sup>65536</sup> mod 65537.

Did you need a calculator?

##### Writeup:

This challenge suggests about Fermat's little theorem 
It states that if p is a prime number and a is any integer such that a is not divisible by p, then:

a<sup>p-1</sup> ≡ 1 (mod p)

It means that a<sup>p-1</sup> is divided by p then the remainder is 1 if p is a prime and a is not divisbble by p.

According to this theorem the answer to this question must be 1.

Answer:- ***1***

### Modular Inverting

##### Challenge Description:

As we've seen, we can work within a finite field F<sub>p</sub>, adding and multiplying elements, and always obtain another element of the field.

For all elements g in the field, there exists a unique integer d such that g * d ≡ 1 mod p.

This is the multiplicative inverse of g.

Example: 7 * 8 = 56 ≡ 1 mod 11

What is the inverse element: 3 * d ≡ 1 mod 13?

##### Writeup:

Now again challenge suggests us to  use the Fermat's little theorem to find the modular inverse.

We know that a<sup>p-1</sup> ≡ 1 (mod p)

Dividing both side by a : a<sup>p-2</sup> ≡ a<sup>-1</sup> (mod p)

Hence the modular inverse of a is : a<sup>-1</sup> = a<sup>p-2</sup> (mod p)

Here d = 3<sup>11</sup> (mod 13)

d = 9

Answer:- ***9***

### SYMMETRIC CIPHERS

### Keyed Permutations

##### Challenge Description:

AES, like all good block ciphers, performs a "keyed permutation". This means that it maps every possible input block to a unique output block, with a key determining which permutation to perform.

Using the same key, the permutation can be performed in reverse, mapping the output block back to the original input block. It is important that there is a one-to-one correspondence between input and output blocks, otherwise we wouldn't be able to rely on the ciphertext to decrypt back to the same plaintext we started with.

What is the mathematical term for a one-to-one correspondence?

##### Writeup:

Generally one-to-one correspondance in terms of mathematics is **bijection**

Answer: crypto{bijection}

---

### Resisting Bruteforce

##### Challenge Description:

If a block cipher is secure, there should be no way for an attacker to distinguish the output of AES from a random permutation of bits. Furthermore, there should be no better way to undo the permutation than simply bruteforcing every possible key. That's why academics consider a cipher theoretically "broken" if they can find an attack that takes fewer steps to perform than bruteforcing the key, even if that attack is practically infeasible.

It turns out that there is [an attack](https://en.wikipedia.org/wiki/Biclique_attack) on AES that's better than bruteforce, but only slightly – it lowers the security level of AES-128 down to 126.1 bits, and hasn't been improved on for over 8 years. Given the large "security margin" provided by 128 bits, and the lack of improvements despite extensive study, it's not considered a credible risk to the security of AES. But yes, in a very narrow sense, it "breaks" AES.

Finally, while quantum computers have the potential to completely break popular public-key cryptosystems like RSA via Shor's algorithm, they are thought to only cut in half the security level of symmetric cryptosystems via Grover's algorithm. This is one reason why people recommend using AES-256, despite it being less performant, as it would still provide a very adequate 128 bits of security in a quantum future.

What is the name for the best single-key attack against AES?

##### Writeup:

If we get the link given in the challenge we got to know your answer.

Answer: ***crypto{Biclique}***

---

### Structure of AES

##### Challenge Description:

To achieve a keyed permutation that is infeasible to invert without the key, AES applies a large number of ad-hoc mixing operations on the input. This is in stark contrast to public-key cryptosystems like RSA, which are based on elegant individual mathematical problems. AES is much less elegant, but it's very fast.

At a high level, AES-128 begins with a "key schedule" and then runs 10 rounds over a state. The starting state is just the plaintext block that we want to encrypt, represented as a 4x4 matrix of bytes. Over the course of the 10 rounds, the state is repeatedly modified by a number of invertible transformations.

Included is a bytes2matrix function for converting our initial plaintext block into a state matrix. Write a matrix2bytes function to turn that matrix back into bytes, and submit the resulting plaintext as the flag.

Challenge files:
  - [matrix.py](https://github.com/Divyanshukumar20/CSOC24/blob/main/Week2/Writeup_files/matrix_e1b463dddbee6d17959618cf370ff1a5.py)

##### Writeup:

As seen in the file we got a python script which is not completed.We havre to complete it.
bytes2matrix is given we have to find the matrix2 bytes function.

It's simple we just have change each value of integere in matrix to get the ASCII character and just add them.
We get our flag.

Complete python script

```python
#!/usr/bin/env python3
#def bytes2matrix(text):
#    """ Converts a 16-byte array into a 4x4 matrix.  """
#    return [list(text[i:i+4]) for i in range(0, len(text), 4)]

def matrix2bytes(matrix):
    text = ""
    """ Converts a 4x4 matrix into a 16-byte array.  """
    for i in range(0,4):
     for j in range(0,4):
       text += chr(matrix[i][j])
    return (text)
matrix = [
    [99, 114, 121, 112],
    [116, 111, 123, 105],
    [110, 109, 97, 116],
    [114, 105, 120, 125],
]

print (matrix2bytes(matrix))
                             
```
```shell
┌──(rinshu㉿kali)-[~]
└─$ ./matrix_e1b463dddbee6d17959618cf370ff1a5.py
crypto{inmatrix}
```
We get the flag as **`crypto{inmatrix}`**

---

### RSA

### RSA Starter 1

##### Challenge Description:

All operations in RSA involve modular exponentiation.

Modular exponentiation is an operation that is used extensively in cryptography and is normally written like: 2<sup>10</sup> mod 17

You can think of this as raising some number to a certain power (2<sup>10</sup> = 1024), and then taking the remainder of the division by some other number (1024 mod 17 = 4). In Python there's a built-in operator for performing this operation: pow(base, exponent, modulus)

In RSA, modular exponentiation, together with the problem of prime factorisation, helps us to build a "trapdoor function". This is a function that is easy to compute in one direction, but hard to do in reverse unless you have the right information. It allows us to encrypt a message, and only the person with the key can perform the inverse operation to decrypt it.

Find the solution to 101<sup>17</sup> mod 22663

##### Writeup:

As mentioned in the wrietup we use `pow()` function of the python to get the result.

```python
#!/usr/bin/env python3
answer = pow(101,17,22663)
print (answer)

```
```shell
┌──(rinshu㉿kali)-[~]
└─$ ./rsa1.py 
19906

```

Answer: ***19906***

### RSA Starter 2

##### Challenge Description:

RSA encryption is modular exponentiation of a message with an exponent e and a modulus N which is normally a product of two primes: N = p * q.

Together the exponent and modulus form an RSA "public key" (N, e). The most common value for e is 0x10001 or 65537.

"Encrypt" the number 12 using the exponent e = 65537 and the primes p = 17 and q = 23. What number do you get as the ciphertext?

##### Writeup:

As we know in RSA the ciphertext encrypt using public key.

ciphertext = (message)<sup>e</sup> mod n

Here n = p*q = 17*23 = 391

e = 65537

ciphertext = 12<sup>65537</sup> mod 391

```python
#!/usr/bin/env python3
result = pow (12,65537,17*23)
print (result)
```
```shell
┌──(rinshu㉿kali)-[~]
└─$ ./encrypt.py   
301
```
Answer = ***301***

### RSA Starter 3

##### Challenge Description:

RSA relies on the difficulty of the factorisation of the modulus N. If the primes can be found then we can calculate the Euler totient of N and thus decrypt the ciphertext.

Given N = p*q and two primes:

p = 857504083339712752489993810777

q = 1029224947942998075080348647219

What is the totient of N?

##### Writeup:

Totient of n counts the positive integers up to n that are relatively prime to n.

If n is written as prime factor of two number p and q then the formula for totient is (p-1)*(q-1).

Thus,
```python
#!/usr/bin/env python3
p = 857504083339712752489993810777
q = 1029224947942998075080348647219

totient = (p-1)*(q-1)

print (totient)

```
```shell
┌──(rinshu㉿kali)-[~]
└─$ ./totient.py 
882564595536224140639625987657529300394956519977044270821168

```
Answer: ***882564595536224140639625987657529300394956519977044270821168***

---

### RSA Starter 4

##### Challenge Description:
The private key d is used to decrypt ciphertexts created with the corresponding public key (it's also used to "sign" a message but we'll get to that later).

The private key is the secret piece of information or "trapdoor" which allows us to quickly invert the encryption function. If RSA is implemented well, if you do not have the private key the fastest way to decrypt the ciphertext is to first factorise the modulus.

In RSA the private key is the modular multiplicative inverse of the exponent e modulo the totient of N.

Given the two primes:

p = 857504083339712752489993810777

q = 1029224947942998075080348647219

and the exponent:

e = 65537

What is the private key d?

##### Writeup:

We can find the private key d using public key e.

We know that d ≡ e<sup>-1</sup> mod ϕ(n),where ϕ(n) is the totient of n.

Thus,
```python
#!/usr/bin/env python3
p =857504083339712752489993810777
q = 1029224947942998075080348647219
e = 65537

totient = (p-1)*(q-1)

d= pow(e,-1,totient)
print (d)
```

```shell
┌──(rinshu㉿kali)-[~]
└─$ ./rsa4.py   
121832886702415731577073962957377780195510499965398469843281
```
d = ***121832886702415731577073962957377780195510499965398469843281***

---

### RSA Starter 5

##### Challenge Description:

I've encrypted a secret number for your eyes only using your public key parameters:

N = 882564595536224140639625987659416029426239230804614613279163

e = 65537

Use the private key that you found for these parameters in the previous challenge to decrypt this ciphertext:

c = 77578995801157823671636298847186723593814843845525223303932

##### Writeup:

We know the private key here as d = *121832886702415731577073962957377780195510499965398469843281*

To decrypt the ciphertext we use this formula

message = c<sup>d</sup> mod n
```python
#!/usr/bin/env python3
n = 882564595536224140639625987659416029426239230804614613279163
p = 857504083339712752489993810777
q = 1029224947942998075080348647219
e = 65537

totient = (p-1)*(q-1)
d= pow(e,-1,totient)

c= 77578995801157823671636298847186723593814843845525223303932

message = pow(c,d,n)

print (message)

```

```shell
┌──(rinshu㉿kali)-[~]
└─$ ./decrypt.py   
13371337

```
Answer: ***13371337***

---

### RSA Starter 6

##### Challenge Description:

How can you ensure that the person receiving your message knows that you wrote it?

You've been asked out on a date, and you want to send a message telling them that you'd love to go, however a jealous lover isn't so happy about this.

When you send your message saying yes, your jealous lover intercepts the message and corrupts it so it now says no!

We can protect against these attacks by signing the message.

Imagine you write a message M. You encrypt this message with your friend's public key:C = M<sup>e<sub>0</sub></sup> mod N<sub>0</sub>.

To sign this message, you calculate the hash of the message: H(M) and "encrypt" this with your private key: S = H(M)<sup>d<sub>1</sub></sup> mod N<sub>1</sub>.

Your friend can decrypt the message using their private key: m = C<sup>d<sub>0</sub></sup> mod N<sub>0</sub>. Using your public key they calculate s = S<sup>e<sub>1</sub></sup> mod N<sup>1</sup>.

Now by computing H(m) and comparing it to s: assert H(m) == s, they can ensure that the message you sent them, is the message that they received!

Sign the flag crypto{Immut4ble_m3ssag1ng} using your private key and the SHA256 hash function.

Challenge files:
  - [private.key](https://github.com/Divyanshukumar20/CSOC24/blob/main/Week2/Writeup_files/private_0a1880d1fffce9403686130a1f932b10.key)

##### Writeup:

Here we have to sign the flag using given private and SHA256 hash function and submit the number we got.

First we convert the flag to its hash value and then convert thst value into integer.

We use hashlib library to get the hash value.
After getting the hash value from SHA256 hash we convert it to bytes to get the integer and then this bytes is converted in long integer using 'bytes_to_long()' function.
```python
#!/usr/bin/env python3
from Crypto.Util.number import bytes_to_long
import hashlib

message = "crypto{Immut4ble_m3ssag1ng}"

sha256_hash = hashlib.sha256()

sha256_hash.update(message.encode())
hash_value = sha256_hash.hexdigest()
bytes = bytes.fromhex(hash_value)
integer = bytes_to_long(bytes)

print (integer)

```
```shell
┌──(rinshu㉿kali)-[~]
└─$ ./rsa6.py   
69523276807549773371481917516452638375664281433555793080445569568100703974091

```

At final we get our hash value as integer is *69523276807549773371481917516452638375664281433555793080445569568100703974091*

Sign this integer using formula given in challenge using private key given.
```python
H_M =69523276807549773371481917516452638375664281433555793080445569568100703974091 
n = 15216583654836731327639981224133918855895948374072384050848479908982286890731769486609085918857664046075375253168955058743185664390273058074450390236774324903305663479046566232967297765731625328029814055635316002591227570271271445226094919864475407884459980489638001092788574811554149774028950310695112688723853763743238753349782508121985338746755237819373178699343135091783992299561827389745132880022259873387524273298850340648779897909381979714026837172003953221052431217940632552930880000919436507245150726543040714721553361063311954285289857582079880295199632757829525723874753306371990452491305564061051059885803
d = 11175901210643014262548222473449533091378848269490518850474399681690547281665059317155831692300453197335735728459259392366823302405685389586883670043744683993709123180805154631088513521456979317628012721881537154107239389466063136007337120599915456659758559300673444689263854921332185562706707573660658164991098457874495054854491474065039621922972671588299315846306069845169959451250821044417886630346229021305410340100401530146135418806544340908355106582089082980533651095594192031411679866134256418292249592135441145384466261279428795408721990564658703903787956958168449841491667690491585550160457893350536334242689

sign = pow(H_M,d,n)

print (sign)

```
Running this program
```shell
┌──(rinshu㉿kali)-[~]
└─$ ./sign.py       
13480738404590090803339831649238454376183189744970683129909766078877706583282422686710545217275797376709672358894231550335007974983458408620258478729775647818876610072903021235573923300070103666940534047644900475773318682585772698155617451477448441198150710420818995347235921111812068656782998168064960965451719491072569057636701190429760047193261886092862024118487826452766513533860734724124228305158914225250488399673645732882077575252662461860972889771112594906884441454355959482925283992539925713424132009768721389828848907099772040836383856524605008942907083490383109757406940540866978237471686296661685839083475

```
Answer: ***13480738404590090803339831649238454376183189744970683129909766078877706583282422686710545217275797376709672358894231550335007974983458408620258478729775647818876610072903021235573923300070103666940534047644900475773318682585772698155617451477448441198150710420818995347235921111812068656782998168064960965451719491072569057636701190429760047193261886092862024118487826452766513533860734724124228305158914225250488399673645732882077575252662461860972889771112594906884441454355959482925283992539925713424132009768721389828848907099772040836383856524605008942907083490383109757406940540866978237471686296661685839083475***

---
