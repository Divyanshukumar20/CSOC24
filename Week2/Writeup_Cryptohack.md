# CSOC Week 2 Crytography

## Cryptohack Challenges

### Introduction 

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
