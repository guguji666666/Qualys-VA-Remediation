## QID 91764

### [QID 91764: Microsoft Windows Codecs Library Web Media Extension Remote Code Execution Vulnerability](https://cve.report/qid/91764)

A remote code execution vulnerability exists in the way that Microsoft Windows Codecs Library handles objects in memory.

#### Affected Product:
Microsoft.WebMediaExtensions prior to version 1.0.40831.0

#### QID detection Logic:
The gets the version of Extension by querying wmi class Win32_InstalledStoreProgram.

### Remediation steps (remove the extension)

#### Check existing `WebMediaExtension`
```powershell
Get-AppxPackage -AllUsers *MEDIA*
```
![image](https://github.com/guguji666666/Qualys-VA-Remediation/assets/96930989/37e71c6b-77ee-41ae-a63c-8faf1552f820)

Then navigate to the path below in registry editor, get the full name of the package
```
Computer\HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Appx\AppxAllUserStore\Applications
```
![image](https://github.com/guguji666666/Qualys-VA-Remediation/assets/96930989/df817ff3-f8e1-48b7-8197-0d4b69e97f11)

Then remove this package
```powershell
Remove-AppxPackage -AllUsers -Package <package full name>
```

After removing these extensions, please double confirm running the powershell commands below:
```powershell
Get-AppxPackage -AllUsers *MEDIA*
```

It may take around 24 hours to refresh the VA findings
