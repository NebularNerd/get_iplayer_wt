# get_iplayer_wt

Run get_iplayer_web_pvr in a Windows Terminal tab  


## About:
This is a quick and easy batch to let you run the [get_iplayer](https://github.com/get-iplayer/get_iplayer) web pvr inside a [Windows Terminal](https://github.com/microsoft/terminal) tab. It's a direct copy of the ```C:\Program Files\get_iplayer\get_iplayer_web_pvr.cmd``` file except it adds a loop to the end to prevent the tab killing the pvr process. I made this purely for fun and to save having a random floating console window. I did post an issue [#417](https://github.com/get-iplayer/get_iplayer/issues/417) about the web pvr not working inside a Windows Terminal, if they reopen the ticket I'll update the devs about my quick fix and see if they want to roll it into future versions.

## Usage:
Simply copy the ```get_iplayer_web_pvr.bat``` file to your get_iplayer directory, typically ```C:\Program Files\get_iplayer\``` then create a new profile in Windows Terminal using the following settings (adjust if you have installed elsewhere):  
- Command Line: ```%SystemRoot%\System32\cmd.exe /c "C:\Program Files\get_iplayer\get_iplayer_web_pvr.bat"```
- Start In: ```%HOMEDRIVE%%HOMEPATH%```
- Icon: ```%SystemDrive%\Program Files\get_iplayer\get_iplayer_pvr.ico```
- Set a theme in the appearance section, I use the hideous Solarized Light theme to help ensure I don't close it by mistake!
Done!  

## File contents:
The only changes made to the stock file are the last 3 lines, this prevents Windows Terminal killing the tab processes, WT behaves differently to a regular command prompt, when it reaches the end of the stock batch file it kills the PVR service off.
```  
@echo off
setlocal
set GIP_INST=%~dp0
if #%GIP_INST:~-1%# == #\# set GIP_INST=%GIP_INST:~0,-1%
start "PVR Manager Service" /min /b cmd /k "%GIP_INST%\get_iplayer_cgi.cmd"
ping 127.0.0.1 -n 5 -w 1000 > NUL
start http://localhost:1935
:noexitloop
pause>nul
GOTO noexitloop
```  

## Screenshot
![I use the hideous Solarized Light theme to help ensure I don't close it by mistake!](https://github.com/NebularNerd/get_iplayer_wt/blob/11aab2a5b8327037e73ce3ce17cfbd7237b9c5b1/get_iplayer_web_pvr_wt.png)
