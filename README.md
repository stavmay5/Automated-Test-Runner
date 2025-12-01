# 🎓 C Auto-Grader System

An automated grading system built in **C** for Linux environments.
This tool iterates through student directories, compiles their C programs, executes them with specific inputs, compares the output against an expected result, and generates a grade report (CSV).

## 👥 Authors
* **Stav Macri**
* **Nadav Swartz**

## 🚀 Key Features
* **Automated Compilation:** Uses `fork` and `exec` to run `gcc` on student submissions.
* **Safe Execution:** Runs each student's program in a separate child process.
* **I/O Redirection:** Uses `dup2` to feed input from a file (`input.txt`) and capture output to a file automatically.
* **Result Comparison:** Includes a custom comparison module (`Part1.c`) to validate outputs byte-by-byte.
* **CSV Reporting:** Generates a `results.csv` file with student names and grades.

## 🛠️ System Architecture
The system is composed of two main parts:
1.  **The Comparator (`Part1.c`):** A utility that compares two files (student output vs. expected output) and returns a status code.
2.  **The Manager (`Part2.c`):** The main engine that:
    * Reads configuration (paths to students, inputs, expected outputs).
    * Iterates over directories using `dirent.h`.
    * Compiles code using `execlp("gcc"...)`.
    * Runs the code with input redirection (`STDIN_FILENO` / `STDOUT_FILENO`).
    * Grades the result based on the comparator's return value.

## 💻 Usage

### 1. Prerequisites
* Linux environment (or WSL).
* GCC compiler.
* A folder structure containing student sub-directories.

### 2. Compilation
Compile the comparator and the main system using the following commands:
```bash
gcc Part1.c -o comp.out
gcc Part2.c -o Grader.out
