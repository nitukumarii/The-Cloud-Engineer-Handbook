**Network Connectivity Checker**


# Network Connectivity Checker

## Script

```bash
#!/bin/bash

host="example.com"

if ping -c 1 "$host" &>/dev/null; then
    echo "Network is up."
else
    echo "Network is down."
fi
```

---

```bash
-c 1
```

### Explanation

`-c` stands for **Count**.

It specifies how many ping packets should be sent.

Example:

```bash
ping -c 1 google.com
```

Sends only **one** ping packet and then exits.


The `$` symbol tells Bash to replace the variable with its value.


## 6. Output Redirection

```bash
&>/dev/null
```

### Explanation

A Linux command can produce two types of output:

- **Standard Output (stdout)** – Normal output
- **Standard Error (stderr)** – Error messages

`/dev/null` is a special Linux file called the **Null Device**.

Anything written to it is discarded permanently.

It behaves like a **black hole**.

Example:

```bash
echo "Hello" > /dev/null
```

Nothing is displayed because the output is discarded.

The operator

```bash
&>/dev/null
```

redirects **both stdout and stderr** to `/dev/null`.

Equivalent command:

```bash
>/dev/null 2>&1
```

### Why use it?

Normally,

```bash
ping -c 1 google.com
```

prints:

```text
PING google.com...
64 bytes from google.com...
```

Using

```bash
ping -c 1 google.com &>/dev/null
```

suppresses all output.

The script only cares whether the command succeeds or fails.

---

## 7. The `if` Statement

```bash
if ping -c 1 "$host" &>/dev/null; then
```

### Explanation

In Bash, an `if` statement checks the **exit status** of a command.

Exit Status:

- `0` → Success
- Non-zero → Failure

If the ping command succeeds, the `then` block executes.

If the ping command fails, the `else` block executes.

---

## 8. Success Message

```bash
echo "Network is up."
```

### Explanation

Executed only when the ping command is successful.

Output:

```text
Network is up.
```

---
