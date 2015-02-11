# XQuartz (X11)

#### Enable pasting

To enable pasting in XQuartz (X11) by pressing `Command + v`, just add this line in the file ~/.Xdefault:

```
*VT100.translations: #override  Meta <KeyPress> V:  insert-selection(PRIMARY, CUT_BUFFER0) \n
```
