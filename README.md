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

# extended function
### Run the frida javascript code from within AutoAssembler.  
If a string is written to an address between 0 and 100, it will be interpreted as frida javascript code and executed.  
The address is also mapped to a script number.  
If you write "UNLOAD" with the same number, the script will be canceled.  

```
{$lua}
[enable]
local jscode = [[
console.log("HELLO,WORLD!";)
]]
writeString(0,jscode)
[disable]
writeString(0,[[UNLOAD]])
```