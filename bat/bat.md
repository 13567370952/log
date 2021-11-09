
## 21-11-09
### svn更新
```bat
@echo off
if "%1"=="h" goto begin
start mshta vbscript:createobject("wscript.shell").run("""%~nx0"" h",0)(window.close)&&exit
:begin
"C:/Program Files/TortoiseSVN/bin/TortoiseProc.exe"  /command:update  /path:"D:\wamp64\www\billing\application" /closeonend:1

```

## 21-11-09
### 模拟回车按键
```bat
CreateObject("WScript.Shell").Run "cmd /c C:\Users\2020-2\Desktop\bill_update.bat",0
CreateObject("WScript.Shell").SendKeys "{enter}" 
```
