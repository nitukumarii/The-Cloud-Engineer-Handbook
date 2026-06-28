"""
Simple log file parser to extract ERROR lines.
Useful for basic troubleshooting and debugging.
"""

def extract_errors(log_file_path):
    error_lines = []

    with open(log_file_path, "r") as file:
        for line in file:
            if "ERROR" in line:
                error_lines.append(line.strip())

    return error_lines


if __name__ == "__main__":
    log_file = "server.log"
    errors = extract_errors(log_file)

    for err in errors:
        print(err)
