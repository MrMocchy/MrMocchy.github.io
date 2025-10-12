
# Random

## CPU温度確認

```powershell title="PowerShell (管理者権限)"
(Get-WmiObject MSAcpi_ThermalZoneTemperature -Namespace "root/wmi")[0].CurrentTemperature / 10 - 273.15
```
環境によっては`[0]`が不要か、または他のインデックスが正しいかも。
