# Script PowerShell - Inventaire

- SNMP
- agent

## IP
`(Get-NetIPAddress -AddressFamily IPV4 -InterfaceAlias Wi-Fi).IPAddress`

## DHCP ou Manual
`(Get-NetIPAddress -AddressFamily IPV4 -InterfaceAlias Wi-Fi).PrefixOrigin`

## Nom
`(Get-CimInstance -ClassName Win32_ComputerSystem).Name`

## Modèle
`(Get-CimInstance -ClassName Win32_ComputerSystem).Model`

## Domaine
`(Get-CimInstance -ClassName Win32_ComputerSystem).Domain`

## Membres du groupe administrateurs
`(Get-LocalGroupMember Administrateurs).Name` 

## Virtualisation
Afficher les VM d'HyperV
`Get-VM`

``` PowerShell
$ListPc = get-adcomputer -Filter * -SearchBase "OU=SPC-Tours-France,OU=Workstations,OU=_WABTEC-SITES,DC=ad,DC=wabtec,DC=com" -Properties name,OperatingSystem,OperatingSystemVersion,Enabled | Select-Object  name,OperatingSystem,OperatingSystemVersion,enabled  
$ListPc | Export-Csv c:\test\listPc4Bene.csv -NoTypeInformation -Encoding UTF8 -Delimiter ";"
```

``` PowerShell

#définir où je récupère l'information dans l'AD
$Where = "OU=SPC-Tours-France,OU=Workstations,OU=_WABTEC-SITES,DC=ad,DC=wabtec,DC=com" 

#Paramètres de ma recherche
$Params = @
	"SearchBase" = $Where
	"Filter" = name,enabled

#Définit la liste
$List = Get-ADcomputer @Params

$List | Foreach-Object
	[PSCustomObject]@
		"Hostname" = $_.Name
		"Statut" = $_.Enabled

#il manque un truc qui lui dit de chercher dans chaque PC en boucle
$Hostname = hostname
$OS = (Get-WmiObject Win32_operatingsystem).Version
$Model = (Get-CimInstance -ClassName Win32_ComputerSystem).Model
$Area = (Get-CimInstance -ClassName Win32_ComputerSystem).Domain
$DHCP = (Get-NetIPAddress -AddressFamily IPV4 -InterfaceAlias Wi-Fi).PrefixOrigin
	if ($DHCP = "Manual")
	{
	$IP = (Get-NetIPAddress -AddressFamily IPV4 -InterfaceAlias Wi-Fi).IPAddress
	}
$Admin = (Get-LocalGroupMember Administrateurs).Name
$Virtu = (get-service windowsxpmode,vmware | Where-Object {$_.Status -eq "Running"}).DisplayName

#export csv
$Inventory | Export-Csv c:\test\inventaire.csv -NoTypeInformation -Encoding UTF8 -Delimiter ";"

```

```PowerShell
#Création fichier vierge CSV
New-Item -ItemType File -Path "C:\Test\inventory.csv"

#Ajout en-tête au fichier .csv
Add-Content -Path "C:\Test\inventory.csv" -Value "Hostname;Model;OS;Domain;DHCP;IP;Admin;Virtualisation"

#Ajout information
Add-Content -Path "C:\Test\inventory.csv" -Value "$(hostname);$((Get-CimInstance -ClassName Win32_ComputerSystem).Model);$((Get-WmiObject Win32_operatingsystem).Version);$((Get-CimInstance -ClassName Win32_ComputerSystem).Domain);$((Get-NetIPAddress -AddressFamily IPV4 -InterfaceAlias Wi-Fi).PrefixOrigin);$((Get-NetIPAddress -AddressFamily IPV4 -InterfaceAlias Wi-Fi).IPAddress);$((Get-LocalGroupMember Administrateurs).Name);$((get-service windowsxpmode,vmware | Where-Object {$_.Status -eq "Running"}).DisplayName)"
```