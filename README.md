# Pymaginopolis

Pymaginopolis is a collection of Python tools for reverse engineering Microsoft 3D Movie Maker.

## Ghidra scripts

The `ghidra_scripts` directory contains scripts for automating reverse engineering of 3D Movie Maker using [Ghidra](https://ghidra-sre.org/).

To load these scripts into Ghidra, open the Script Manager, choose Script Directories and add the `ghidra_scripts` directory to the list.

## Python library

Pymaginopolis is a Python library for reading and writing Microsoft 3D Movie Maker data files. It also includes a disassembler for the custom scripting engine that 3DMM uses to control the user interface. 

### Compatible applications

Pymaginopolis can read "chunky" data files used by the following Microsoft products:

* Microsoft 3D Movie Maker
* Microsoft Nickelodeon 3D Movie Maker
* Microsoft Creative Writer 2
* Microsoft Plus! for Kids Media Gallery

### Features

* Read/write chunky files
  * Chunk compression not supported yet
* Read/write support for some chunk types:
  * String tables (GST)
  * Scripts (GLOP, GLSC)

## Requirements

* Python 3.6+

## Script Engine

Microsoft 3D Movie Maker and Creative Writer 2 are built on the same game engine. This game engine has a scripting system that is used to control user interface elements and 2D animation. Graphical objects (GOBs) can have scripts attached to them to handle messages such as when the user clicks on an object.

Most releases of 3DMM/CW2 have a partial set of opcode names embedded in the binary. The Japanese release of 3DMM has the full set of opcode names. There is also documentation for some of the opcodes in the [script engine patent](https://patents.google.com/patent/US5867175).

The opcode list used by the disassembler is located in `pymaginopolis\scriptengine\data\opcodes.xml`. The disassembler will resolve constants defined in `pymaginopolis\data\constants-3dmm.xml`. Most of these constants are from manual reverse engineering of 3DMM.

## Usage

Dump a chunky file to XML:
```
python -m pymaginopolis.tools.disassembler 3dmovie.chk 3dmovie.xml
```

Combine an existing chunky file with chunks in an XML file:
```
python -m pymaginopolis.tools.xml2chk new.chk chunks.xml --template existing.chk
```

Disassemble all of the scripts in a chunky file:

```
python -m pymaginopolis.tools.disassembler D:\3DMOVIE\STUDIO.CHK
```

## Roadmap

* I am currently working on an assembler for writing new scripts and patching them into existing chunky files.
