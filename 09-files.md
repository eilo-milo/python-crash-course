

---

# Working with File Objects (Reading, Writing, and Binary Files)


---

## 1. Opening and Closing Files

### 1.1 Manual Open and Close
* Files can be opened using Python's built-in `open()` function.
* Explicitly calling `.close()` is mandatory when using this approach; failing to close files risks descriptor leaks and system resource exhaustion.

```python
f = open('test.txt', 'r')
print(f.name)
print(f.mode)
f.close()
```

### 1.2 Using Context Managers (`with`)
* The standard best practice for handling file operations is using the `with open(...) as f:` context manager syntax.
* Automatically handles file closure upon exiting the block, even if runtime exceptions are raised.
* Accessing file operations outside the context block raises a `ValueError: I/O operation on closed file`.

```python
with open('test.txt', 'r') as f:
    f_contents = f.read()
    print(f_contents)

# f.closed evaluates to True outside the block
```

---

## 2. File Access Modes

| Mode | Identifier | Description |
| :--- | :--- | :--- |
| **Read** | `'r'` | Default mode. Opens a file for reading; throws `FileNotFoundError` if missing. |
| **Write** | `'w'` | Opens a file for writing. Creates the file if non-existent, completely overwrites if it exists. |
| **Append** | `'a'` | Opens a file to append data to the end without truncating existing content. |
| **Read & Write** | `'r+'` | Opens a file simultaneously for reading and writing operations. |
| **Binary Modes** | `'rb'`, `'wb'` | Reads or writes raw binary bytes (used for images, PDFs, audio, executables). |

---

## 3. Reading Files Efficiently

### 3.1 `.read()`, `.readlines()`, and `.readline()`
* **`f.read()`**: Loads the entire file contents into memory as a single string.
* **`f.readlines()`**: Returns a Python list containing every line as a separate string element (including newline characters `\n`).
* **`f.readline()`**: Reads and returns a single line sequentially on each call.

```python
with open('test.txt', 'r') as f:
    first_line = f.readline()
    print(first_line, end='')
```

### 3.2 Iterating Over File Lines
* Directly iterating over the file object using a `for` loop processes data line by line without loading the full file into memory.

```python
with open('test.txt', 'r') as f:
    for line in f:
        print(line, end='')
```

### 3.3 Reading in Fixed Chunk Sizes
* Passing an integer size argument to `f.read(size)` specifies character batch lengths.
* When the pointer reaches EOF (end-of-file), `f.read()` returns an empty string `""`.

```python
with open('test.txt', 'r') as f:
    size_to_read = 100
    f_contents = f.read(size_to_read)
    
    while len(f_contents) > 0:
        print(f_contents, end='')
        f_contents = f.read(size_to_read)
```

### 3.4 Managing Pointer Positions (`tell` and `seek`)
* **`f.tell()`**: Returns the current byte/character position of the read/write cursor in the file stream.
* **`f.seek(offset)`**: Moves the cursor to the specified position index (e.g., `f.seek(0)` resets the cursor to the start of the file).

```python
with open('test.txt', 'r') as f:
    f_contents = f.read(10)
    print(f.tell())  # Output: 10
    
    # Reset pointer back to the beginning
    f.seek(0)
    f_contents = f.read(10)
    print(f_contents)
```

---

## 4. Writing to Files

### 4.1 Creating and Overwriting
* Attempting `.write()` in read mode triggers an `io.UnsupportedOperation: not writable`.
* Opening in write mode (`'w'`) creates the file automatically if it does not already exist, or truncates existing files to 0 bytes.

```python
with open('test2.txt', 'w') as f:
    f.write("First Line\n")
    f.write("Second Line\n")
```

### 4.2 Appending Data
* Using mode `'a'` ensures subsequent writes add onto existing content rather than overwriting the entire file.

```python
with open('test2.txt', 'a') as f:
    f.write("Appended Line\n")
```

### 4.3 Overwriting via Pointer Manipulation
* Using `f.seek(0)` inside a write-mode context positions the pointer at the beginning and selectively overwrites only matching character byte lengths rather than erasing subsequent data.

---

## 5. Working with Multiple Files & Copying

### 5.1 Copying Text Files Line by Line
* Multiple files can be opened by nesting `with` statements to read from a source file while writing to a destination file.

```python
with open('test.txt', 'r') as rf:
    with open('test_copy.txt', 'w') as wf:
        for line in rf:
            wf.write(line)
```

### 5.2 Working with Binary Files (Images)
* Non-text files (such as `.jpg`, `.png`, `.mp4`) must be opened in binary mode (`'rb'` / `'wb'`) to prevent `UnicodeDecodeError` / UTF-8 codec decode failures.

### 5.3 Chunk-Based Binary Copying
* For large files and binary assets, read and write data in fixed memory chunks (e.g., 4096 bytes).

```python
with open('bronx.jpg', 'rb') as rf:
    with open('bronx_copy.jpg', 'wb') as wf:
        chunk_size = 4096
        rf_chunk = rf.read(chunk_size)
        
        while len(rf_chunk) > 0:
            wf.write(rf_chunk)
            rf_chunk = rf.read(chunk_size)
```

---
