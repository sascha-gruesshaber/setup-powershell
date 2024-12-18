# How to setup my PowerShell:
![image](https://user-images.githubusercontent.com/11362893/168903228-b8a9c969-f259-4549-bb6b-93ea8d80d99a.png)

1. Open current powershell and execute the following commands:
```PS
winget install Microsoft.WindowsTerminal
winget install Microsoft.PowerShell
winget install Git.Git

# Install a mono font to be used in the windows terminal
winget install --id=DEVCOM.JetBrainsMonoNerdFont  -e

```
2. Open up windows terminal and setup the newly installed nerd font as default
3 Execute the following commands in the windows terminal in the latest powershell:
```PS
winget install Starship.Starship
Install-Module -Name Terminal-Icons -Repository PSGallery
Install-Module -Name z

Write-Host "Write imports to your $profile"
Add-Content $profile "#Profile Setup done via https://github.com/sascha-gruesshaber/setup-powershell"
Add-Content $profile "Invoke-Expression (&starship init powershell)"
Add-Content $profile "Import-Module -Name Terminal-Icons"
Add-Content $profile "Import-Module z"

Exit
```
3. Restart your Windows Terminal, it should look a lot nicer now :-)

## Additional aliases:

### Remove gone branches
```PS
function Remove-GoneBranches {
    git branch -vv | where {$_ -match '\[origin/.*: gone\]'} | foreach { 
        git branch -D $_.split(' ', [StringSplitOptions]'RemoveEmptyEntries')[0]
    }
}
Set-Alias rgb Remove-GoneBranches
```

### Better git diff:

```PS
winget install dandavison.delta

git config --global core.pager delta
git config --global interactive.diffFilter 'delta --color-only'
git config --global delta.navigate true
git config --global delta.dark true
git config --global delta.side-by-side true
git config --global merge.conflictStyle zdiff33
```
