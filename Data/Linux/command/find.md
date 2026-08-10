---
status: start
Recall: None
source:
---

 #linuxCLI #documentation

---
# What does man do

Show man page in [[less]] (content displayer)

# What does man **NOT** do

Show shell built-in. For that, use [[help]] 

---
# How to read man page

## Visual cues

|             Cue              |                       Meaning                        |
| :--------------------------: | :--------------------------------------------------: |
|           **Bold**           |        Type exactly as shown, case sensitive.        |
| *Italic* or <u>Underline</u> |                Replace with argument                 |
|            [-arg]            |                       Optional                       |
|          \| (pipe)           |                    Choose between                    |
|             ...              |                Command is repeatable                 |
|          -arg=value          | give value, usually to option, with or without space |
## Options

can come in full or shorten form
	-w, --width=<u>COLS</u>

> [!warning]
> 
> Be careful for the section
> 
> **Why**: The same name can refer to different things, and therefore can have multiple man-page sections.
> **Keep in mind** : Is this the right section?
> **Do** : use **man -k** to search for man page, then read description
