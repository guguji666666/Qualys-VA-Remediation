# QID 91871

The QID 91871 is detected on the latest scans showing the below result.
RESULT: Microsoft is vulnerable Microsoft.MSPaint detected Version '6.1907.29027.0'

The QID detected the version of Microsoft.MSPaint by querying wmi class Win32_InstalledStoreProgram


## Remediation steps on Win 10

Run powershell command
```powershell
Get-WmiObject -Class Win32_InstalledStoreProgram
```

Find the entries that contains `Paint`
```powershell
Get-AppxPackage -AllUsers *Paint* 
```

![image](https://user-images.githubusercontent.com/96930989/229726325-ffce4140-9ecd-45a1-8bfe-3cb38f2402ec.png)

Find the entries that contains `Microsoft.MSPaint`
```powershell
Get-AppxPackage -AllUsers -Name Microsoft.MSPaint
```

Go to registry key, navigate to the path below, look for the app's package name that contains `Paint`
```
KEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Appx\AppxAllUserStore\Applications\
```

Remove the app for all users
```powershell
Set-ExecutionPolicy Unrestricted
Remove-AppxPackage -AllUsers -Package <PackageFullName>
```


Then we ran the commands below and confirmed Microsoft.Paint is removed completely
```powershell
Get-AppxPackage -AllUsers *Paint* 
Get-AppxPackage -AllUsers -Name Microsoft.MSPaint
Get-WmiObject -Class Win32_InstalledStoreProgram
```

Paint 3D is no longer found in the installed apps



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
Remove-AppxPackage -AllUsers -Package <PackageFullName>
```

Then we ran the commands below and confirmed Microsoft.Paint is removed completely

```powershell
Get-AppxPackage -AllUsers *Paint* 
Get-AppxPackage -AllUsers -Name Microsoft.Paint
Get-WmiObject -Class Win32_InstalledStoreProgram
```

Paint/Paint 3D apps should no longer be found in the installed apps
