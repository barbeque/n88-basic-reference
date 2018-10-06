# Commands
## SAVE
*Usage*: `SAVE [filename] <A|P>`
Save the current program to a file on disk. If you provide the same name as an existing file, the existing file will be overwritten.

*Examples*:
`SAVE "myprogram.n88"`
Save the program as `myprogram.n88`

`SAVE "myprogram.n88",A`
Save the program as `myprogram.n88` in raw ASCII format.

`SAVE "myprogram.n88",P`
Save the program as `myprogram.n88` in an "encrypted binary format" (probably pre-tokenized?)

`SAVE "2:myprogram.n88"`
Save the current program as `myprogram.n88` on the second floppy-disk drive.
