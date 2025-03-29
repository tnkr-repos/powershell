# IMPORT EXPORT CONVERT OBJECTS

- Import - Read data from external format (usually a file) and bring the data into the shell in the form of objects
- Export - Take objects in the shell, convert them to some other data structure, and write the data out to an external form (usually a file)
- ConvertTo - Take objects in the shell, change them into some other data structure, and then leave that converted data in the shell
- ConvertFrom - Take some data structure and convert it into an object data structure that the shell uses

- CSV
  - ConvertTo-Csv - Can be used to create CSV or other delimited files (using `-Delimited` parameter)
  - Includes type of object as the first line of the CSV. Use `-NoTypeInformation` to exclude this from the file
  - Exporting and converting don't work on the cmdlet's default output. They process all objects and all properties. If that isn't what is required, select the necessary properties
  - When exporting or converting to the CSV format any properties that are nested objects don't translate well. So stick with properties that have simple values
  - To bring data into the shell as objects from a CSV file use `Import-Csv` and let PowerShell do the work of interpreting the CSV file

```powershell
Get-Process | Select-Object name, id, vm, pm | ConvertTo-Csv | Out-File procs.csv
Get-Process | Export-Csv procs.csv    # convertto-csv | out-file combined in one

Import-Csv data.csv | Where-Object { $PSItem.Department -eq "IT" } | Sort-Object -Property name
```

- HTML
  - The only cmdlet is `ConvertTo-HTML` - it is only a one-way trip
  - Make sure to use simple property values and no nested objects
  - It has many more uses for its different parameters

```powershell
Get-Service | Where-Object { $PSItem.Status -eq 'Stopped' } |
  ConvertTo-HTML -Property Name, Status, DisplayName |
  Out-File Stopped.html
```

- CliXML
  - It's XML that PowerShell understands natively
  - It is great to persist objects over time as it can handle nested properties

```powershell
Get-Process | Export-CliXml procs.xml
```

