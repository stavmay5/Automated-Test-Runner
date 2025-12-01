# 🎓 C Auto-Grader System

An automated grading system built in **C** for Linux environments.
This tool iterates through student directories, compiles their C programs, executes them with specific inputs, compares the output against an expected result, and generates a grade report (CSV).

## 👥 Authors
* **Stav Macri**
* **Nadav Swartz**

## 🚀 Key Features
* **Automated Compilation:** Uses `fork` and `exec` to run `gcc` on student submissions.
* **Safe Execution:** Runs each student's program in a separate child process.
* **I/O Redirection:** Uses `dup2` to feed input from a file (`input.txt`) and capture output automatically.
* **Result Comparison:** Includes a custom comparison module to validate outputs byte-by-byte.
* **CSV Reporting:** Generates a `results.csv` file with student names and grades.

---

## 🛠️ System Architecture & Visuals

### 1. The Comparator (`file_comparator.c`)
A utility that compares two files (student output vs. expected output) and returns a status code.
* **Return 1:** Files are different.
* **Return 2:** Files are identical.

![Comparator Demo](file_comparison_test.png)

### 2. The Manager (`auto_grader.c`)
The main engine that reads configuration, compiles student code, and grades it.

![File Structure Setup](config_file_paths.png)

---

## 💻 Usage

### 1. Prerequisites
* Linux environment (or WSL).
* GCC compiler.
* A folder structure containing student sub-directories.

### 2. Compilation
Compile the comparator and the main system using the new filenames:
```bash
gcc file_comparator.c -o comp.out
gcc auto_grader.c -o Grader.out
