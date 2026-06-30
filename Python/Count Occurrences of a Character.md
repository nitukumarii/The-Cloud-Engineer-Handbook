# Problem: Count Occurrences of a Character

## Task

Write a function that takes:

- A string `s`
- A character `ch`

Return how many times `ch` appears in `s`.

---

## Function Signature

```python
def count_character(s, ch):
    # Your code here
```

---

## Constraints

- Do NOT use `s.count(ch)`
- Use a loop
- Return the result (do not print it)

---

## Example 1

### Input
```python
s = "oracle cloud"
ch = "o"
```

### Output
```
2
```

---

## Example 2

### Input
```python
s = "mississippi"
ch = "s"
```

### Output
```
4
```

---














**Solution**


Keypoints 

* **Function parameters must be variable names, not values.**
* example - def count_character(oracle cloud, o):
oracle cloud, o - these are values not a variable


* **:(Colon)**
* Used to start a code block

def function():

if condition:

for loop:

* **;(Semicolon)**

* <img width="355" height="302" alt="image" src="https://github.com/user-attachments/assets/26e190fc-beb1-4a99-abc0-89442a5f2fb0" />



def count_character(s, ch):
    count = 0

    for i in s:
        if i == ch:
            count += 1

    return count


**Explaination**


Python first creates a variable called count in memory and assigns it the value 0, which acts as a local variable inside the function. Then the for loop goes through the string one character at a time. Each character is stored in i, and Python compares it with ch. If the condition is true, Python executes count = count + 1, which means it reads the current value of count, adds 1 to it, and stores the updated value back in the same variable. This keeps updating the same memory location. Finally, return count sends the final value of count outside the function as the result.

















## Hint (Optional)

Loop through each character in the string and increment a counter when it matches `ch`.
