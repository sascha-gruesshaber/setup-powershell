# How to setup my nice PowerShell on Windows:
![image](https://user-images.githubusercontent.com/11362893/168903228-b8a9c969-f259-4549-bb6b-93ea8d80d99a.png)

1. Open current powershell and execute the following commands:
```
winget install Microsoft.WindowsTerminal
winget install Microsoft.PowerShell
# winget install Git.Git
```
2. Install a nice font from https://www.nerdfonts.com/
    - Hack NF is a nice one for example 
3. Open Windows Terminal and ...
    - ... set the new font as default for all shells in the settings
    - ... set the default shell to the newest installed PowerShell in the settings
    - ... set transparency
    STRG+SHIFT+, -> 
    ```
    "profiles": 
    {
        "defaults": 
        {
            "font": 
            {
                "face": "Hack NF",
                "size": 10
            },
            "opacity": 87,
            "useAcrylic": true
        },
        ...
     ```
4. Execute the following commands in the windows terminal in the latest powershell:
```
Write-Host "Installing Oh My Posh", Terminal-Icons and z..."
winget install oh-my-posh
Install-Module -Name Terminal-Icons -Repository PSGallery
Install-Module -Name z

Write-Host "Download a nice theme for Oh My Posh and save it locally"
curl https://raw.githubusercontent.com/JanDeDobbeleer/oh-my-posh/main/themes/powerlevel10k_rainbow.omp.json --output .OhMyPoshTheme.json

Write-Host "Write imports to your $profile"
Add-Content $profile "#Profile Setup done via https://github.com/doenersoldat/setup-powershell"
Add-Content $profile "oh-my-posh init pwsh --config '~/.OhMyPoshTheme.json' | Invoke-Expression"
Add-Content $profile "Import-Module -Name Terminal-Icons"
Add-Content $profile "Import-Module z"
Exit
```
5. Restart your Windows Terminal, it should look a lot nicer now :-)
