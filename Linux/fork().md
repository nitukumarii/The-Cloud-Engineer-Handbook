# fork() in Linux

**Definition:**
`fork()` is a Linux system call that creates a new **child process** by duplicating the **parent process**.

## Return Values

| Return Value | Meaning |
|--------------|---------|
| `0` | Executing in the **child process**. |
| `> 0` | Executing in the **parent process**. The value returned is the **child's PID**. |
| `-1` | **Error** – Child process could not be created (e.g., process limit or insufficient resources). |

**Memory Trick:**
- `0` → Child
- `>0` → Parent (Child PID)
- `-1` → Error
