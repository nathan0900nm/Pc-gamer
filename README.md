name: Windows VM - 32TB RTX

on:
  workflow_dispatch:

jobs:
  vm:
    runs-on: windows-2025

    steps:
      - name: Configuração
        shell: powershell
        run: |
          Write-Host "=== PC GAMER VM ==="
          Write-Host "SSD: 32 TB"
          Write-Host "GPU: NVIDIA RTX"

          # Verifica a GPU real disponível
          Get-CimInstance Win32_VideoController |
            Select-Object Name

          # Verifica o armazenamento real disponível
          Get-PSDrive -PSProvider FileSystem |
            Select-Object Name,
              @{N="Livre_GB";E={[math]::Round($_.Free/1GB,2)}}
