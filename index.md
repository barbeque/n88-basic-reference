---
title: N88 BASIC reference
---
This translation is a work in progress and does not contain all the commands possible in PC-88 BASICs.

# Structures
## Labels
A label provides a line reference that can be called by `GOTO` or `GOSUB` without having to manually track the line number and update it if it changes.

*Example*:
```
10 PRINT "HELLO"
20 GOSUB *WORLD
30 END
40 *WORLD: PRINT "WORLD"
50 RETURN
```

# Commands
## ASC
*Usage*: `ASC([char])`

Convert the first character of a string to the numeric ASCII index for it.

*Examples*:
 * `ASC("X")`: Produces 88 (ASCII 'X')
 * `ASC("Administrator")`: Produces 65 (ASCII 'A')

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

## CALL
*Usage*: `CALL [variable] (,argument 1) (,argument 2) ...`

Call a machine-language subroutine. The `variable` argument holds the address of the subroutine to execute from.

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

## CONSOLE
*Usage*: `CONSOLE [scroll start], [scroll number of lines], [display function keys], [colour/monochrome]`

Set modes for text screens.
 - By specifying the "scroll start" and "scroll number," you can define the scrolling area (scroll window) on the screen.
 - `CLS` and `PRINT CHR$(12)` work on this scroll window.
 - "Scroll start line" indicates the line from which to start scrolling.
 - If you pass `1` to "display function keys," the programmable function key help will appear on the bottommost line of the display. Passing `0` disables this feature.
 - Setting "colour/monochrome" to `1` applies colour text mode, and `0` is monochrome.

*Examples*:
 * `CONSOLE 0, 10, 1, 1`: Sets the first ten lines as a scroll area and disables function key display.
 * `CONSOLE , , , 1`: Leaves all other settings as they were and enables colour text expression.

## CONT
*Usage*: `CONT`

Resume execution from a `STOP` or `END` statement.

## CSNG
*Usage*: `CSNG([number])`

Convert a number to a single-precision float.

*Examples*:
 * `CSNG(123) => 123`
 * `CSNG(3.14159) => 3.14159`
 * `CSNG(-1E+40) => "Overflow" error`

## CSRLIN
*Usage*: `CSRLIN`

Return the screen row number that the cursor is on.

In 25-line mode, this will be 0-24.
In 20-line mode, this will be 0-19.

0 is the topmost row of the screen.

## DATE$
*Usage* `DATE$`

Variable containing the current date, in YY/MM/DD format.

*Examples*:
 * `DATE$ = "85/08/19"`: Set the computer's date to August 19, 1985.
 * `PRINT MID$(DATE$, 4, 2)`: Print the current month number.

## DEF FN
*Usage* `DEF FN[NAME][ARGUMENTS] = [BODY]`

Define a function.

*Examples*:
```
110 DEF FNDB(X)=X*2
120 PRINT "Twice 10 is";FNDB(10)
```

## DELETE
*Usage*: `DELETE [line number]`

Delete a line number from the current BASIC program.

*Examples*:
 * `DELETE 90`: Delete line 90.

## DIM
*Usage*: `DIM [NAME]([size0], [size ...])`

Define an array.

If the array described by `NAME` already exists, you will get a "duplicate definition" error. Use `ERASE` to remove the variable definition and then you can recreate it.

*Examples*:
 * `DIM MT(3,3,3)`: define a 3D array named MT with 3x3x3 dimensions.

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

## EXP
*Usage*: `EXP([number])`

Raise _e_ to the power specified.

*Examples*:
 * `EXP(3) => 20.0855`
 * `EXP(-12) => 6.14422E-06`
 * `EXP(100) => Overflow error`

## FILES / LFILES
*Usage*: `FILES <disk number>`

List the files that are on disk

*Examples*:
 * `FILES` List the files on the primary floppy disk.
 * `FILES 2` List the files on the secondary floppy disk.
 * `LFILES` List the files in a linear display instead of columnar.

## FIX
*Usage*: `FIX([decimal number])`

Convert a decimal number to an integer, _and floor it_.

*Examples*:
 * `A=1.5 FIX(A) => -1`

## FPOS
*Usage*: `FPOS([file handle])`

Get the current position in a file.

*Examples*:
```
110 OPEN "2:data" FOR OUTPUT AS #1
120 PRINT FPOS(1)
```

## FRE
*Usage*: `FRE([memory type])`

Get free available memory.

*Examples*:
 * `FRE(0)` - Get free variable space.
 * `FRE(1)` - Get free text space.
 * `FRE(2)` - Get free variable + text space.

## GET
*Usage*: `GET [file handle], [variable]`

Fetch a line from a file, refreshing any `FIELD` variables set previously.

*Examples*:
```
110 OPEN "2:address" AS #1
120 FIELD #1,30 AS A$,20 AS B$,50 AS C$
130 FOR I=1 TO LOF(1)
140	GET #1, I
150	PRINT "NAME",A$
160	PRINT "TEL",B$
170	PRINT "ADDRESS",C$
180 NEXT I
190 CLOSE:END
```

## GOSUB / RETURN
*Usage*: `GOSUB [line number or label]`, `RETURN <line number>`

Jump to a subroutine, or return from one.

RETURNing without GOSUB will throw an error.

*Examples*:
 * `GOSUB 1000`: Jump to the subroutine at line 1000.
 * `GOSUB *INVENTORY`: Jump to a subroutine following the label `*INVENTORY`.
 * `RETURN 100`: Return from the subroutine, and continue execution at line 100.

## GOTO
*Usage*: `GOTO [line number]`

Jump to a line number of the program.

*Examples*:
 * `GOTO 1000`

## HEX$
*Usage*: `HEX$([decimal value])`

Convert a decimal integer to hexadecimal.

*Examples*:
 * `HEX$(-32768) => "8000"`
 * `HEX$(65535) => "FFFF"`

## INKEY$
*Usage*: `INKEY$`

Get the currently held down key. Does not block. Returns empty string if no key is being held down.

*Examples*:
```
110 PRINT "Enter any key to end"
120 A$=INKEY$
130 IF A$="" THEN 110 ELSE END
```

## INP
*Usage*: `INP [I/O port address]`

Read data from an I/O port specified by the address

*Examples*:
 * `INP(&h02)`: Read from the keyboard port

## INPUT WAIT
*Usage*: `INPUT WAIT [time span], [prompt]<;variables>`

Put up an input prompt, but only wait a certain period of time before continuing.

Time span is in tenths of a second, so e.g. 50 is 5 seconds.

*Examples*:
 * `INPUT WAIT 100, "Your name";NA$` - Display "Your name" prompt, and wait 10 seconds. When a character string is entered, it goes into the variable `NA$`.

## INSTR
*Usage*: `INSTR(needle, haystack)`

Get the index of a substring inside a string. Returns 0 when not found, otherwise a 1-indexed character index of the start of the string.

*Examples*:
 * `INSTR("BISCUIT", "CHEESE") => 0`
 * `INSTR("COLUMNS III", "COLUMNS") => 1`

## INT
*Usage*: `INT([decimal number])`

Convert a decimal number to an integer, _with rounding_.

*Examples*:
 * `A=-1.5 INT(A) => -2`

## INP
*Usage*: `INP([port])`

Read data from the Z80 I/O port (0-255) specified by `port`.

*Examples*:
 * `INP(&h33)`: Read a byte from port 0x33.

## KILL
*Usage*: `KILL [filename]`

Delete a file from disk.

*Examples*:
 * `KILL "2:data"` Erase the file named `data` on the second floppy disk.

## LEN
*Usage*: `LEN([string])`

Get the length of a string or string variable.

*Examples*:
 * `LEN(HELLO$)`: Get the length of the `HELLO$` string variable.
 * `LEN("HI THERE")`: Get the length of the string "HI THERE" (8)

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

## OUT
*Usage*: `OUT [port], [data]`

Write `data` to the Z80 I/O port (0-255) specified by `port`.

*Examples*:
 * `OUT &h54, &h03`: Set port $54 (colour palette 0) to $03 (purple.)

## PAINT
*Usage*: `PAINT (Wx, Wy) <area colour> <border colour>`

Fill the last shape rendered with the provided colour.

*Examples*:
```
110 SCREEN 0,0:CLS 3
120 X=INT(RND*639):Y=INT(RND*199)
130 R=RND*50+1:C=RND*6+1
140 CIRCLE(X,Y),R,C
150 PAINT(X,Y),C
160 GOTO 120
```

Randomly draws filled circles on the screen.

## POS
*Usage*: `POS <expression>`

Returns the horizontal position of the cursor.

The value returned is an integer up to the character width of the display.

Useful for word wrapping.

`expression` has no meaning; normally it is 0.

*Examples*:
 * `POS(0)`: Return the horizontal position of the cursor.

## OUT
*Usage*: `OUT [I/O address] [value]`

Write a value to an I/O port specified by the address.

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

Find an item in an array, returning the index of the item found.

*Examples*:
 * `NUM = SEARCH(A%, 100, 0, 3)` - Search the `A%` array for the value 100, starting at index 0 and stepping 3 indices every time.

## SGN
*Usage* `SGN [number]`

Get the negative/positive sign of a number.

*Examples*:
 * `SGN(0.5) => 1`
 * `SGN(0) => 0`
 * `SGN(-0.5) => -1`

## SPC
*Usage*: `SPC [number]`

Print a certain number of spaces. Useful for aligning screen elements in text mode?

*Examples*:
 * `SPC(7) => _ _ _ _ _ _ _` (seven spaces)

## VAL
*Usage*: `VAL([string])`

Parses a string into a number variable.
