
## Project top level 
1. src
     - mainapp -> Main.c
     - disp  -> display.c
2. inc
     - disp  -> display.h

## src (Directory)  
- lib1
- lib2
- lib3
- mainapp

## Cmake :
- CMakeLists.txt inside the source tree
### contents :
- commands to define project,add source,includes and executable

- projects(<project name>) #optional
- set(<src_variable_name><src1><src2><src3>....)#mandatory
- Include_directories(
             inc_dir1/
             inc_dir2/
             .
             .)
- Add_executable(<targest name/output file name>${src_variable_name})
 
- create a bulid directory out of souce tree
- Enter inside the build directory and execute :
- Cmake<path/to/source/tree>
- Cmake scans the contents of CMakeLists.txt to generate Makefile based on the source tree
 
- .a = static library file ,it doesnot have main function.
- Libraries name always start with lib.
### If we have sorce code,how to generate sorce code?
Main.c display.c display.c

gcc main.c display.c

Libdisplay.a lib display.a

gcc main.c-L/path/to/library-ldisplay

- -L is used to provide the path of library.
- . -> current working directory.
- l -> link the library.

Compile the file only till the object generation.
  gcc -c display.c  ->  display.o
For converting display.o to display.a
   ar -rc <libraryname.a> <objectfile.o>
   ar -> command
   Ex : ar -rc libdisplay.a display.o 

#### display.h :
```c
#ifndef _DISPLAY_H
#define _DISPLAY_H

void display(char *buffer);

#endif
```
#### main.c :
```c
#include<stdio.h>
#include "display.h"

void main(){
        display("Hello world\n");
}
```
#### display.c :
```c
#include<stdio.h>

void display(char *buffer){
        printf("%s\n",buffer);
}
```
gcc -c display.c  -> display.o
ar -rc libdisplay.a display.o  -> libdisplay.a
gcc main.c -L. -l display  -> a.out


