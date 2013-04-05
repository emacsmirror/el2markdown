# el2markdown - Convert commentary section of elisp files to markdown

*Author:* Anders Lindgren<br>
*Version:* 0.0.0<br>

This package converts *Commentary* section in Emacs Lisp modules to
text files in MarkDown format, a format supporting headings, code
blocks, basic text styles, bullet lists etc.

The MarkDown is used by many web sites as an alternative to plain
texts. For example, it is used by sites like StackOverflow and
GitHub.

## What is converted

Everything between the `Commentary:` and `Code:` markers are
included in the generated text. In addition, the title and *some*
metadata are also included.

## How to write comments

The general rule of thumb is that the Emacs Lisp module should be
written using plain text, as they always have been written.

However, some things are recognized. A single line ending with a
colon is cosidered a *heading*. If this line is at the start of a
comment block, it is considered a main (level 2) heading. Otherwise
it is considered a (level 3) subheading.

### Use Markdown formatting

It is possible to use markdown syntax in the text, like *this*, and
**this**.

### Special formats

* Code blocks using either the Markdown convention by indenting the
  block with four extra spaces, or by starting a paragraph with a
  `(`.
* In elisp comments, a reference to `code` (backquote - quote),
  they will be converted to MarkDown style (backquote - backquote).
* In elisp comments, bullets in lists are typically separated by
  empty lines. In the converted text, the empty lines are removed,
  as required by MarkDown.


## Example

    ;; This is a heading:
    ;;
    ;; Bla bla bla ...

    ;; This is another heading:
    ;;
    ;; This is a pararaph!
    ;;
    ;; A subheading:
    ;;
    ;; Another paragraph...
    ;;
    ;; * A bullet in a list
    ;;
    ;; * Another bullet.

## Installation

Place this package somewhere in Emacs `load-path` and add the
following lines to a suitable init file:

    (autoload 'el2markdown-view-buffer  nil t)
    (autoload 'el2markdown-write-file   nil t)
    (autoload 'el2markdown-write-readme nil t)

## Usage

To generate the markdown representation of the current buffer to a
temporary buffer, use:

    M-x el2markdown-view-buffer RET

To write the markdown representation of the current buffer to a
file, use:

    M-x el2markdown-write-file RET name-of-file RET

In sites like GitHub, if a file named README.md exists in the root
directory of an archive, it is displayed when viewing the archive.
To generate a README.md file, in the same directory as the current
buffer, use:

    M-x el2markdown-write-readme RET

### Batch mode

You can run el2markdown in batch mode. The function
`el2markdown-write-readme` can be called directly using the `-f`
option. The others can be accessed with the `--eval` form.

For example,

    emacs -batch -l el2markdown.el my-file.el -f el2markdown-write-readme



---
Converted from `el2markdown.el` by *el2markup*.