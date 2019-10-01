---
title: 'A simple and fun C++ program Keyboard Cat'
date: 2019-10-01
permalink: /posts/2019/10/keyboard-cat-linux-cpp-random-string/
tags:
  - Programming
  - C++
  - Linux
---

Recently i was working on a CTF challenge found online. I came a across a problem where i have to send random characters to a an executable. I found some long linux commands to generate random strings. Why no one has made a simple program to get this job done? I decided to make simple program myself.

Either i am too lazy to search for a program or i just love c++, or may be both. I don’t know. Keyboard cat or kcat can simply generate ransom ASCII characters and stream to stdout.

I’m not sure about the possible use cases of this program but it was fun.

# How to install keboard cat in linux
### Install dependencies
##### Debian, Ubuntu
```
sudo apt-get install cmake gcc
```
##### Arch linux
```
sudo pacman -S cmake gcc
```
### Install kcat
```
git clone https://github.com/SusmithKrishnan/keyboardcat
./configure
make
sudo make instal
```

### keyboardcat
Keyboard cat is a simple CLI tool to generate ransom streams of ASCII characters to stdout. Speed and Charset can be adjusted and written to stdout or file. Can be used as simple random string generator or for display purpose. If there is any bug or feature request feel free to create an Issue or pull request.
```
Usage
KCat v1.0
Keboard cat usage:
    -d    --delay      Delay between each char in microseconds
    -s    --slow       Print in slow mode
    -f    --fast       Print in fast mode
    -i    --insane     Print in insane mode
    -l    --lower-case Include lowercase characters
    -u    --upper-case Include uppercase characters
    -n    --num        Include numbers
    -x    --special    Include special chars
    -h    --help       Print this help and exit
```    

### Example

Print numbers only
```
kcat -n
```

Print lowercase alphanum
```
kcat -ln
```

Print special chars faster
```
kcat -x -d 10
```
