# WORKING WITH THE COMPONENT OBJECT MODEL (COM)

- Before Microsoft invented the .NET framework folks relied on Component Object Model (COM) to write software components that can easily interoperate
- Active Directory Service Interfaces (ADSI), WMI, and object models that enable you to script against Office products are all based on COM
- The .NET framework ships the ability to load and use software that comply with the COM specification. This is done through the _interop layer_
- Instantiating is the act of loading an object into memory, storing a reference to that object in a variable, and generally preparing to use the object
  - `$obj = New-Object -ComObject '<object_type>'`
  - The `-ComObject` parameter tells Powershell to fall back to the old COM way of doing things, rather than trying to create an instance of a .NET Framework class
  - If it fails then either the COM object isn't compatible with PowerShell, the progID isn't in the registry, or need to consult documentation for the correct way to instantiate the object of this type
- It is to be used only when performing a lot of automation based on the Office suite. If you have a .NET alternative, use that instead, and try and avoid working with COM objects
- COM objects have members - properties and methods. Properties may be read-only or writable; methods cause the objects to execute some task or behavior. Properties in COM objects are other embedded COM objects.
  - Properties are accessed by referring to the object variable and property name - `$Network = New-Object -ComObject WScript.Network; $Network.Username`
  - Methods work the same way (you cannot omit parentheses after function name even if it doesn't take any parameters) - `Network.MapNetworkDrive('Z:\','\\server\share')`
  - Use `Get-Member` on any ComObject to get the properties and methods to be used on it. Once the object exists in PowerShell, you can use it like any other PowerShell object

```powershell
$data = @()
$fso = New-Object -ComObject 'Scripting.FileSystemObject'
$top = $fso.GetFolder('C:\Test')
$data += New-Object PSObject -Property @{
  Path = $top.Path
  Size = $top.Size
}
foreach ($sf in $top.SubFolders) {
  $data += New-Object PSObject -Property @{
    Path = $sf.Path
    Size = $sf.Size
  }
}
$data

$word = New-Objeect -ComObject 'Word.Application'
$excel = New-Object -ComObject 'Excel.Application'
```
