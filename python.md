# Python skills

## printf

Python's % operator hearkens to printf's syntax when interpolating the contents of a tuple. This operator can, for example, be used with the print function:

```python
print("%s\t%s" % (foo,bar))
```

Version 2.6 of Python added the more versatile str.format() method:

```python
print("If you multiply five and six you get {0}.".format(5*6))
```

It's easy to create a C language-like printf() function in either Python 2.x or 3.x:

```python
import sys
def printf(format, *args):
    sys.stdout.write(format % args)

printf("%d x %d is %d\n", 6, 7, 6*7)
```
