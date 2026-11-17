# Experiment 4: Dirty-Code Analysis and Standards-Compliant Refactoring

## Aim
To analyse the faculty-provided C code for dirty-code practices with security impact, refactor it, and compare Cppcheck results before and after correction.

## Findings Table

| No. | Dirty-code practice | Location | Security / code-quality consequence | Relevant standard / guidance |
|---|---|---|---|---|
| 1 | Unsafe strcpy and insufficient buffer | dirty_code.c, lines 6–8 | Buffer overflow and possible memory corruption | CERT C STR31-C |
| 2 | Magic numbers | dirty_code.c, line 10 and lines 12–14 | Reduces readability and maintainability | Secure coding maintainability practice |
| 3 | Deeply nested conditions | dirty_code.c, lines 12–18 | Makes code difficult to read, review and maintain | MISRA C guidance on control flow |
| 4 | Dead code | dirty_code.c, lines 20–22 | Unreachable code adds unnecessary complexity | MISRA C:2012 Rules 2.1 and 2.2 |
| 5 | Unchecked fopen return value | dirty_code.c, line 24 | A NULL file pointer may be passed to fprintf | CERT C EXP34-C |
| 6 | Unchecked fprintf return value | dirty_code.c, line 25 | Failed writes may go unnoticed | Defensive file-I/O error handling |
| 7 | Unchecked fclose return value | dirty_code.c, line 27 | File closing or flushing errors may go unnoticed | Defensive file-I/O error handling |

## Cppcheck Analysis Before Refactoring

Command:
cppcheck --enable=all --inconclusive --std=c11 --suppress=missingIncludeSystem Exp4/dirty_code.c

Observed results:
- One buffer-access-out-of-bounds error related to strcpy().
- Three style warnings for conditions that are always true because marks is assigned 75.
- The scan also displayed an informational active-checkers message.

## Refactoring Performed

- Replaced unsafe strcpy() with a sufficiently sized character array.
- Introduced named constants for marks.
- Removed unnecessary nested conditions.
- Removed the unreachable if (0) block.
- Added a NULL check after fopen().
- Checked the return value of fprintf().
- Checked the return value of fclose().

## Cppcheck Analysis After Refactoring

Command:
cppcheck --enable=all --inconclusive --std=c11 --suppress=missingIncludeSystem clean_code.c

Observed result:
- No warnings or errors reported.
- Only the informational active-checkers message was displayed.

## Compilation and Execution

Compilation:
gcc -Wall -Wextra -Wpedantic -std=c11 clean_code.c -o clean_code

Execution:
./clean_code

Output:
Excellent

The corrected program compiled and executed successfully.

## Result

The original program contained unsafe string handling, magic numbers, deeply nested conditions, dead code and unchecked file operations. After refactoring, Cppcheck reported no warnings or errors, and the corrected program compiled and executed successfully.
