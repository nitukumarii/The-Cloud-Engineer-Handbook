

# Problem: Print all ERROR lines from a log file

def error_lines(log_file):
    with open(log_file, "r") as file:
        for line in file:
            if "ERROR" in line:
                print(line.strip())


    ## `strip()` in Python

`strip()` is a built-in string method that removes unwanted whitespace characters from the beginning and end of a string, such as spaces, tabs (`\t`), and newline characters (`\n`). It is commonly used when reading files because each line usually ends with a newline character (`\n`). Using `line.strip()` removes the newline and any extra spaces, making the output cleaner and easier to compare or process. It does not modify the original string; instead, it returns a new cleaned string.


