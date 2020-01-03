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
