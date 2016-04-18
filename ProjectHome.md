This project is dedicated to porting the GCC (and some other GNU tools) to the iPhone/iTouch

We would like to thank the guys at http://iphone-dev.googlecode.com.  Without them, this port would have never happened. To compile your own copy of iphone-GCC you will need a cross compiler from here

### FW v2 is currently not supported, Sorry. ###

# Help is required in designing the GUI, if you want to help email david.m.thornton #

## We cannot post the header files here as it is illegal ##

### Details about the port ###

| **Processor**        | arm    |
|:---------------------|:-------|
| **Vendor**           | apple  |
| **iPhone/iTouch OS** | darwin |


## Bugs Worth Noting ##

  * On very rare occasions, the llvm gives an internal compiler error
  * The memory consumption for c++ sources is very big; this may cause a crash