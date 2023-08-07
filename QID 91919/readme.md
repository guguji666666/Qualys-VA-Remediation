## QID 91919

#### Microsoft Windows Codecs Library HEVC Video and AV1 Extensions Remote Code Execution(RCE)Vulnerability for June 2022

### Remediation steps ( remove the extensions)

#### Check existing `HEVC`
```powershell
Get-AppxPackage -AllUsers *HEVC*
```
![image](https://github.com/guguji666666/Qualys-VA-Remediation/assets/96930989/bb431ac6-39de-4c84-93a5-36a87ca7e57a)


Then navigate to the path below in registry editor, get the full name of the package
```
Computer\HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Appx\AppxAllUserStore\Applications
```
![image](https://github.com/guguji666666/Qualys-VA-Remediation/assets/96930989/ffca196e-2c10-47ad-9e4d-58beef84cd39)

Then remove this package
```powershell
Remove-AppxPackage -AllUsers -Package <package full name>
```

#### Check existing `AV1`
```powershell
Get-AppxPackage -AllUsers *AV1*
```
![image](https://github.com/guguji666666/Qualys-VA-Remediation/assets/96930989/8a3f8c4e-2d94-4f85-9105-142cef8a6b10)

Then navigate to the path below in registry editor, get the full name of the package
```
Computer\HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Appx\AppxAllUserStore\Applications
```

Then remove this package
```powershell
Remove-AppxPackage -AllUsers -Package <package full name>
```

After removing these extensions, please double confirm running the powershell commands below:
```powershell
Get-AppxPackage -AllUsers *HEVC*
```
```powershell
Get-AppxPackage -AllUsers *AV1*
```

It may take around 24 hours to refresh the VA findings




