## QID 92030

### [QID 92030: Microsoft Raw Image Extension and VP9 Video Extension Information Disclosure Vulnerability](https://cve.report/qid/92030)

#### Affected Product:
* Raw Image Extension Win10 Version 21H2 and 22H2 , Win11 Version 21H2 prior to 2.0.61662.0
* Raw Image Extension Win11 Version 22H2 prior to 2.1.61661.0
* VP9 Video Extensions prior to 1.0.61591.0

#### QID detection Logic:
The detection gets the version of VP9VideoExtension by querying wmi class Win32_InstalledStoreProgram.

### Remediation steps ( remove the extensions)

#### Check existing `RawImageExtension`
```powershell
Get-AppxPackage -AllUsers *RawImage*
```
![image](https://github.com/guguji666666/Qualys-VA-Remediation/assets/96930989/656ff5c9-bbf1-4fe3-a59b-f9ce9ada4b0d)

Then navigate to the path below in registry editor, get the full name of the package
```
Computer\HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Appx\AppxAllUserStore\Applications
```
![image](https://github.com/guguji666666/Qualys-VA-Remediation/assets/96930989/87f66bdf-7018-47e0-8a2a-76d2f32ffcaf)

Then remove this package
```powershell
Remove-AppxPackage -AllUsers -Package <package full name>
```


#### Check existing `VP9 Video Extensions`
```powershell
Get-AppxPackage -AllUsers *VP9*
```
![image](https://github.com/guguji666666/Qualys-VA-Remediation/assets/96930989/2c3f8f6d-0e89-498b-9d2f-c06d40ba1912)

Then navigate to the path below in registry editor, get the full name of the package
```
Computer\HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Appx\AppxAllUserStore\Applications
```
![image](https://github.com/guguji666666/Qualys-VA-Remediation/assets/96930989/787a4177-fcd0-4693-bbf6-a8685cd67c4b)

Then remove this package
```powershell
Remove-AppxPackage -AllUsers -Package <package full name>
```

After removing these extensions, please double confirm running the powershell commands below:
```powershell
Get-AppxPackage -AllUsers *RawImage*
```
```powershell
Get-AppxPackage -AllUsers *VP9*
```

Then it may take around 24 hours to refresh the VA findings




