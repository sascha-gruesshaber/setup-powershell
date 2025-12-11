# How to setup my PowerShell:
![image](https://user-images.githubusercontent.com/11362893/168903228-b8a9c969-f259-4549-bb6b-93ea8d80d99a.png)

1. Open current powershell and execute the following commands:
```PS
winget install Microsoft.WindowsTerminal
winget install Microsoft.PowerShell
winget install Git.Git
winget install -e --id=JesseDuffield.lazygit

# Install a mono font to be used in the windows terminal
winget install --id=DEVCOM.JetBrainsMonoNerdFont  -e
```

2. Open up windows terminal and setup the newly installed nerd font as default

3. Execute the following commands in the windows terminal in the latest powershell:
```PS
Install-Module -Name Terminal-Icons -Repository PSGallery
Install-Module -Name z

winget install JanDeDobbeleer.OhMyPosh --source winget

Write-Host "Write startp config to your local user `$profile`"
Add-Content $profile "#Profile Setup done via https://github.com/sascha-gruesshaber/setup-powershell"
Add-Content $profile "oh-my-posh init pwsh | Invoke-Expression"
Add-Content $profile "Import-Module -Name Terminal-Icons."
Add-Content $profile "Import-Module z"
```
4. Restart your Windows Terminal, it should look a lot nicer now :-)

## Additional things:

### Remove gone branches
```PS
function Remove-GoneBranches {
    git branch -vv | where {$_ -match '\[origin/.*: gone\]'} | foreach { 
        git branch -D $_.split(' ', [StringSplitOptions]'RemoveEmptyEntries')[0]
    }
}
Set-Alias -Name rgb Remove-GoneBranches
```

### Shortcut for lazygit
```PS
Set-Alias -Name lg -Value "lazygit"
```

### Config für lazygit
```yml
os:
  edit: 'code {{filename}}'
gui:
  nerdFontsVersion: "3"
customCommands:
  - key: '<c-u>'
    context: 'localBranches'
    description: 'Remove all gone branches from local git repository (no healthy upstream branches)'
    command: 'pwsh -command "rgb"'
  - key: '<c-n>'
    description: 'Create a new branch following our naming conventions'
    context: 'localBranches'
    prompts:
      - type: 'menu'
        title: 'Kind of branch?'
        key: 'BranchType'
        options:
          - name: 'feature'
            description: 'a feature branch'
            value: 'feature'
          - name: 'bugfix'
            description: 'a bug fix branch'
            value: 'bug'
      - type: 'input'
        title: 'Ticket number?'
        key: 'BranchName'
        initialValue: 'XYZ-'
    command: "git checkout -b {{.Form.BranchType}}/{{.Form.BranchName}}"
    loadingText: 'Creating branch "{{.Form.BranchType}}/{{.Form.BranchName}}"'
```
