# Oracle OCI Cloud Operations Engineer (IC3) - Python Scripting Topics

These are the most common Python topics required for Cloud Operations, SRE, Linux Automation, and HackerRank scripting rounds.

## 1. Python Basics ⭐⭐⭐⭐⭐
- Variables
- Data Types
- Operators
- Input/Output

---

## 2. Conditional Statements ⭐⭐⭐⭐⭐
- if
- if-else
- elif
- Nested if

---

## 3. Loops ⭐⭐⭐⭐⭐
- for
- while
- break
- continue
- range()

---

## 4. Functions ⭐⭐⭐⭐⭐
- def
- Parameters
- Return values
- Scope

---

## 5. Strings ⭐⭐⭐⭐⭐
- strip()
- split()
- replace()
- lower()
- upper()
- find()
- startswith()
- endswith()
- String slicing

---

## 6. Lists ⭐⭐⭐⭐⭐
- append()
- remove()
- pop()
- sort()
- len()
- Indexing
- Iteration

---

## 7. Dictionaries ⭐⭐⭐⭐⭐
- Creating dictionaries
- Accessing values
- get()
- keys()
- values()
- items()
- Frequency counting

---

## 8. Tuples ⭐⭐⭐
- Creating tuples
- Packing & unpacking

---

## 9. Sets ⭐⭐⭐
- add()
- remove()
- Union
- Intersection
- Remove duplicates

---

## 10. File Handling ⭐⭐⭐⭐⭐
- open()
- read()
- readline()
- readlines()
- write()
- append()
- with open()
- File modes (r, w, a)

---

## 11. Exception Handling ⭐⭐⭐⭐
- try
- except
- finally
- raise

---

## 12. Modules & Packages ⭐⭐⭐⭐
- import
- from ... import ...
- os
- sys
- pathlib
- subprocess
- socket
- ssl
- json
- csv
- datetime

---

## 13. JSON Processing ⭐⭐⭐⭐
- json.load()
- json.loads()
- json.dump()
- json.dumps()

---

## 14. CSV Processing ⭐⭐⭐
- csv.reader()
- csv.writer()
- Reading reports
- Writing reports

---

## 15. Date & Time ⭐⭐⭐⭐
- datetime.now()
- timedelta
- strptime()
- strftime()

---

## 16. Regular Expressions (Regex) ⭐⭐⭐
- re.search()
- re.match()
- re.findall()
- Extract IPs
- Extract timestamps
- Validate patterns

---

## 17. Basic OOP ⭐⭐
- Class
- Object
- self
- __init__()
- Instance Attribute
- Class Attribute

---

## 18. Networking Modules ⭐⭐⭐⭐
- socket
- ssl
- HTTP requests
- DNS lookup
- Port connectivity

---

## 19. Linux Automation ⭐⭐⭐⭐⭐
- Execute Linux commands
- Parse log files
- Process monitoring
- Disk usage automation
- Backup scripts
- Health check scripts

---

## 20. Common HackerRank Scripting Problems ⭐⭐⭐⭐⭐
- Parse log files
- Count ERROR/WARNING entries
- Top N IP addresses
- Count HTTP status codes
- Find duplicate lines
- Read CSV and generate reports
- Parse JSON
- Reverse a string
- Count words
- Find duplicate words
- Validate IP addresses
- SSL Certificate Expiry Checker
- Disk Usage Report
- CPU Monitoring Script
- Memory Usage Report
- Backup Automation Script
- Process Monitoring Script

---

# Not Required for Oracle OCI Cloud Operations HackerRank

- ❌ Dynamic Programming
- ❌ Binary Trees
- ❌ Graph Algorithms
- ❌ Linked Lists
- ❌ Tries
- ❌ Segment Trees
- ❌ Advanced System Design
- ❌ Competitive Programming

---

# Recommended Learning Order

1. Python Basics
2. Functions
3. Strings
4. Lists
5. Dictionaries
6. File Handling
7. Exception Handling
8. JSON
9. CSV
10. Date & Time
11. Modules
12. Linux Automation Scripts
13. Networking Automation
14. OOP Basics


# Python Coding Practice for SRE / DevOps / Cloud Interviews

These are the most commonly asked beginner-to-intermediate Python coding questions in SRE, DevOps, Cloud Engineer, and Infrastructure interviews (Oracle, Amazon, Microsoft, Google, etc.).

---

# 1. Strings

## Reverse a String
- Reverse using slicing
- Reverse using loop
- Reverse without built-in functions

Example:
```
Input: "oracle"
Output: "elcaro"
```

---

## Compare Two Strings

Check whether two strings are equal.

Example:
```
Input:
abc
abc

Output:
Equal
```

---

## Check Palindrome

Determine whether a string reads the same forward and backward.

Example:
```
Input: madam
Output: True
```

---

## Check Anagram

Determine whether two strings contain the same characters.

Example:
```
Input:
listen
silent

Output:
True
```

---

## Count Vowels

Count the total vowels in a string.

Example:
```
Input: interview
Output: 4
```

---

## Count Character Frequency

Return frequency of every character.

Example:
```
Input: apple

Output:
a : 1
p : 2
l : 1
e : 1
```

---

## First Non-Repeating Character

Example:
```
Input: swiss

Output:
w
```

---

## Remove Duplicate Characters

Example:
```
Input: programming

Output:
progamin
```

---

# 2. Arrays / Lists

## Find Maximum Number

Example:
```
Input:
[3,7,2,9,5]

Output:
9
```

---

## Find Second Largest Number

Example:
```
Input:
[10,4,8,20,15]

Output:
15
```

---

## Remove Duplicates

Example:
```
Input:
[1,2,2,3,4,4,5]

Output:
[1,2,3,4,5]
```

---

## Merge Two Arrays

Example:
```
Input:
[1,2,3]
[4,5]

Output:
[1,2,3,4,5]
```

---

## Find Missing Number

Example:
```
Input:
[1,2,3,5]

Output:
4
```

---

## Rotate Array

Rotate an array by K positions.

Example:
```
Input:
[1,2,3,4,5]
K = 2

Output:
[4,5,1,2,3]
```

---

## Count Occurrences

Count how many times an element appears.

Example:
```
Input:
[1,2,2,3,2]

Output:
2 occurs 3 times
```

---

# 3. Dictionaries

## Word Frequency

Count each word in a sentence.

Example:
```
Input:
python is easy python is powerful

Output:
python : 2
is : 2
easy : 1
powerful : 1
```

---

## Character Frequency

Store frequency using a dictionary.

Example:
```
Input:
banana

Output:
b : 1
a : 3
n : 2
```

---

## Count Duplicate Elements

Return only duplicated elements.

Example:
```
Input:
[1,2,2,3,4,4,5]

Output:
2
4
```

---

# 4. Files

## Read a Log File

Read every line from a log file.

Common interview topic for SRE roles.

---

## Print ERROR Lines

Extract only ERROR entries.

Example:
```
INFO Server Started
ERROR Database Down
INFO User Login
ERROR Timeout

Output:

ERROR Database Down
ERROR Timeout
```

---

## Count ERROR Entries

Return total ERROR messages.

Example:
```
Output:
2
```

---

## Parse CSV

Read CSV files using Python.

Typical operations:

- Read rows
- Print rows
- Search values
- Count records

---

## Parse JSON

Load JSON and access values.

Typical operations:

- Read JSON
- Extract keys
- Update values
- Print nested fields

---

# 5. Functions

## Retry Function

Write a function that retries an operation if it fails.

Common interview topic in SRE automation.

Concepts covered:

- Loops
- Exception handling
- Sleep
- Retry count

---

## Health Check Function

Write a function that checks whether a service is healthy.

Typical checks:

- Website reachable
- API returns HTTP 200
- Process running
- Port open

---

# HackerRank Topics to Master

Focus on beginner-to-intermediate problems involving:

- ✅ Strings
- ✅ Lists (Arrays)
- ✅ Dictionaries
- ✅ Loops
- ✅ Functions
- ✅ File Handling
- ✅ Basic Searching
- ✅ Basic Sorting
- ✅ Exception Handling

---

# Suggested Practice Order

1. Strings
2. Lists / Arrays
3. Dictionaries
4. Functions
5. File Handling
6. JSON
7. CSV
8. Exception Handling
9. Automation Scripts
10. HackerRank Practice

---

# Goal

Master approximately **25–30 beginner-to-intermediate HackerRank problems** instead of diving into advanced Data Structures & Algorithms.

For most SRE, DevOps, Cloud, and Infrastructure Engineer interviews, strong Python fundamentals, scripting, debugging, and automation skills are significantly more valuable than advanced algorithmic techniques.
