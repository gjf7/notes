# Vim

## Core
1. dot command: repeat last
2. `>G` increases the indentation from the current line until the end of the file.
3. DRY 例如给每行末尾加上分号
    - 短的话 dot command
    - 长 : | %normal 也可以先选好范围
    eg. :%normal i// 每行的光标位置都在行首
4. `*` search without Typing 
5. s - deletes the character under the cursor and then enters Insert mode.
6. repeat <-> reverse

| command | next | previous |
| --------------- | --------------- | --------------- |
|f / F{char}/t T{char}| ;  |  ,
|/pattern<CR>         | n  |  N
|?pattern<CR>         | n  |  N
|: s/targer/replacement| &  |  u
|qx{changes}q         | @x |  u

7. text objects

| sign   | 含义  |
|--------------- | --------------- |
| )          |           
| }          |           
| ]          |           
| >          |           
| '          |
| "          |
| `          |
| t          | A pair of <xml> tags
| -          |
| w          |
| s          | sentence
| p          | paragraph

8. Operator + Motion = Action

| Operator | Action |
| -------------- | --------------- |
|c  |               |
|d  |               |
|y  |               |
|g~ | Swap case     |
|gu/U | Make lowercase/uppercase
|>  |               |
|<  |               |
|=  | Autoindent    |
|!  |               |

9. zz - redraws the screen with the current line in the middle of the window, which allows us to read half a screen above and below the line we’re working on. 

## Insert Mode
1. `<C-r>`{register(yank 0, unnamed ")} - Paste from a Register Without Leaving Insert Mode
2. R - Replace mode gr -  treats the tab character as though it consisted of spaces. 
3. A <--> I
4.  `<C-w>` and `<C-u>` delete backward to the start of the previous word or to the start of the line

## Virtual Mode

| key | |
| -------------- | --------------- |
|v    |                               |
|V    |                               |
|`<C-v>`| block-wise                    | |gv   | reselect last visual selection|

1. o - Toggling the Free End of a Selection 换边
2. gUit - Prefer Operators to Visual Commands Where Possible
3. block-wise selection then `c` - Change Columns of Text
4. block-wise selection then edit- multi-cursor like style


## Ex command - best for line-oriented tasks
1. . - current line
2. $ - end of file
3. :copy co t
4. :move m
5. :normal
6. @: - repeat last ex command
7. `<C-d>` command asks Vim to reveal a list of possible completions


```js
var counter;
for (counter=1; counter <= 10; counter++) {
  // do something with counter
};
```
rename counter to aaa

1. /counter
2. `*`
3. :%s//`<C-r><C-w>`/g - Reuse the Last Search Pattern

- q/ - Open the command-line window with history of searches
- q: - Open the command-line window with history of Ex commands

:!ls - run commands in the shell

:h ex-cmd-inde
## Files
0. :h window-resize
1. :ls - listing of all the buffers that have been loaded into memory
2. `%` - which of the buffers is visible in the current window
3. `#` - alternate file 
4. <C-^> - toggle between the current and alternate files
5. bnext、bprev、bfirst、blast

6. :tabe[dit] {filename} - Open {filename} in a new tab
7. <C-w>T - Move the current window into its own tab
8. :tabc[lose] - Close the current tab page and all of its windows
9. :tabo[nly] - Keep the active tab page, closing all others

| Ex Command      |   Normal Command     |    Effect
|--------------- | -------------------- | ----------------------------------
|:tabn[ext] {N}  |   {N}gt              |    Switch to tab page number {N}
|:tabn[ext]      |   gt                 |    Switch to the next tab page
|:tabp[revious]  |   gT                 |    Switch to the previous tab page

10. :tabmove [N] - When [N] is 0, the current tab page is moved to the beginning,
               if we omit [N], the current tab page is moved to the end.

## Open Files and Save Them to Disk
1. :e  - Open a File by Its Filepath Using ‘:edit’
2. :find - Open a File by Its Filename 需要先配置 path， :set path+=src/**

## Getting around faster
1. g + motion for display line

|Command |Move Cursor  |
| -------------- | --------------- |
|j  |Down one real line
|gj |Down one display line
|k  |Up one real line
|gk |Up one display line
|0  |To first character of real line
|g0 |To first character of display line
|^  |To first nonblank character of real line
|g^ |To first nonblank character of display line $ To end of real line
|g$ |To end of display line

2. word vs WORD
3. Mark Your Place
   - m{a-zA-Z} uppercase for global marks
   - `{mark} moves the cursor to the exact position
   - `[ Start of last change or yank
   - `] End of last change or yank
   - `. Location of last change
4. `%` -  jump between opening and closing sets of parentheses
5. :jumps - Any command that changes the active file for the current window can be described as a jump.
6. gi  - If we leave Insert mode and then scroll around the document, we can quickly carry on where we left off by pressing `gi`
7. changelist  :changes g; g,

## Registers
1. P paste before cursor
2. default unnamed register `""`, yank's own register - `"0` 
3. swap two words
```text
I like fish and chips.

ww
de
mm
ww
ve
p
`m
P
```
4. "1 - 9 Most recent deleted or changed text
