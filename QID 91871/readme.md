# QID 91871

The QID 91871 is detected on the latest scans showing the below result.
RESULT: Microsoft is vulnerable Microsoft.MSPaint detected Version '6.1907.29027.0'

The QID detected the version of Microsoft.MSPaint by querying wmi class Win32_InstalledStoreProgram


## Remediation steps on Win 10 (Remove the application)

![image](https://user-images.githubusercontent.com/96930989/229955007-4a5c912e-243b-488d-b2ff-f7d58d05e34d.png)

Run powershell command
```powershell
Get-WmiObject -Class Win32_InstalledStoreProgram
```

![image](https://user-images.githubusercontent.com/96930989/229954738-38b1b520-0f6a-405f-9b00-fea6f656f153.png)

Find the entries that contains `Paint`
```powershell
Get-AppxPackage -AllUsers *Paint* 
```

![image](https://user-images.githubusercontent.com/96930989/229726325-ffce4140-9ecd-45a1-8bfe-3cb38f2402ec.png)

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
Remove-AppxPackage -AllUsers -Package Microsoft.MSPaint_2019.729.2301.0_neutral_~_8wekyb3d8bbwe
```


Then we ran the commands below and confirmed Microsoft.Paint is removed completely
```powershell
Get-AppxPackage -AllUsers *Paint*
```
```powershell
Get-AppxPackage -AllUsers -Name Microsoft.MSPaint
```
```powershell
Get-WmiObject -Class Win32_InstalledStoreProgram
```

![image](https://user-images.githubusercontent.com/96930989/229955210-3ada3a68-93d3-45f6-ba6c-1280d83835fd.png)

![image](https://user-images.githubusercontent.com/96930989/229955298-93916bb1-2bcb-4d3d-b54e-60b1ac7651e7.png)


Paint 3D is no longer found in the installed apps

![image](https://user-images.githubusercontent.com/96930989/229955323-19d3c955-19d9-464e-9ae3-eb4bbff6bc19.png)


## Remediation steps on Win 11

Run powershell command
```powershell
Get-WmiObject -Class Win32_InstalledStoreProgram
```

You may find several entries related to `Microsoft.Paint`

![image](https://user-images.githubusercontent.com/96930989/229701750-17a5a739-3565-4c7e-9a22-53d2c176ece4.png)


Find the entries that contains `Paint`
```powershell
Get-AppxPackage -AllUsers *Paint* 
```
![image](https://user-images.githubusercontent.com/96930989/229702117-e03634d4-3ba1-4821-b4be-af8f46dfb224.png)


Find the entries that contains `Microsoft.Paint`
```powershell
Get-AppxPackage -AllUsers -Name Microsoft.Paint
```

Go to registry key, navigate to the path below, look for the app's package name that contains `Paint`
```
Computer\HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Appx\AppxAllUserStore\Applications
```
![image](https://user-images.githubusercontent.com/96930989/229831718-15218353-b975-45ea-9033-969d6e1e7c18.png)


Remove the app for all users
```powershell
Set-ExecutionPolicy Unrestricted
```
```powershell
Remove-AppxPackage -AllUsers -Package <PackageFullName>
```

Then we ran the commands below and confirmed Microsoft.Paint is removed completely

```powershell
Get-AppxPackage -AllUsers *Paint* 
```
```powershell
Get-AppxPackage -AllUsers -Name Microsoft.Paint
```
```powershell
Get-WmiObject -Class Win32_InstalledStoreProgram
```

Paint/Paint 3D apps should no longer be found in the installed apps
