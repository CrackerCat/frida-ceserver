# frida-ceserver

frida-based ceserver.  
iOS analysis is possible with Cheat Engine.

Original by Dark Byte.

# Usage

Install python library.

```
pip install packaging
```

Install frida on iOS.

```
python main.py Cydia

# or

python main.py com.saurik.Cydia
```

Then, connect to the Cheat Engine in network mode.

The debugger is not available!

![img](https://user-images.githubusercontent.com/56913432/120924433-baa86600-c70e-11eb-8794-ab5c28ec50b6.png)

# Extended function

### Run the frida javascript code from within AutoAssembler.

If a string is written to an address between 0 and 100, it will be interpreted as frida javascript code and executed.  
The address is also mapped to a script number.  
If you write "UNLOAD" with the same number, the script will be canceled.

```
{$lua}
[enable]
local jscode = [[
console.log("HELLO,WORLD!");
]]
writeString(0,jscode)
[disable]
writeString(0,[[UNLOAD]])
```

# BinUtils

### ARM64 Disassembler/Assembler

By default, Cheat Engine does not implement the ARM64 disassembler.  
This can be supported by using the extension BinUtils.  
Download android-ndk, change path_to_android_ndk in the script below to the destination and put it in the autorun folder.  
Select View->BinUtils->ARM64 BinUtils to change the disassembly to ARM64.

```
local arm64config={}
arm64config.Name="ARM64"
arm64config.Description="BinUtils"
arm64config.Architecture="aarch64"
arm64config.Path=[[path_to_android_ndk\toolchains\aarch64-linux-android-4.9\prebuilt\windows-x86_64\bin]]
arm64config.Prefix="aarch64-linux-android-"
registerBinUtil(arm64config)
```

# Config

### target

If you specify it, you don't need to specify the name of the target app in the argument.

### isMobile

`0`:Linux  
`1`:Android or iOS

### mode

spawn is only valid for mobile device.  
`0`:spawn  
`1`:attach

### arch

`0`:i386  
`1`:x86_64  
`2`:arm  
`3`:aarch64

### fix_module_size

It is not possible to get the exact size of some modules in iOS.  
In this case, the module size will be corrected to the actual file size in order to get a larger module size.  
`true`:Enable the above function  
`false`:Disable the above function

### ceversion

Specify the version of the cheat engine itself.  
Since the part related to communication between the main unit and the ceserver differs depending on the version, the setting is necessary.
