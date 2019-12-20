# WindowsCMD

### Access to UNC

##### pushd <UNC path> will create a temporary virtual drive and get into it.
##### popd will delete the temporary drive and get you back to the path you were when you entered pushd.
```
C:\a\local\path> pushd \\network_host\a\network\path
U:\a\network\path> REM a temporary U: virtual drive has been created  
U:\a\network\path> popd  
C:\a\local\path> REM the U: drive has been deleted  
C:\a\local\path>  
```

### GetFilesNamesAndTime
```
dir /a:-d /o:ns /t:w /s >files.txt
```

### ReplaceTextContent
```
echo off
set BFR_STR1=01234
set AFR_STR1=56789
set BFR_STR2=ABCDE
set AFR_STR2=FGHIJ

set INPUT_FILE=D:.\test_before.txt
set OUTPUT_FILE=.\test_after.txt

del %OUTPUT_FILE%

echo Start（%INPUT_FILE%）
setlocal enabledelayedexpansion
for /f "delims=" %%A in (%INPUT_FILE%) do (
    set line0=%%A
    set line1=!line0:%BFR_STR1%=%AFR_STR1%!
    set line2=!line1:%BFR_STR2%=%AFR_STR2%!
    echo !line2!>>%OUTPUT_FILE%
)
endlocal
echo End
pause
```

### TakeOwnership
```
takeown /F "C:\Windows\regedit.exe" /A
/F - file to become owner of
/A - means it will set the users group (ie. Administrators, not userxyz)

icacls "C:\Windows\regedit.exe" /grant Administrators:F
/grant - will add permissions
:F - Full Control

icacls "C:\Windows\regedit.exe" /setowner "NT SERVICE\TrustedInstaller"
/setowner - new owner

icacls "C:\Windows\regedit.exe" /grant:r Administrators:RX
/grant:r - will set permissions (removing higher ones)
:RX - Read and Execute
```

