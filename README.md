# enbParmLinks
A enbplugin for SkyrimLE enb that provides linkage between enb variables or system values and address.
___

# Installation
Put enbParmLink.enbplugin under /enbseries in your SkyrimLE base directory.

# Setup
All linkage is defined through enbParmLink.cfg located in /enbseries, with 2 section [READ] and [SYNC].
```ini
[READ]
EFFECT.TXT:"target parm" = ENBEFFECT.FX:"source parm"
[SYNC]
ENBDEPTHOFFIELD.FX:"sync fov" = FLOAT:0x01B39A4C
```
where in the [Read] section, the expression on the right hand side will be assigned to the left hand side.

while in the [SYNC] section, any changes from either sides will sync to the counter part.

# Syntax
## Read-Only expressions:
___
`SYSTEM:<SYSVALS>`

+ SYSVALS

   avaliable values:
   + MOUSE_X
   + MOUSE_Y

      Cursor position on XY coordinate in pixels relative to upper left corner of game window.
   + KEY_HOLD_*
   + KEY_PRESS_*
   + KEY_TOGGLE_*

      Keyboard input states. Replace asterisks with VK keycode of target key.


`EXPR:<EXPR_STRING>, <EXPRESSION>,...`
+ EXPR_STRING

   Arithmetic expression enclosed by "".
+ EXPRESSION

   A expresion linked to the variables denoted by a0, a1... in the EXPR_STRING. 
   Seperate multiple expressions by "," when more then one variables are used.
   
Remarks:

   Avaliable operators are: 

## Read-Writes expressions:
___
`<SECTION_NAME>:<ENBPARM_UINAME>`
+ SECTION_NAME

   Section names listed by enb UI. For example, ENBBLOOM.FX, COLORCORRECTION, .etc
+ ENBPARAM_UINAME

   Parameter name listed in .fx parm annotation UIName, or name listed in enbUI.
   
`<TYPE>:<ADDRESS>+<OFFSET>+...`

# Licence

This software is using following projects with respective licences:
___
  [muParserSSE](https://github.com/beltoforion/muparsersse) Copyright (C) 2011 Ingo Berg
  
  [simpleini](https://github.com/brofield/simpleini) Copyright (c) 2006-2013 Brodie Thiesfield
  
  with MIT Licence:
  ```
  Permission is hereby granted, free of charge, to any person obtaining a copy of this 
  software and associated documentation files (the "Software"), to deal in the Software
  without restriction, including without limitation the rights to use, copy, modify, 
  merge, publish, distribute, sublicense, and/or sell copies of the Software, and to 
  permit persons to whom the Software is furnished to do so, subject to the following conditions:

  The above copyright notice and this permission notice shall be included in all copies or 
  substantial portions of the Software.

  THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT
  NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND 
  NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, 
  DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, 
  OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE. 
  OR OTHER DEALINGS IN THE SOFTWARE.
  ```
