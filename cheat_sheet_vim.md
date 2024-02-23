- Topics: Cheat Sheet for Vim Editor
- Last Revised: Feb. 21, 2024

---

- Note 1: Square bracket pair `[]` embraces possible options separated by `/`. For example, "`Ctrl`+[`E`/`Y`] | Move the screen one line up/down" tells that you can move the screen one line up by `Ctrl`+`E`, and one line down by `Ctrl`+`Y`.

# View Files

|Command|Action|
|:---|:---|
|`h`/`j`/`k`/`l` or `arrow left`/`down`/`up`/`right`|Cursor moves *left*/*down*/*up*/*right*.|
|`Ctrl`+[`E`/`Y`]|Move the screen one line *up*/*down*.|
|`Ctrl`+[`f`/`b`]|Move the screen a page *down*/*up*. `f` stands for *forward*. `b` stands for *backward*.|
|`Ctrl`+[`d`/`u`]|Move the screen a half screen down / up. `d` stands for *down*. `u` stands for *up*.|
|`z`[`z`/`t`/`b`]|Move the current line to the *middle*/*top*/*bottom* of the screen.|

# Modify Files

## From Normal Mode to Insert Mode

|Command|Action|
|:---|:---|
|`a`|Insert text on the right of cursor. "a" stands for *append*.|
|`i`|Insert text on the left of cursor. "i" stands for *insert*.|
|`A` (e.g., `Shift`+`a`)|Insert text at the end of the line.|
|`I` (e.g., `Shift`+`i`)|Insert text at the beginning of the line.|
|`o`|Insert a new line after the current line. "o" for *open* a new line.|
|`O` (e.g., `Shift`+`o`)|Insert a new line before the current line.|

## Switch Case of Characters

You can use (1) visual mode or (2) starting with `g` and ending with `<motion>` (left/up/down/right) to select text.

|Normal Mode|Visual Mode|Action|
|:---|:---|:---|
|`~` or `g~` then `<motion>`|`v` then `~`|Toggle case of the current character.|
|`3~`|`v` then select 3 character after then `~`|Toggle case of the next 3 characters.|
|`g~iw`|`v` then `iw` then `~`|Toggle case of the current word.|
|`g~$`|`v` then `$` then `~`|Toggle case of all character to the end of the current line.|
|`g~~`|`V` then `~`|Toggle case of the current line.|
|`gU` then `<motion>`|`v` then `U`|Make the current character uppercase.|
|`gUU`|`V` then `U`|Change the current line to uppercase.|
|`gUiW`|`v` then `iw` then `U`|Change THE current word to uppercase.|
|`gu` then `<motion>`|`v` then `u`|Make the current character lowercase.|

More use case

- Make title line (make every first letter of a word uppercase): `:s/\v<(.)(\w*)/\u\1\L\2/g`

## Delete Text

|Command|Action|
|:---|:---|
|`x`| Delete the character where the cursor is.|
|`<action>`+[`i`/`a`/`t`]+`<something>` pattern|Delete a word or delete to something (detail see below).|
|`dw`|Delete everything at and after the cursor until the end of the word (*with* the following spaces).|
|`de`|Delete everything at and after the cursor until the end of the word (*without* the following spaces). `e` stands for 'end'.|
||**Example**: `I want to de[l]ete this.` -> `I want to de[ ]this.` (Note: `[]` is the position of cursor.)
||**Example**: `I want to (de[l]ete) save this.` -> `I want to (de[)] save this.`|
|`cw`|Same as `d`+`w`. Then enter insert mode.|
|`d0`|Delete everything before the cursor at the same line.|
|`D` (e.g. `Shift`+`d`)|Delete everything after (including) the cursor at the same line.|
|`dG`|Delete all lines after (including) the one where the cursor is.|
|`ggdG`|Delete the whole file. `g`+`g` goes to the beginning of the file.|

### Overall Command Pattern

- `<action>`+`i`+`<something>`
- `<action>`+`a`+`<something>`
- `<action>`+`t`+`<something>`

The `<action>` can be `d` (*delete*) or `c` (*change*):

- `d`: delete something and stay in the normal mode.
- `c`: delete something and go to insert mode.

`i` (*inner*), `a` (*around*) or `t` (*to*):
- `i`: affect only the word itself without any spaces and delimiters around it.
- `a`: affect both word and the spaces or delimiters around it.
- `t`: affect those beginning from the cursor bis the one before the specified character.

The `<something>` can be `w` (*word*) or delimiters:

- `w`: delete the whole word without the surrounding spaces. `d`+`i`+`w`: delete the whole word. `c`+`i`+`w`: delete the whole word and enter the insert mode.
- Delimiters such as parenthesis `(` or `)`, square bracket `[` or `]`, curly brace `{` or `}`, quote `"`, etc.

### Use *delete* function

|Command|Action|
|:---|:---|
|`diw`|Delete the whole word but not the surrounding spaces. It means "delete inner word".|
|`daw`|Delete the whole and the surrounding spaces. It means "delete around word".|
||**Example**: `I want to (de[l]ete) save this.` -> `I want to ([)] save this.`|
|`da)`|Delete everything inside and including parentheses.|
||**Example**: `I want to (delete) save this.` -> `I want to [ ]save this.`|
|`dt<something>`|Delete everything from the cursor to one character before `<something>`.|

### Use *change* function

("Change" means delete and then enter to insert mode.)

|Command|Action|
|:---|:---|
|`cw`|Same as `dw`. Then enter insert mode.|
|`ciw`|Same as `diw`. Then enter insert mode.|
|`caw`|Same as `daw`. Then enter insert mode.|
|`ct<something>`|Same as `dt<something>`. Then enter insert mode.|
|`cc`|Change entire line.|
|`c$` or `C`|Change to the end of the line.|

# Search and Replace


# Buffer

|Command|Action|
|:---|:---|
|`:edit </path/to/file>` or `:e`|Open a file in the buffer and becomes active. This will fail if the change of the current buffer has been saved.|
|`:badd </path/to/file>` or `:bd`|Open a file in the buffer at the backend without leaving the current buffer.| 
||Note: use `Ctrl`+`d` to view the directory and `Ctrl`+`l` to autocomplete the path and file name.|
|`:ls` or `:files` or `buffers`|List all the buffers. The meaning of flags can be found below.|
|`ball`|View all buffers by making n horizontal splits (where n is the number of files in buffer).|
|`:vertical ball`|Same as `ball` in a way of making n vertical splits.|
|`:bdelete <buffername>/<bufferindex>` or `:bd`|Delete buffers by name or index.|
||**Example**: `:1,4bd` is to delete buffers 1,2,3, and 4.| 
|`:buffer` or `b`|Switch from one buffer to another buffer. Note that ``tab` can be used to select different buffers.|
||**Example**: `:buffer <filename>` to switch to `<filename>`. `:b6` to switch to the buffer with index 6.|
|`:bnext` or `:bn`|Swith to the nex buffer.|
|`:bprevious` or `:bp`|Switch to the previous buffer.|
|`:bfirst` or `:b1`|Switch to the first buffer.|
|`:blast` or `:bl`|Switch to the last buffer.|
|`:set hidden`|Disable the message for discarding or saving changes when leaving the active buffer with unsaved change. To set it default, add `set hidden` in the vimrc file.|

**The flags in the list of buffers show some information**
- `%`: Buffer which is the current window.
- `#`: Alternate buffer (the last file which was most recently edited in the current window)
- `a`: Active buffer (the file which is being edited in the current window).
- `h`: Hidden buffer (buffer with unsaved modifications but is not being displayed in any window).
- `u`: Unlisted buffer (files that are not open in Vim but are present in the current working directory; use `:ls!` to view this).
- `-`: Buffer with 'modifiable' set to off.
- `=`: A read-only buffer.
- `+`: A modified buffer (buffer with changes that are not written to disk).
- `X`: A buffer that has read errors.

# Split Windows

|Command|Action|
|:---|:---|
|`:split` or `sp` or `Ctrl`+`w` then `s`|Split a window horizontally. `w` stands for window.|
|`:vsplit` or `vs` or `Ctrl`+`w` then `v`|Split a window vertically.|
|`:q` or `Ctrl`+`w` then `q`|Close the current window and buffer.|
|`:on`|Close all other windows except the current one.|
|`Ctrl`+`w` then `h`/`j`/`k`/`l`|Navigate the split windows left/down/up/right.|
|`Ctrl`+`w` then `w`|Switch focus between the split buffers.|
|`Ctrl`+`w` then `x`|Swap the position of the currently focused buffer with an inactive one.|

# Others
- `:help magic`: show documentation of four different magic mode in regular expression.
- `:ter[minal]`: open a terminal window.
- `:sav[eas] file`: save file as
- `K`: open man page for word under the cursor.
