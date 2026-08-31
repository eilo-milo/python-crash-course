
---

# Working with the `os` and `os.path` Modules

---

## 1. Overview and Exploration
* The built-in `os` module provides direct programmatic access to underlying operating system operations (file system navigation, path resolution, environment variables, and process management).
* Use the built-in `dir()` function to inspect all attributes and callable methods available within the module.

```python
import os

print(dir(os))
```

---

## 2. Navigating and Querying the File System

### 2.1 Getting the Current Working Directory (`os.getcwd()`)
* `os.getcwd()` returns a string representing the directory path from which the script is currently executing.

```python
print(os.getcwd())
```

### 2.2 Changing Directories (`os.chdir()`)
* `os.chdir(path)` updates the current working directory to the target path provided as a string.

```python
os.chdir('/Users/username/Desktop')
print(os.getcwd())  # Output will reflect the Desktop directory
```

### 2.3 Listing Files and Folders (`os.listdir()`)
* `os.listdir(path='.')` returns a Python list of names of all files and folders inside the specified directory (defaults to the current working directory).

```python
print(os.listdir())
```

---

## 3. Creating, Deleting, and Renaming

### 3.1 Creating Directories (`mkdir` vs. `makedirs`)
* **`os.mkdir(path)`**: Creates a single top-level directory; throws an error if intermediate parent directories do not exist.
* **`os.makedirs(path)`**: Creates target directories recursively, automatically generating all missing intermediate subdirectories in the tree.

```python
# Creates single folder:
os.mkdir('OS-Demo')

# Creates full directory tree:
os.makedirs('OS-Demo/Sub-Dir-1/Sub-Dir-2')
```

### 3.2 Removing Directories (`rmdir` vs. `removedirs`)
* **`os.rmdir(path)`**: Deletes a single directory; fails if intermediate directories are included or the target folder is not empty.
* **`os.removedirs(path)`**: Recursively removes target and intermediate empty directories up the specified path.

```python
# Safer for targeted removals:
os.rmdir('OS-Demo/Sub-Dir-1')

# Recursive deletion:
os.removedirs('OS-Demo/Sub-Dir-1/Sub-Dir-2')
```

### 3.3 Renaming Files and Directories (`os.rename()`)
* `os.rename(src, dst)` takes the original path name first and renames it to the destination name provided in the second argument.

```python
os.rename('test.txt', 'demo.txt')
```

---

## 4. Inspecting File Metadata (`os.stat()`)
* `os.stat(filepath)` returns detailed metadata regarding a file or folder (e.g., file size, modification timestamps, ownership).
* `st_size`: Returns size in bytes.
* `st_mtime`: Returns the last modification time as a Unix timestamp. Convert it to human-readable format via `datetime.datetime.fromtimestamp()`.

```python
from datetime import datetime

file_stats = os.stat('demo.txt')

# Size in bytes
print(file_stats.st_size)

# Human-readable modification time
mod_time = file_stats.st_mtime
print(datetime.fromtimestamp(mod_time))
```

---

## 5. Traversing Directory Trees (`os.walk()`)
* `os.walk(top_path)` is a generator that recursively traverses an entire directory hierarchy from the top down.
* Yields a 3-value tuple on each iteration:
  1. `dirpath`: Current folder path string.
  2. `dirnames`: List of subdirectories inside current folder.
  3. `filenames`: List of files inside current folder.

```python
for dirpath, dirnames, filenames in os.walk('/Users/username/Desktop'):
    print('Current Path:', dirpath)
    print('Directories:', dirnames)
    print('Files:', filenames)
    print()
```

---

## 6. Environment Variables (`os.environ`)
* `os.environ` acts as a dictionary mapping environment variable names to their system values.
* Access specific variables using `.get('VAR_NAME')` to avoid runtime KeyError exceptions when keys do not exist.

```python
# Access user home directory
home_dir = os.environ.get('HOME')  # Windows: os.environ.get('USERPROFILE')
print(home_dir)
```

---

## 7. Path Manipulation with `os.path`

### 7.1 Joining Paths Accurately (`os.path.join`)
* Avoid manual string concatenation (`path + '/' + file`) because operating system path delimiters vary across platforms (`/` vs `\`).
* `os.path.join()` handles leading/trailing separators automatically without missing or double slashes.

```python
home_dir = os.environ.get('HOME')
file_path = os.path.join(home_dir, 'test.txt')
print(file_path)
```

### 7.2 Extracting Base and Directory Names
* **`os.path.basename(path)`**: Returns the final file/folder component of a path.
* **`os.path.dirname(path)`**: Returns the parent directory containing the base name.
* **`os.path.split(path)`**: Returns a tuple containing `(dirname, basename)`.

```python
fake_path = '/tmp/test/demo.txt'

print(os.path.basename(fake_path))  # Output: demo.txt
print(os.path.dirname(fake_path))   # Output: /tmp/test
print(os.path.split(fake_path))     # Output: ('/tmp/test', 'demo.txt')
```

### 7.3 Verifying Existence and Path Types
* `os.path.exists(path)`: Returns `True` if the path exists on disk.
* `os.path.isdir(path)`: Returns `True` if the path points to an existing directory.
* `os.path.isfile(path)`: Returns `True` if the path points to an existing file.

```python
print(os.path.exists('/tmp/demo.txt'))
print(os.path.isdir('/tmp'))
print(os.path.isfile('/tmp/demo.txt'))
```

### 7.4 Splitting File Extensions (`os.path.splitext`)
* `os.path.splitext(path)` cleanly separates the file root from the file extension into a 2-element tuple, avoiding fragile string-slice operations.

```python
file_path = '/tmp/test/demo.txt'
root, ext = os.path.splitext(file_path)

print(root)  # Output: /tmp/test/demo
print(ext)   # Output: .txt
```

---

