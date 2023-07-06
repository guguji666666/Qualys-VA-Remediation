[QID 91761 Microsoft Windows Codecs Library and VP9 Video Extensions Multiple Vulnerabilities](https://cve.report/qid/91761)

## Remediation steps on Win 10/11

### In `Apps & features` we can't find the VP9 extension
![image](https://github.com/guguji666666/Qualys-VA-Remediation/assets/96930989/44330279-59d5-43ff-8ecf-acefe2611bce)

### In Microsoft Store we can find VP9 extension installed
![image](https://github.com/guguji666666/Qualys-VA-Remediation/assets/96930989/87e6ea02-20fa-4371-86f1-422be425b4c2) <br>
![image](https://github.com/guguji666666/Qualys-VA-Remediation/assets/96930989/a9b32886-c61e-4de5-81a2-70f4187b0aea)


Run powershell command
```powershell
Get-WmiObject -Class Win32_InstalledStoreProgram > c:\temp\appsinstalled.txt
```

In txt file we can find several entries related to `VP9` <br>
![image](https://github.com/guguji666666/Qualys-VA-Remediation/assets/96930989/926e54e2-c62e-4dd7-a02d-33b732f41369)

Then run the powershell command below
```powershell
Get-AppxPackage -AllUsers *VP9* 
```
![image](https://github.com/guguji666666/Qualys-VA-Remediation/assets/96930989/7b4bf1d3-a246-4ce7-85ad-9fefe0694a04)


Go to registry key, navigate to the path below, look for the app's package name that contains `VP9`
```
Computer\HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Appx\AppxAllUserStore\Applications
```
![image](https://github.com/guguji666666/Qualys-VA-Remediation/assets/96930989/6c1cd75d-f988-4a3f-a63c-0f6858977c56)


Remove the app for all users
```powershell
Set-ExecutionPolicy Unrestricted
```
```powershell
Remove-AppxPackage -AllUsers -Package <PackageFullName>
```

Sample
```powershell
Set-ExecutionPolicy Unrestricted
```
```powershell
Remove-AppxPackage -AllUsers -Package Microsoft.VP9VideoExtensions_1.0.61591.0_neutral_~_8wekyb3d8bbwe
```

Then we ran the commands below and confirmed `Microsoft.VP9VideoExtensions` is removed completely
```powershell
Get-AppxPackage -AllUsers *VP9*
```
```powershell
Get-WmiObject -Class Win32_InstalledStoreProgram > c:\temp\appsinstalledAfter.txt
```

VP9VideoExtensions is no longer found in the installed apps <br>
![image](https://github.com/guguji666666/Qualys-VA-Remediation/assets/96930989/c9da0bf7-c191-407a-ad0c-2e1b5fac8da4)

Reopen Microsft store, the VP9 video extension is no longer detected <br>
![image](https://github.com/guguji666666/Qualys-VA-Remediation/assets/96930989/ab75d5c8-9ebe-4512-9b44-2e1d32b09b19)

If you want to install it with latest version, please reboot the machine and install it from Microsoft store

