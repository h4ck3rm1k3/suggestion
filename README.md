Suggestion
==========

> Simple input box pull-down prompt service

### Introduction

In the search input box and other locations, the user input keywords, the system prompts you can use the keyword to enhance the user experience

### screenshot

! [Img] (https://raw.githubusercontent.com/wklken/gallery/master/suggestion/suggestion.gif)

### dependency

1. jquery-2.1.1.min.js

Twitter typeahead 0.10.5 [github] (https://github.com/twitter/typeahead.js/) | [examples] (http://twitter.github.io/typeahead.js/examples/)

### use

Clone

2. go run test_web.go

3. http: // localhost: 9090

4. input

---------------

### data file format

Default file format:

    Format: word \ tweight
    Coding: utf-8 [must]
    Require: weight type (int)

    Plant war zombie \ t1000






### implementation way 1: easymap

Use the map way to achieve the tree structure, there are python and golang two versions (see easymap subdirectory)

Quick run:
`` `Shell
Git clone https://github.com/wklken/suggestion.git
Cd suggestion / easymap
Python suggest.py
Go run suggest.go
`` ``


`` ``
Applicable: small system, the keyword in 10W or so (Chinese + Pinyin + Pinyin total of about 30W)
Advantages: logical simple structure clear, the code is small enough to facilitate the expansion (eg to modify the storage structure, in the return to add pictures and other additional information)
Disadvantages: memory footprint, 30W keywords, the average word length 3, take 800M memory, the other also have a certain consumption of cpu
Handling and Practice:
      Python version plus layer of redis / memcached, python version, stand-alone 8 process, 16 core, take 1G memory, the total daily request in the 300-500w or so, qps peak in 300 or so, no pressure [ .]
      Golang version did not try to produce, should be no pressure
`` ``

### implementation mode 2: double-array-trie

Use the darts implementation to achieve double-array-trie, golang code

Darts implementation reference project: [awsong / go-darts] (https://github.com/awsong/go-darts)

Double-array-trie article: [What is Trie] (http://en.wikipedia.org/wiki/Trie) | [An Implementation of Double-Array Trie] (http://linux.thai.net/~thep /datrie/datrie.html)

Quick run
`` ``
Go run test_web.go
Visit http: // localhost: 9090

Or

 go run test_run.go

Input dict length: 29
Build out length 65708
3.55us
<Nil>
Search: Plant Wars
Result Len: 10
Plant Wars Zombie 154717704
Plant Wars zombie year Chinese version 44592048
Plant Wars Zombie OL 43566752
Plant Wars Zombie 2 630955
Plant Wars Alien 530403
Plant War Monster 29727
Plant Wars Alien Variety Edition 14773
Plant Wars Bugs 5999
Plant Wars Alien 4456
Plant War Inse 2 Invincible Edition 3419
`` ``


`` ``
Applicable: keywords in more than 10w system
Advantages: small memory footprint, performance guarantee
Disadvantages: the underlying rely on double-array-trie, logic a bit around the custom is not very convenient
Handling and practice: add a layer of redis / memcached
`` ``

#### TODO

    Focus on darts version (easymap separated)
    Performance test
    2. The data structure can be customized
    3. Fault-tolerant processing
    4 case, pinyin, the first letter and so on

#### Change Log

    2013-10-13 created, python version
    2013-12-14 increase golang version
    2014-05-11 Increase the double-array-trie implementation of the golang version
    2014-11-04 fix golang version bug, increase front end show

#### Donation

If you think my project is helpful to you, you can buy me a coffee :)

! [Donation] (https://raw.githubusercontent.com/wklken/gallery/master/donation/donation.png)

---------------

Wklken (Pythonista / Vimer)

Email: wklken@yeah.net

Blog: http://www.wklken.me

Github: https://github.com/wklken

2013-10-13 in Shenzhen
