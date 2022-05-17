# Setup:
1. Open Powershell and execute the following commands:
```
winget install Microsoft.WindowsTerminal
winget install Microsoft.PowerShell
winget install Git.Git
```
2. Install a nice Font from https://www.nerdfonts.com/ (for example HACK is alwas nice!
3. Open Windows Terminal
  1. Set the new font as default for all 
  2. Set the default shell to the newest installed PowerShell
4. Execute the following commands in the windows terminal in the latest powershell:
```
curl https://raw.githubusercontent.com/JanDeDobbeleer/oh-my-posh/main/themes/iterm2.omp.json --output .OhMyPoshTheme.json
winget install oh-my-posh
Install-Module -Name Terminal-Icons -Repository PSGallery
Install-Module -Name z

#Write Imports to your $profile
Add-Content $profile "#Profile Setup done via https://github.com/doenersoldat/setup-powershell"
Add-Content $profile "oh-my-posh init pwsh --config '~/.OhMyPoshTheme.json' | Invoke-Expression"
Add-Content $profile "Import-Module -Name Terminal-Icons"
Add-Content $profile "Import-Module z"
```
5. Done
