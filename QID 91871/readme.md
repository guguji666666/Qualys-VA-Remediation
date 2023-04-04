## QID 91871

The QID 91871 is detected on the latest scans showing the below result.
RESULT: Microsoft is vulnerable Microsoft.MSPaint detected Version '6.1907.29027.0'

The QID detected the version of Microsoft.MSPaint by querying wmi class Win32_InstalledStoreProgram

### Remediation steps

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
Note the PackageFullName, we need it later

![image](https://user-images.githubusercontent.com/96930989/229702915-e12f5704-bbf1-4913-9ec8-a687f6bcf6af.png)

Remove the app for all users
```powershell
Remove-AppxPackage -AllUsers -Package <PackageFullName>
```

Sample
```powershell
Remove-AppxPackage -AllUsers -Package Microsoft.Paint_11.2301.22.0_x64__8wekyb3d8bbwe
```

Then we ran the commands below and confirmed Microsoft.Paint is removed completely

![image](https://user-images.githubusercontent.com/96930989/229703379-a17577f0-eca4-4c94-97f9-21e2191d69bf.png)

The entries related to Microsoft.Paint are also removed from `Get-WmiObject -Class Win32_InstalledStoreProgram`

Paint 3D is not found in the installed apps

![image](https://user-images.githubusercontent.com/96930989/229704855-b90334c9-0a90-479d-8533-3ea826c9175c.png)
