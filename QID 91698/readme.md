## QID 91698

### QID: 91698 : Microsoft Windows Codecs Library Remote Code Execution Vulnerabilities
### Scan Results: Microsoft vulnerable Microsoft.WebpImageExtension detected Version '1.0.22753.0'

### Remediation steps (remove the extension)

#### Check existing `WebpImageExtension`
```powershell
Get-AppxPackage -AllUsers *WebpImageExtension*
```
![image](https://github.com/guguji666666/Qualys-VA-Remediation/assets/96930989/b9092b2b-93e8-4b7a-b9c7-a3b6eb0cfbe2)

Then navigate to the path below in registry editor, get the full name of the package
```
Computer\HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Appx\AppxAllUserStore\Applications
```
![image](https://github.com/guguji666666/Qualys-VA-Remediation/assets/96930989/54b93067-506a-427a-b2c5-5bc37fa82d84)

Then remove this package
```powershell
Remove-AppxPackage -AllUsers -Package <package full name>
```

After removing these extensions, please double confirm running the powershell commands below:
```powershell
Get-AppxPackage -AllUsers *WebpImageExtension*
```

It may take around 24 hours to refresh the VA findings

