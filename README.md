# RTSResearch
Using Composite for RTS
Composite repo https://github.com/gwsystems/composite

Info on composite https://composite.seas.gwu.edu/

1. Building composite
Running into issues on 64bit Ubuntu
Issue 1: make init threw errors saying that assembly instructions included in a header file is not 64bit compatible. The linker was using 64bit libraries. Crawling through the spaghetti of makefiles, found src/components/lib/ps/Makefile.inc that was missing the -m32 option for gcc. Was a shot in the dark, but make init worked.
Issue 2: make threw and error saying -r and -pie are not compatible. Found the makefile that was using -r (xlinker) to pass options. Mad googling showed me that my gcc has -pie (position independent executable) enabled by default. Two options - try to reconfigure gcc without pie (not sure what will break). Or find every instance of CFLAGS in composite makefile and add -no-pie. 
