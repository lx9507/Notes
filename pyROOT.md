# PyROOT

#### About the conflicting python installations which can cause crash in import ROOT in anaconda python

Everything I have read suggests this is due to conflicting python installations.  So following some other threads, I do the following
```bash
otool -L /Users/walkloud/install/root/lib/libPyROOT.so 
/Users/walkloud/install/root/lib/libPyROOT.so:
    @rpath/libPyROOT.so (compatibility version 0.0.0, current version 0.0.0)
    /usr/lib/libSystem.B.dylib (compatibility version 1.0.0, current version 1197.1.1)
    @rpath/libRIO.so (compatibility version 0.0.0, current version 0.0.0)
    @rpath/libTree.so (compatibility version 0.0.0, current version 0.0.0)
    @rpath/libCore.so (compatibility version 0.0.0, current version 0.0.0)
    @rpath/libCint.so (compatibility version 0.0.0, current version 0.0.0)
    libpython2.7.dylib (compatibility version 2.7.0, current version 2.7.0)
    /usr/lib/libc++.1.dylib (compatibility version 1.0.0, current version 120.0.0)
```

The second to last line is the culprit - this lib should be pointing to the anaconda python lib, but it is actually catching the /System python lib...  So then I use install_name_tool to fix the path of this lib
```bash
install_name_tool -change libpython2.7.dylib /Users/walkloud/install/anaconda/lib/libpython2.7.dylib libPyROOT.so
```
and then the above ROOT import works and I can interact as described via the pyroot docs, at least the minimal testing.

From [googlegroups](https://groups.google.com/a/continuum.io/forum/#!msg/anaconda/8kSroSuKpBQ/qENxLsRxLcwJ).
