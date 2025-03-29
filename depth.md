# POWERSHELL IN DEPTH

## CHAPTER 6 - OPERATORS

- Help files
  - `about_operators`
  - `about_arithmetic_operators`
  - `about_assignment_operators`
  - `about_comparison_operators`
  - `about_logical_operators`
  - `about_operator_precedence`
  - `about_type_operators`

- Logical operators need to be applied on objects of similar types, otherwise we might be non boolean values as a result, which should not be the case:

```powershell
$a = 1, 2, 3
$a -eq 1       # 1
$a -contains 1 # True
$a[0] -eq 1    # True
```

- Logical Operators in PowerShell - `-eq, -ne, -gt, -lt, -ge, -le, -like, -notlike, -match, -cmatch, -notmatch, -cnotmatch, -contains, -notcontains, -replace`

- All string comparisons are insensitive by default. For case-sensitive comparison use operators with the `c` prefix, and for explicitly specifying case-insensitive comparison add an `i` prefix

- Any conversion activity involves the value of the RHS of the comparison operator. The value is converted to the same type as the value to the left-hand side

```powershell
9 -gt "10"    # False
9 -le "10"    # True
```

- `-contains` looks inside a collection of objects and see if that collection contains another object. But it tries to compare all properties of the objects, and if any one of them is different then it declares them as not a match

```powershell
$collection = 
```
