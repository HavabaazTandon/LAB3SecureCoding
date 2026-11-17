# Experiment 3: Memory Defect Detection and Remediation

## Aim
To identify, analyse, and remediate common memory defects in C programs using Valgrind and AddressSanitizer (ASan).

## Tools Used
- GCC
- Valgrind
- AddressSanitizer (ASan)
- Ubuntu on WSL

## Defects Analysed

### 1. Uninitialized Variable
The original program uses an integer variable without initializing it before reading its value.

**Remediation:** Initialize the variable to zero before use.

**Observation:** Valgrind Memcheck reported the use of an uninitialized value. ASan did not report this ordinary uninitialized integer read.

### 2. Memory Leak
The original program dynamically allocates memory using malloc() but does not release it using free().

**Remediation:** Release the allocated memory using free() after its use.

**Observation:** Valgrind reported 40 bytes as definitely lost. AddressSanitizer with leak detection also detected the memory leak.

### 3. Double Free
The original program releases the same dynamically allocated memory twice.

**Remediation:** Remove the second free() call and set the pointer to NULL after releasing the memory.

**Observation:** Valgrind reported an invalid free operation. AddressSanitizer detected the double-free error.

## Testing of Corrected Programs
The corrected programs were tested again using Valgrind and AddressSanitizer.

- Valgrind reported zero errors for the corrected programs.
- No memory leak was reported for the corrected programs.
- All three corrected ASan programs completed without sanitizer errors.

## Result
The three memory defects—uninitialized variable use, memory leak, and double free—were identified and corrected. The corrected programs passed the performed Valgrind and AddressSanitizer checks.
