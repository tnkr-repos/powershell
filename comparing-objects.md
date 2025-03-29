# COMPARE-OBJECT

- Alias - `Diff`
- Use XML format for saving PowerShell objects instead of CSV because XML can represent deeply nested data, whereas CSV can only represent a single, flat level of data
- To compare processes from a baseline to the currently running use the following snippet

```powershell
Compare-Object -ReferenceObject (Import-CliXml baseline.xml) -DifferenceObject (Get-Process) -Property Name
```

- `-ReferenceObject` - Baseline; Use a parenthetical command that imports the baseline data from the XML file. The entire contents of the XML file is converted to objects, and those become the values for the parameter
- `-DifferenceObject` - What you wanto to compare the reference to
- `-Property` - Tell which object property to compare
- The results include a "Side Indicator" - An arrow which points to right to tell if there is something extra in the current set, and points left if there is something extra in the reference set
