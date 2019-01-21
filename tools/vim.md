VIM
===

## General
Use `.` to repeat the last action.

## Tabs
In the terminal, use `vim -p` and one or multiple file to open them in tabs (also works with e.g. `vim -p *.cpp`) 
Open a file in a new tab with `:tabe {file}`
Navigate between tabs with the `tabn` and `tabp` commands. 
Navigate between tabs with `gT` in normal mode. Using `{i}gT` moves to the i-th tab.

## Editing and Navigating
Use `o` (`O`) to insert a newline after (before) the current one and put the cursor at its start.

## Editing

Use `ci` or `ca` to change section, coupled with key such as `w` (for word), `(` (for parenthesis), `"` (for quotes).

## Navigating
Use `<Ctrl-f>` (`<Ctrl-b>`) to move forward (backward) a screen in the current file.
Use `<Ctrl-u>` (`<Ctrl-d>`) to mode forward (backward) half a screen in the current file.
Use `{` (`}`) to move backward (forward) a paragraph.
Use `H` `M` `L` to navigate respectively to the top, middle, or bottom of the screen (excluding non-line part of the screen).

## Selection
In visual mode:

Use `aw` (`ap`) to select the word (paragraph) from the cursor position up to the next word (paragraph).
Use `iw` (`ip`) to select the word (paragraph) the cursor is on.


