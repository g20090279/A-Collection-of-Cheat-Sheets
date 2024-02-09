- Topics: Cheat Sheet for Vim Editor
- Last Revised: Feb. 07, 2024

## Insert Text

|Command|Action|
|:---|:---|
|`a`|Insert text on the right of cursor. "a" stands for *append*.|
|`i`|Insert text on the left of cursor. "i" stands for *insert*.|
|`A` (e.g., `Shift`+`a`)|Insert text at the end of the line.|
|`I` (e.g., `Shift`+`i`)|Insert text at the beginning of the line.|
|`o`|Insert a new line after the current line. "o" for *open* a new line.|
|`O` (e.g., `Shift`+`o`)|Insert a new line before the current line.|

## Delete Text

|Command|Action|
|:---|:---|
|`x`| Delete the character where the cursor is.|
|`<action>`+[`i`/`a`/`t`]+`<something>` pattern|Delete a word or delete to something (detail see below).|
|`d`+`w`|Delete everything at and after the cursor until the end of the word.|
||**Example**: `I want to de[l]ete this.` -> `I want to de[ ]this.` (Note: `[]` is the position of cursor.)
||**Example**: `I want to (de[l]ete) save this.` -> `I want to (de[)] save this.`|
|`c`+`w`|Same as `d`+`w`. Then enter insert mode.|
|`d`+`0`|Delete everything before the cursor at the same line.|
|`D` (e.g. `Shift`+`d`)|Delete everything after (including) the cursor at the same line.|
|`d`+`G`|Delete all lines after (including) the one where the cursor is.|
|`g`+`g`+`d`+`G`|Delete the whole file. `g`+`g` goes to the beginning of the file.|

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
|`d`+`i`+`w`|Delete the whole word but not the surrounding spaces. It means "delete inner word".|
|`d`+`a`+`w`|Delete the whole and the surrounding spaces. It means "delete around word".|
||**Example**: `I want to (de[l]ete) save this.` -> `I want to ([)] save this.`|
|`d`+`a`+`)`|Delete everything inside and including parentheses.|
||**Example**: `I want to (delete) save this.` -> `I want to [ ]save this.`|
|`d`+`t`+`<something>`|Delete everything from the cursor to one character before `<something>`.|

### Use *change* function

|Command|Action|
|:---|:---|
|`c`+`w`|Same as `d`+`w`. Then enter insert mode.|
|`c`+`i`+`w`|Same as `d`+`i`+`w`. Then enter insert mode.|
|`c`+`a`+`w`|Same as `d`+`a`+`w`. Then enter insert mode.|
|`c`+`t`+`<something>`|Same as `d`+`t`+`<something>`. Then enter insert mode.|

# Buffer

|Command|Action|
|:---|:---|
|`:edit </path/to/file>` or shortly `:e`|Open a file in the buffer and becomes active. This will fail if the change of the current buffer has been saved.|
|`:badd </path/to/file>` or shortly `:bd`|Open a file in the buffer at the backend without leaving the current buffer.| 
||Note: use `Ctrl`+`d` to view the directory and `Ctrl`+`l` to autocomplete the path and file name.|
|`:ls` or `:files` or `buffers`|List all the buffers. The meaning of flags can be found below.|
|`ball`|View all buffers by making n horizontal splits (where n is the number of files in buffer).|
|`:vertical ball`|Same as `ball` in a way of making n vertical splits.|
|`:bdelete <buffername>/<bufferindex>` or shortly `:bd`|Delete buffers by name or index.|
||**Example**: `:1,4bd` is to delete buffers 1,2,3, and 4.| 
|`:buffer` or shortly `b`|Switch from one buffer to another buffer. Note that ``tab` can be used to select different buffers.|
||**Example**: `:buffer <filename>` to switch to `<filename>`. `:b6` to switch to the buffer with index 6.|
|`:bnext` or shortly `:bn`|Swith to the nex buffer.|
|`:bprevious` or shortly `:bp`|Switch to the previous buffer.|
|`:bfirst` or `:b1`|Switch to the first buffer.|
|`:blast` or shortly `:bl`|Switch to the last buffer.|
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
