


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

main.c display.c display.c

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

### display.h :
```c
#ifndef _DISPLAY_H
#define _DISPLAY_H

void display(char *buffer);

#endif
```
### main.c :
```c
#include<stdio.h>
#include "display.h"

void main(){
        display("Hello world\n");
}
```
### display.c :
```c
#include<stdio.h>

void display(char *buffer){
        printf("%s\n",buffer);
}
```
gcc -c display.c  -> display.o
ar -rc libdisplay.a display.o  -> libdisplay.a
gcc main.c -L. -l display  -> a.out

## Project top level 
1. src
     - mainapp -> Main.c
     - disp  -> display.c
2. inc
     - disp  -> display.h
  
## Build_directory
  
- Each and every folder and subfolder will need to have CMakeLists.txt.
- CMAKE_SOURCE_DIR  -> path to source tree.
- CMAKE_BINARY_DIR  -> path to build dircetory.

add_subdirectory(<DIR_NAME)
add_subdirectory(src)

- display.c will be compiled to generate libdisplay.a and main.c will be compiled and main.c linked to libdisplay.a.

## Library creation :
add_library(<LIB_NAME>SRC)
addlibrary(display display.c)    -> it generates libdisplay.a

## Linking Libraries :
target_link_libraries(<OUTPUT_FILE><LIB_NAME>) 
target_link_libraries(mainapp display)

- Never write an absolute path in CMakeList.txt because these paths are changed.
- Use the reference of macros to access source directory path and build directory path.
- Similar source tree will be generated in the build directory and all the corresponding libraries will be placed in the corresponding location.
- Binaries which are not executable are called as archives.Ex:static library
- Binaries which are executable are called as run time outputs.

- To specify generation of runtime outputs and archeives :
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/Bin)
set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/Lib)

- Top level CMakeLists.txt will have instructions to be executed before compilation and move to subdirectories to scan another CMakeLists.txt for further instructions.

add_executable(mainapp main.c file2.c file3. file4.c ...)
- addexecutable use this souce file is to  execute and remaining files are dependencies.
- Cmake eases the creation of makefiles in a complex architectured source code.


## Compilers :
compilers translates high level language to machine understandable language.

- Based on architectures :

### Native/host compiler :
Being on a machine, compiles for same machine.

## Cross compiler :
Being aon a machine, compiles for different machine.
And generated code was not compiled on the own machine.


