---
title: N88 BASIC reference
---

# Commands
## FILES / LFILES
*Usage*: `FILES <disk number>`
List the files that are on disk

*Examples*:
 * `FILES` List the files on the primary floppy disk.
 * `FILES 2` List the files on the secondary floppy disk.
 * `LFILES` List the files in a linear display instead of columnar.

## LOAD
*Usage*: `LOAD [filename] <,R>`
Load a program from disk.

*Examples*:
 * `LOAD "demo"` Load the `demo` program into RAM.
 * `LOAD "demo",r` Load and immediately run the `demo` program.
 * `LOAD "2:test.n88"` Load the `test.n88` program from the second floppy drive.

## SAVE
*Usage*: `SAVE [filename] <,A|,P>`
Save the current program to a file on disk. If you provide the same name as an existing file, the existing file will be overwritten.

*Examples*:
 * `SAVE "myprogram.n88"` Save the program as `myprogram.n88`
 * `SAVE "myprogram.n88",A` Save the program as `myprogram.n88` in raw ASCII format.
 * `SAVE "myprogram",P` Save the program as `myprogram` in an "encrypted binary format" (probably pre-tokenized/compiled?)
 * `SAVE "2:myprogram.n88"` Save the current program as `myprogram.n88` on the second floppy-disk drive.
