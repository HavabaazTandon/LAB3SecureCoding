# Lab 3 - Memory Defect Detection and Remediation

## Experiment 3: Memory Defect Detection and Remediation

### Tools Used
- GCC
- Valgrind
- AddressSanitizer (ASan)

### Memory Defects Analysed
1. Uninitialized variable
2. Memory leak
3. Double free

Each defect was tested using original and corrected C programs. Valgrind and AddressSanitizer were used to identify the errors and verify the corrections.

### Result
All three memory defects were identified and corrected. The corrected programs passed the performed Valgrind and AddressSanitizer checks.

## Folder Structure
- Exp3: Original and corrected C programs
- Exp4: Files for the separate dirty-code analysis experiment
- evidence: Valgrind and AddressSanitizer output files
- report: Experiment reports and findings

## Repository
https://github.com/HavabaazTandon/LAB3SecureCoding
