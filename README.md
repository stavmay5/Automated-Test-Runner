# 🎓 C Auto-Grader System

An automated grading system built in **C** for Linux environments.
This tool iterates through student directories, compiles their C programs, executes them with specific inputs, compares the output against an expected result, and generates a grade report (CSV).

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
```

### 3. Configuration
Create a file named `config.txt` in the same directory. It must contain exactly **3 lines** with the paths to your files:

**Example content of** `config.txt`:
```Plaintext
./students
./input.txt
./expected_output.txt
```
(Line 1: Students folder path, Line 2: Input file path, Line 3: Expected result file path)

### 4. Execution
Run the grader with the config file argument:
```bash
./Grader.out config.txt
```

### 5. Results
The system will generate a `results.csv` file containing the final grades.

## 📂 File Structure
 * `file_comparator.c`: File comparison logic (The "Judge").
 * `auto_grader.c`: Main automation logic (The "Manager").
 * `input.txt`: The input numbers fed into the students' programs.
 * `expected_output.txt`: The correct output expected from the students.
