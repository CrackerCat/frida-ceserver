# frida-ceserver
frida-based ceserver.   
iOS analysis is possible with Cheat Engine.  

Original by Dark Byte.  

# Usage
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
  
# BintUils
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
