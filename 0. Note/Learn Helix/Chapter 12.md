---
tags:
  - note
Project:
  - "[[Learn Helix]]"
Status: In progress
---
# Entering match mode
m this mode is most useful for handling bracket pairs.
For example when you have a bracket selected you can press mm to jump to the next bracket.

# Selecting inside a set of brackets
mi \[ or \( or \) or \] will select the content within the brackets of that type. This is not inclusive of the brackets.
This can also be used for things like quotation marks.
ma is the inclusive equivalent.

# Adding brackets to a selection
ms( or ) adds brackets to your selection. 
Once again works for all brackets and quotation marks.

# Removing brackets
md( or )
See above.

# Replacing brackets
mr( or ) then the bracket you want.
See above.