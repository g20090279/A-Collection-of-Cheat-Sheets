- Topics: Cheat Sheet for Vim Editor
- Last Revised: Jan. 31, 2024

## Insert Text

- (normal mode) `a`: insert text on the right of cursor. "a" stands for append.
- (normal mode) `i`: insert text on the left of cursor. "i"  stands for insert.
- (normal mode) `A` (e.g., `Shift`+`a`): insert text at the end of the line.
- (normal mode) `I` (e.g., `Shift`+`i`): insert text at the beginning of the line. 
- (normal mode) `o`: insert a new line after the current line. "o" for open a new line.
- (normal mode) `O` (e.g., `Shift`+`o`): insert a new line before the current line.

## Delete Text

- (normal mode) `x`: delete the character where the cursor is.

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

- `w`: delete the whole word without the spaces around it. `d`+`i`+`w`: delete the whole word. `c`+`i`+`w`: delete the whole word and enter the insert mode.
- Delimiters such as parenthesis `(` or `)`, square bracket `[` or `]`, curly brace `{` or `}`, quote `"`, etc.

### Use *delete* function
- (normal mode) `d`+`w`: delete everything at and after the cursor until the end of the word. 
  
  **Example**: I want to de[l]ete this. -> I want to de[ ]this. (Note: [] is the position of cursor.)

  **Example**: I want to (de[l]ete) save this. -> I want to (de[)] save this.
  
- (normal mode) `d`+`i`+`w`: delete the whole word but not the spaces around it. It means "delete inner word".

  **Example**: I want to de[l]ete this. -> I want to [ ]this.

- (normal mode) `d`+`a`+`w`: delete the whole and the spaces around it. It means "delete around word".

  **Example**: I want to (de[l]ete) save this. -> I want to ([)] save this.

- (normal mode) `d`+`a`+`)`: delete everything inside and including parentheses.

  **Example**: I want to (delete) save this. -> I want to [ ]save this.

- (normal mode) `d`+`t`+`<something>`: delete everything from the cursor to one character before `<something>`.

### Use *change* function
- (normal mode) `c`+`w`: same as `d`+`w`. Then enter insert mode.
- (normal mode) `c`+`i`+`w`: same as `d`+`i`+`w`. Then enter insert mode.
- (normal mode) `c`+`a`+`w`: same as `d`+`a`+`w`. Then enter insert mode.
- (normal mode) `c`+`t`+`<something>`: same as `d`+`t`+`<something>`. Then enter insert mode. 
