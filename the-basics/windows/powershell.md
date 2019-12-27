# PowerShell

PowerShell is Windows new shell. It comes by default from Windows 7. But can be downloaded and installed in earlier versions.

* PowerShell provides access to almost everything an attacker might want.
* It is based on the .NET framework.
* It is basically bash for windows

## Basics <a id="basics"></a>

So a command in PowerShell is called **cmdlet**. To get help on how to use a **cmdlet** while in PowerShell, the man-page, you do:

```text
Get-Help    <cmdlet    name    |    topic    name>
```

Example

```text
get-help echo
get-help get-command
```

### Format Output <a id="format-output"></a>

```text
 get-process | Format-Table ProcessName
```

### Grep Equivalent <a id="grep-equivalent"></a>

Select-String

```text
cat .\filelist.txt | Select-String Music
```

**Find Juicy Stiff in the File System**

```text
ls -PATH C:\PATH\TO\DIRECTORY -Recurse | Select-String -pattern STRING
```

Searches C:\PATH\TO\DIRECTORY for files that contain the "STRING", displaying the file name and the line containing the STRING.

Note: ls is an alias for Get-ChildItem

