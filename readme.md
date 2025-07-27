# fm
## Introduction
fm is a console file manager, optimized for usage with screen readers such as [tdsr](https://github.com/tspivey/tdsr).
## Requirements
* Python 3
* The send2trash module, which should be available in your distribution as python3-send2trash or python-send2trash
## Usage
To start fm, just run it. By default it will start up in the current directory, and read the name of the first file there.
Arrow keys will move through the list, Enter opens things.
The cursor will be on the first character of the filename each time a new one is displayed.
If the name is too long to fit on one line, it will be truncated, and a $ will be shown at the end.
Press space to have the entire name displayed. After you do this, your cursor will be on the last line of the name.

## Configuration file
The configuration file is located at `~/.config/fm/config`.
An example is included in `example.cfg`.

## Searching
IF you have a long list of files, you might want to search for something specific.
To do this, press / (slash), and type a search query, then press enter.
Once you do this, fm will search through the list of files from the file after the cursor to the end, and stop at the first result.
If nothing is found, it will say "Not found".

The queries use Python's `fnmatch` module, case insensitively. Examples:
* `*.txt`
* `*test*`

To search for the next item in the list which matches the previously-entered query, press n. Capital N will search for the previous one.

## Deleting files
To delete a file, press `d`. This will put it in the trash, which is compatible with GUI file managers such as PCManFM.
To permanently delete a file, press D (capital D).

The trash-cli package is needed for dealing with the trash.
Use `trash-list` to list it, `trash-restore` to restore something from it and `trash-empty` to empty it.

## Keys
* Up arrow - move to the previous file.
* Down arrow -  move to the next file.
* Space - Display the entire filename.
* . (period) - go to the parent directory.
* g - prompt for a directory to go to, and go there.
* Enter - open file with the opener.
* d - send the currently selected file to trash.
* Shift d - permanently delete the selected file.
* s - display the size of the currently selected file.
* / (slash) - Prompt for a search query, and start searching down the list for it.
* n - search next
* N - search previous
* ! (exclamation point) - start $SHELL in the current directory.
* Control-T - open a new tab.
* Control-W - Close the current tab.
* 1 through 0 - switch tabs.
* m - move file.
* c - copy file.
* e - edit file
* t - show modification time of file.

## Known bugs
* The s command calls du to print the size of the currently selected item. Because du outputs a final newline which causes an unwanted blank line before the cursor,
the top half of the terminal is scrolled up, resulting in a blank line at the top.
