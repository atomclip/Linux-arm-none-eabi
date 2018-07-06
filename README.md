# GNU Arm embedded toolchain for Linux (64-bit)

The GNU Embedded Toolchain for Arm is a ready-to-use, open source suite of tools
for C, C++ and Assembly programming targeting Arm Cortex-M and Cortex-R family 
of processors. It includes the GNU Compiler (GCC) and is available free of 
charge directly from Arm for embedded software development on Windows, Linux and
macOS operating systems.

<div>
<img src="https://raw.githubusercontent.com/atomclip/linux-arm-none-eabi/master/images/Linux.png" alt="Linux" width="24%">
<img src="https://raw.githubusercontent.com/atomclip/linux-arm-none-eabi/master/images/GNU.png" alt="GNU" width="24%">
<img src="https://raw.githubusercontent.com/atomclip/linux-arm-none-eabi/master/images/Cortex-M.png" alt="Cortex-M" width="24%">
<img src="https://raw.githubusercontent.com/atomclip/linux-arm-none-eabi/master/images/Cortex-R.png" alt="Cortex-R" width="24%">
</div>

This repository is the original Linux (64-bit) version of the GNU Compiler from 
Arm packaged for Visual Studio Code:

[GNU Arm embedded toolchain](https://developer.arm.com/open-source/gnu-toolchain/gnu-rm/downloads)

## Install
In Visual Studio Code goto extensions (shift+ctrl+x), search for '*atomclip*' 
and install the extension that is suited for your operating system. 

The extension has three paths for the toolchain. You can use this in the 
tasks.json.

- arm-none-eabi.bin
- arm-none-eabi.include
- arm-none-eabi.lib

Here is an example of tasks.json for GNU make. 
```javascript
{
  "version": "2.0.0",
  "tasks": [
    {
      "label": "build firmware",
      "type": "shell",
      "command": "make test",
      "options": {
        "env": {
          "INCLUDE": "${config:arm-none-eabi.include}",
          "LIB": "${config:arm-none-eabi.lib}",
        }
      },
      "osx": {
        "options": {
          "env": {
            "PATH": "${config:arm-none-eabi.bin}:${env:PATH}",
          }
        },
      },
      "linux": {
        "options": {
          "env": {
            "PATH": "${config:arm-none-eabi.bin}:${env:PATH}",
          }
        },
      },
      "windows": {
        "options": {
          "env": {
            "PATH": "${config:arm-none-eabi.bin};${env:PATH}",
          }
        },
      },
      "group": {
        "kind": "build",
        "isDefault": true,
      },
      "problemMatcher": "$gcc"
    }
  ]
}
```
With the following makefile:
```makefile
.PHONY: test

test:
	@echo $(PATH)
	@echo $(INCLUDE)
	@echo $(LIB)
```

## Release Notes


### Version 0.1.0
Version 7-2018-q2-update for Linux.
Added script to create symlinks in /usr/local/bin.

### Version 0.0.5
Operating system specific PATH environment variable. 

### Version 0.0.3
Version 7-2017-q4-major for Linux (64-bit)
Released: December 18, 2017