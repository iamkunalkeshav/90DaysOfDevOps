# File Read and Write Practice – Day 06

This note documents basic Linux file input/output practice.
The goal is to understand how to create files, write text,
append new lines, and read files using fundamental commands.

---

## File Creation

- `touch notes.txt`  
  Creates an empty file named `notes.txt`.

---

## Writing to a File (Overwrite)

- `echo "This is line 1" > notes.txt`  
  Writes the first line to the file.  
  If the file already exists, its contents are overwritten.

---

## Appending to a File

- `echo "This is line 2" >> notes.txt`  
  Appends a second line to the file without removing existing content.

- `echo "This is line 3" | tee -a notes.txt`  
  Appends a third line to the file and also prints it to the terminal.

---

## Reading the File

- `cat notes.txt`  
  Displays the full contents of the file.

---

## Reading Parts of the File

- `head -n 2 notes.txt`  
  Displays the first two lines of the file.

- `tail -n 2 notes.txt`  
  Displays the last two lines of the file.

---

## Key Learnings

- `>` overwrites file content
- `>>` appends to a file
- `tee` writes and displays output at the same time
- `cat`, `head`, and `tail` are used to read files efficiently

These commands are commonly used when working with logs,
configuration files, and scripts in DevOps.
