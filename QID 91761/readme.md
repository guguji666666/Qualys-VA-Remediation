[QID 91761 Microsoft Windows Codecs Library and VP9 Video Extensions Multiple Vulnerabilities](https://cve.report/qid/91761)

## Remediation steps on Win 10/11

### In `Apps & features` we can't find the VP9 extension
![image](https://github.com/guguji666666/Qualys-VA-Remediation/assets/96930989/44330279-59d5-43ff-8ecf-acefe2611bce)

Run powershell command
```powershell
Get-WmiObject -Class Win32_InstalledStoreProgram > c:\temp\appsinstalled.txt
```

Find the entries that contains `VP9`
```powershell
Get-AppxPackage -AllUsers *Paint* 
```

Find the entries that contains `Microsoft.MSPaint`
```powershell
Get-AppxPackage -AllUsers -Name Microsoft.MSPaint
```
![image](https://user-images.githubusercontent.com/96930989/229954842-9b0c910a-27b5-4ced-be3d-e5e628a3540c.png)

Go to registry key, navigate to the path below, look for the app's package name that contains `Paint`
```
Computer\HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Appx\AppxAllUserStore\Applications
```

![image](https://user-images.githubusercontent.com/96930989/229954944-824e661f-8487-491c-9a43-8a91a8163ea7.png)

Remove the app for all users
```powershell
Set-ExecutionPolicy UnrestrictedSet-ExecutionPolicy Unrestricted
```
```powershell
Remove-AppxPackage -AllUsers -Package <PackageFullName>
```

Sample
```powershell
Set-ExecutionPolicy UnrestrictedSet-ExecutionPolicy Unrestricted
```
```powershell
Remove-AppxPackage -AllUsers -Package Microsoft.MSPaint_2019.729.2301.0_neutral_~_8wekyb3d8bbwe
```

Then we ran the commands below and confirmed Microsoft.Paint is removed completely
```powershell
Get-AppxPackage -AllUsers *Paint* Set-ExecutionPolicy Unrestricted
```
```powershell
Get-AppxPackage -AllUsers -Name Microsoft.MSPaintSet-ExecutionPolicy Unrestricted
```
```powershell
Get-WmiObject -Class Win32_InstalledStoreProgram
```

![image](https://user-images.githubusercontent.com/96930989/229955210-3ada3a68-93d3-45f6-ba6c-1280d83835fd.png)

![image](https://user-images.githubusercontent.com/96930989/229955298-93916bb1-2bcb-4d3d-b54e-60b1ac7651e7.png)


Paint 3D is no longer found in the installed apps

![image](https://user-images.githubusercontent.com/96930989/229955323-19d3c955-19d9-464e-9ae3-eb4bbff6bc19.png)
