---
title: N88 BASIC reference
---

# Commands
## BEEP
*Usage*: `BEEP <mode>`

It beeps.

*Examples*:
 * `BEEP`: Start beeping.
 * `BEEP 0`: Stop beeping.

## BLOAD
*Usage*: `BLOAD [filename] <load address> <,R>`
Load a machine-language program.

If load address is omitted, it will be loaded to the address specified when the binary was saved with `BSAVE`.

Append `R` to immediately run the program. If a load address is also specified, execution will begin from that address.

*Examples*:
 * `bload "2:test.bin",&he000` - Load `test.bin` from the secondary disk drive, storing it in memory starting at 0xE000.

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

## CLS
*Usage*: `CLS <mode>`
Clear the screen.

Modes:
 * 1: Clear text screen
 * 2: Clear graphics screen
 * 3: Clear both text and graphics screens

## DELETE
*Usage*: `DELETE [line number]`
Delete a line number from the current BASIC program.

*Examples*:
 * `DELETE 90`: Delete line 90.

## DSKF
*Usage*: `DSKF([drive number]<, parameter>)`
Get information on a floppy disk inserted into drive `drive number`. Note that drive numbers are 1-indexed.

Parameters you can extract are:
 * 0 - Maximum track number
 * 1 - Number of sectors per track
 * 2 - Single sided (0) or double-sided (1) floppy disk
 * 3 - Number of clusters per track
 * 4 - Number of clusters per floppy disk
 * 5 - Track index containing the directory info
 * 6 - Number of sectors per cluster
 * 7 - Start sector of FAT
 * 8 - Last sector of FAT
 * 9 - Number of FAT (?)
 * 10 - Sector index containing ID

*Examples*
 * `DSKF(1)` Get remaining capacity of the disk in drive 1.
 * `DSKF(2, 0)`

## FILES / LFILES
*Usage*: `FILES <disk number>`
List the files that are on disk

*Examples*:
 * `FILES` List the files on the primary floppy disk.
 * `FILES 2` List the files on the secondary floppy disk.
 * `LFILES` List the files in a linear display instead of columnar.

## KILL
*Usage*: `KILL [filename]`
Delete a file from disk.

*Examples*:
 * `KILL "2:data"` Erase the file named `data` on the second floppy disk.

## LOAD
*Usage*: `LOAD [filename] <,R>`
Load a program from disk.

*Examples*:
 * `LOAD "demo"` Load the `demo` program into RAM.
 * `LOAD "demo",r` Load and immediately run the `demo` program.
 * `LOAD "2:test.n88"` Load the `test.n88` program from the second floppy drive.

## LOC
*Usage*: `LOC [file handle]`
Get the current location in an open file.

*Examples*:
 * `LOC(2)` Get current location in file handle #2.

## LOCATE
*Usage*: `LOCATE [x] [y] <Enable Cursor?>`
Move the text cursor around the screen.

*Examples*:
 * `LOCATE 0, 0, 0` Move the cursor to the top left of the screen and disable cursor display.
 * `LOCATE 0, 10` Move the cursor to the left side of the 11th line from the top.

## LOF
*Usage*: `LOF [file handle]`
Get the size of a file.

*Examples*:
 * `LOF(2)` Get the size of file handle #2.

## MON
*Usage*: `MON`
Enter machine-language monitor mode.

Press CTRL+B to return to BASIC.

## NAME
*Usage*: `NAME [old file] AS [new file]`
Rename a file on disk.

*Examples*:
 * `NAME "sumple" as "sample"`

## NEW
*Usage*: `NEW`
Obliterate the current program and start from scratch.

## POS
*Usage*: `POS <expression>`
Returns the horizontal position of the cursor.

The value returned is an integer up to the character width of the display.

Useful for word wrapping.

`expression` has no meaning; normally it is 0.

*Examples*:
 * `POS(0)`: Return the horizontal position of the cursor.

## ROLL
*Usage*: `ROLL [number of pixels]`
Scroll the graphic screen upward by the pixel count.

*Examples*:
 * `ROLL 16`: Scroll upward by 16 pixels.

## SAVE
*Usage*: `SAVE [filename] <,A|,P>`
Save the current program to a file on disk. If you provide the same name as an existing file, the existing file will be overwritten.

*Examples*:
 * `SAVE "myprogram.n88"` Save the program as `myprogram.n88`
 * `SAVE "myprogram.n88",A` Save the program as `myprogram.n88` in raw ASCII format.
 * `SAVE "myprogram",P` Save the program as `myprogram` in an "encrypted binary format" (probably pre-tokenized/compiled?)
 * `SAVE "2:myprogram.n88"` Save the current program as `myprogram.n88` on the second floppy-disk drive.

## SEARCH
*Usage*: `SEARCH [array] <, start index> <,step>`
Find an item in an array, returning the index.

*Examples*:
 * `NUM = SEARCH(A%, 100, 0, 3)` - Search the `A%` array for the value 100, starting at index 0 and stepping 3 indices every time.
