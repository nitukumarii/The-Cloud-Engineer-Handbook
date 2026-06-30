# Problem: Count Vowels in a String

def count_vowels(s):
    vowels = {'a', 'e', 'i', 'o', 'u'}
    count = 0

    for i in s:
        if i in vowels:
            count += 1

    return count



**Explaination**

Python creates a local variable count = 0 to keep track of vowels found in the string. Then it loops through each character of the string one by one. For every character, it checks whether it exists in the vowels set using in, which is fast because sets use hash-based lookup. If the character is a vowel, count is increased by 1 using count += 1, which updates the same variable in memory. Finally, return count sends the total number of vowels back as the output of the function.
