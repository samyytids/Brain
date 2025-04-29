---
tags:
  - note
Project:
  - "[[Learn Helix]]"
Status: In progress
---
# Selecting to a character
These can search across multiple lines.

f\<ch> selects up to and including a character
- I am an Iexample
- fp
- I am an ==Iexamp==le
t\<ch> selects up to a character
- I am an Iexample
- tp
- I am an ==Iexam==ple
F and T do the same but backwards.

# Replacing selection
r\<ch> replaces all characters in the selection with another character.

# Repetition
. repeats the last insert mode command (say you type something, it'll type it again)
Alt + . repeats the last selection command