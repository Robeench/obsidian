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