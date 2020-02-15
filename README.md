# PowerShell `innoextract`

Downloads the latest version of [`innoextract`](https://github.com/dscharrer/innoextract)
to `inno.exe`.

```powershell
$response = Invoke-WebRequest -Uri https://github.com/dscharrer/innoextract/releases/latest
$match = $response.Content | Select-String -Pattern '[\d\.]+\/innoextract-[\d\.]+-windows\.zip'
$url = "https://github.com/dscharrer/innoextract/releases/download/" + $match.Matches[0].Value
Invoke-WebRequest -Uri $url -OutFile inno.zip
Expand-Archive -LiteralPath inno.zip -DestinationPath inno -Force
Remove-Item –path inno.zip
Move-Item inno/innoextract.exe inno.exe -Force
Remove-Item –path inno –Recurse
```

## Running

```powershell
& .\inno.ps1
```
