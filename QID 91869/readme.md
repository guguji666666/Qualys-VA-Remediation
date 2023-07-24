# QID 91869
[QID 91869: Microsoft Windows Codecs Library Remote Code Execution (RCE) Vulnerability for March 2022](https://cve.report/qid/91869)

## Affected Product:
* HEIFImageExtension before 1.0.43012.0
* VP9VideoExtensions before 1.0.42791.0 (already removed by us before)
* RawImageExtension before 2.1.30391.0
* HEVCVideoExtension before 1.0.50361.0 and 1.0.50362.0

## Remediation steps (remove the extensions)

### HEIFImageExtension
#### Check existing `HEIFImageExtension`
```powershell
Get-AppxPackage -AllUsers *HEIFI*
```
![image](https://github.com/guguji666666/Qualys-VA-Remediation/assets/96930989/c487b4fc-8408-4170-8d29-b130d3eb748f)

Then navigate to the path below in registry editor, get the full name of the package
```
Computer\HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Appx\AppxAllUserStore\Applications
```
![image](https://github.com/guguji666666/Qualys-VA-Remediation/assets/96930989/e5dec8d2-682f-4b98-8945-1ec124848665)

Then remove this package
```powershell
Remove-AppxPackage -AllUsers -Package <package full name>
```

### VP9VideoExtensions

### RawImageExtension
#### Check existing `RawImageExtension`
```powershell
Get-AppxPackage -AllUsers *RawImage*
```
![image](https://github.com/guguji666666/Qualys-VA-Remediation/assets/96930989/62ff921f-2c4a-4477-9a84-70ce2a8196e7)

Then navigate to the path below in registry editor, get the full name of the package
```
Computer\HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Appx\AppxAllUserStore\Applications
```
![image](https://github.com/guguji666666/Qualys-VA-Remediation/assets/96930989/12b5f79e-0c86-4240-9f09-693c906ae9e4)

Then remove this package
```powershell
Remove-AppxPackage -AllUsers -Package <package full name>
```

### HEVCVideoExtension
#### Check existing `HEVCVideoExtension`
```powershell
Get-AppxPackage -AllUsers *HEVC*
```
![image](https://github.com/guguji666666/Qualys-VA-Remediation/assets/96930989/52c2e3cb-7259-467e-b4c2-df89b307be3b)

Then navigate to the path below in registry editor, get the full name of the package
```
Computer\HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Appx\AppxAllUserStore\Applications
```
![image](https://github.com/guguji666666/Qualys-VA-Remediation/assets/96930989/6c34ff5a-7d29-4279-87da-28daf7fcb16b)

Then remove this package
```powershell
Remove-AppxPackage -AllUsers -Package <package full name>
```

#### Verification
```powershell
Get-AppxPackage -AllUsers *HEIFI*
```
```powershell
Get-AppxPackage -AllUsers *RawImage*
```
```powershell
Get-AppxPackage -AllUsers *HEVC*
```
