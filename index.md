---
title: N88 BASIC reference
---

# Commands
## CHR$
*Usage*: `CHR$([index])`
Return the shift-JIS character corresponding to an integer character code.

[Shift-JIS table for reference](http://rikai.com/library/kanjitables/kanji_codes.sjis.shtml)

*Examples*:
 * `CHR$(&H41)` => "A"
 * `CHR$(&H889F)` => "亜"

## CINT
*Usage*: `CINT([value])`
Convert to a 16-bit signed integer.

Values between -32768 and 37267 are valid, everything else gets an overflow error.

*Examples*:
 * `CINT(1.2345)` => 1
 * `CINT(-3.456)` => -3
 * `CINT(56789)` => overflow error

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

## POS
*Usage*: `POS <expression>`
Returns the horizontal position of the cursor.

The value returned is an integer up to the character width of the display.

Useful for word wrapping.

`expression` has no meaning; normally it is 0.

*Examples*:
 * `POS(0)`: Return the horizontal position of the cursor.

## SAVE
*Usage*: `SAVE [filename] <,A|,P>`
Save the current program to a file on disk. If you provide the same name as an existing file, the existing file will be overwritten.

*Examples*:
 * `SAVE "myprogram.n88"` Save the program as `myprogram.n88`
 * `SAVE "myprogram.n88",A` Save the program as `myprogram.n88` in raw ASCII format.
 * `SAVE "myprogram",P` Save the program as `myprogram` in an "encrypted binary format" (probably pre-tokenized/compiled?)
 * `SAVE "2:myprogram.n88"` Save the current program as `myprogram.n88` on the second floppy-disk drive.
