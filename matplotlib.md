# Matplotlib Error

## About the incompatability of differernt versions of libpng from python

Matplotlib is built depending on the libpng of X11, which is usually different from that of the system, used by Python.
This may cause a bug in IPython notebook when using “%matplotlib inline” to plot a image inline.
The solution is to build matplotlib avoiding the libpng of X11, just using that of the system.
Here is a very simple way without modifying the environment variables:


```bash
sudo pip uninstall matplotlib
cd /opt/X11/include/libpng15
sudo mv png.h _png.h
sudo mv pngconf.h _pngconf.h
sudo mv pnglibconf.h _pnglibconf.h
sudo pip install matplotlib
sudo mv _png.h png.h
sudo mv _pngconf.h pngconf.h
sudo mv _pnglibconf.h pnglibconf.h
```
