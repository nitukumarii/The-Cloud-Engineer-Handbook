Whenever you provide Python code, format it exactly as a GitHub Markdown code block.

Requirements:
- Wrap the code inside triple backticks with `python` (```python ... ```).
- Preserve proper indentation (4 spaces).
- Do not put the code on a single line.
- Do not add line numbers.
- Do not add explanations inside the code block.
- Add a short comment at the top describing the problem (e.g., `# Problem: Count ERROR lines from a log file`).
- Ensure the code is ready to copy and paste directly into GitHub or VS Code.

Example format:

```python
# Problem: Print all ERROR lines from a log file

def error_lines(log_file):
    with open(log_file, "r") as file:
        for line in file:
            if "ERROR" in line:
                print(line.strip())
```
