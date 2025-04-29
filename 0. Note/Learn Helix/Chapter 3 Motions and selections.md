---
tags:
  - note
Project:
  - "[[Learn Helix]]"
Status: In progress
---
# Selecting words
All of the below have a CAPS alternative.
The caps versions are space delimitted only while the lower ones are delimited by things like quotes and dashes.

w will select the next word
- I am an example
- ==I== am an example
- I ==am== an example

e will move you to the end of the current word
- I am an exIample
- I am an ex==Iample==

b will move you to the beginning of the current word
- I am an exIample
- I am an ==ex==Iample

# Change mode
c allows you to change the current selection
Which basically makes it a combined di. 
So it will delete and enter insert mode.

# Counts with motions
By prepending a motion with a number you can repeat that motion N times.
- I am an exampleI
- 3b
- I ==am an exampleI==

# Select/extend mode
v lets you select stuff and pressing it again let's you leave select mode and return to normal mode.

This can be used in conjunction with motions to quickly highlight text
- I am an example
- v2w
- ==I am== an example

# Selecting a whole line
x selects entire lines, when used on a blank line it will select the line underneath as well.
X selects entire lines, when used on a blank line it will do nothing.

# Deselecting
; deselects you current highlight

