# enbParmLinks
A enbplugin for SkyrimLE enb that provides linkage between enb variables or system values and address.
___

# Installation
Put enbParmLink.enbplugin under `/enbseries` in your SkyrimLE base directory.

# Setup
All linkage is defined through `enbParmLink.cfg` located in `/enbseries`, under 3 sections `[INIT]`, `[READ]` and `[SYNC]`.
```ini
; Expression on the right hand side will be assigned to the left hand side.
[READ]
; Assign value from one ENB UI entry to another.
EFFECT.TXT:"target parm" = ENBEFFECT.FX:"source parm"


; Any changes from either sides will sync to the counter part
[SYNC]
; Sync the value between a float in the memory and a ENB entry.
ENBDEPTHOFFIELD.FX:"sync fov" = FLOAT:0x01B39A4C


; Values are set upon ENB reset, load or saves.
[INIT] 
; to assign simple value to target
FLOAT:0x01B39A4C = 70
```
To assign a calculated value, use keyword `EXPR:`
```
EFFECT.TXT:"calculated value" = EXPR:" (a0*2 + a1) ", EFFECT.TXT:"val", EFFECT.TXT:"useCalc"
```
where variable are listed after the EXPR expression in sequential order from a0 - a19, separated by commas.

Additionally, multiline expressions or linking to same key is also avalible.
```ini
; linking to same variable
EFFECT.TXT:"VALUE" = EXPR:"conditional(1, (a0 == 0) || ( a0 == 2 ) || (a0 == 4) )", EFFECT.TXT:"raw"
EFFECT.TXT:"VALUE" = EXPR:"conditional(2, (a0 == 0x01) || ( a0 == 0x03 ) || (a0 == 0x05) )", EFFECT.TXT:"raw"


; multi-line are enclosed by <<<LINES & LINES pairs
EFFECT.TXT:"focal length" = <<<LINES
    EXPR:" conditional( 18 /tan(_pi/360 * a0), a0 && (a1 == 0) ) ", 
    FLOAT:0x01B39A4C , EFFECT.TXT:"calc fov"
LINES
```

# Syntax
## Read-Only expressions:
___
### `SYSTEM:<SYSVALS>`

+ **SYSVALS**

   avaliable values:
   + **ENBVERSION**
   
      ENB binary version.
   + **MOUSE_X**
   + **MOUSE_Y**

      Cursor position on XY coordinate in pixels relative to upper left corner of game window.
   + <strong>KEY_HOLD_*</strong>
   + <strong>KEY_PRESS_*</strong>
   + <strong>KEY_TOGGLE_*</strong>

      Keyboard input states. Replace asterisks with VK keycode of target key.


### `EXPR:<EXPR_STRING>, <EXPRESSION>,...`
+ **EXPR_STRING**

   Arithmetic expression enclosed by "".
+ **EXPRESSION**

   A expresion linked to the variables denoted by a0, a1... in the EXPR_STRING. 
   Seperate multiple expressions by "," when more then one variables are used.
   
+ **Remarks:**

   + Numeric operators: `+`, `-`, `*`, `/`, `^`, `%`
   + Logical operators: `&&`, `||`, `==`, `!=`, `>`, `<`, `>=`, `<=`, `?:`*(ternary operator)*
   + Intrinsic functions: `sin()`, `cos()`, `tan()`, `atan2(x,y)`, `asin()`, `acos()`, `atan()`, `sinh()`, `cosh()`, `tanh()`, `asinh()`, `acosh()`, `atanh()`, `log2()`, `log10()`, `ln()`, `exp()`, `sqrt()`, `abs()`, `sign()`, `rint()`*(round)*, `min(x,y)`, `max(x,y)`, `clamp(x, min, max)`, `saturate(x)`, `lerp(x,y,w)`, `pow(x,y)`
   + Special functions: 
        `conditional( value, cond)` Only sets the value when the condition is true.
   
### `<CONSTANT>`
+ **CONSTANT**

   Numeric Constant. example usage `FLOAT:0x01B39A4C = 70`


## Read-Writes expressions:
___
### `<SECTION_NAME>:<ENBPARM_UINAME>`
+ **SECTION_NAME**

   Section names listed by enb UI. For example, ENBBLOOM.FX, COLORCORRECTION, .etc
+ **ENBPARAM_UINAME**

   Parameter name listed in .fx parm annotation UIName, or name listed in enbUI.
+ **example:** `ENFEFFECT.FX:"my Awsome Variable"`
 
### `<TYPE>:<ADDRESS>+<OFFSET>+...`
+ **TYPE**

   Variable type of this address. Possible values are `INT`, `FLOAT`, `BOOL`.
+ **ADDRESS**

   The memory address of the variable.
+ **OFFSET**

   The memory offsets to apply if base address need to be dereferenced. 
 + **example:** `FLOAT:0x012E56A0+0x20`

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
