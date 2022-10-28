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


# Script liste des postes
``` powershell
#Récupérer liste PC via l'AD, avec hostname + statut enable
$ListPc = get-adcomputer -Filter * -SearchBase "OU=SPC-Tours-France,OU=Workstations,OU=_WABTEC-SITES,DC=ad,DC=wabtec,DC=com" -Properties hostname |Select-object hostname

#Exporter vers le csv $listPC
$ListPc | Export-Csv c:\test\listPC_spc.csv -NoTypeInformation -Encoding UTF8 -Delimiter ";" -Append
```

# Script d'inventaire
``` powershell
#Variable reprenant mon fichier avec les PC de SPC
$listPC = "C:\test\listPC_spc.csv"
$output = ($listPC).Substring(0,$listPC.Length-4) + "_result.csv"

New-Item -Path $output -Value "Hostname;Model;OS;Domain;DHCP;IP;Admin;Virtualisation`n" | out-null

#Importer mon fichier
$inventory_spc = Import-Csv $listPC -Delimiter ";" | Select-Object -First 15

#Pour chaque hostname, faire : 
foreach($PC in $inventory_spc.name){

    #Vérification PC allumé avec ping x1
    if (Test-Connection $PC -Count 1 -Quiet) {       
        [array]$CollectInfo = Invoke-Command -ComputerName $PC -ScriptBlock {
            $(hostname)+";"+
            $((Get-CimInstance -ClassName Win32_ComputerSystem).Model)+";"+
            $((Get-WmiObject Win32_operatingsystem).Version)+";"+
            $((Get-CimInstance -ClassName Win32_ComputerSystem).Domain)+";"+ 
            $((Get-NetIPAddress -AddressFamily IPV4 -InterfaceAlias Wi-Fi).PrefixOrigin)+";"+
            $((Get-NetIPAddress -AddressFamily IPV4 -InterfaceAlias Wi-Fi).IPAddress)+";"+ 
            $((Get-LocalGroupMember Administrateurs).Name)+";"+ 
            $((get-service vmware | Where-Object {$_.Status -eq "Running"}).DisplayName)
         }
         Add-Content -Path $output -Value $CollectInfo
      } else {
         Add-Content -Path $output -Value "$PC;NA;NA;NA;NA;NA;NA;NA"
      
      }
        #Ajout de $CollectInfo à mon doc $listPC
        #Add-Content -Path $listPC -Value $CollectInfo
        $CollectInfo | export-csv $output -append -Delimiter ";" -NoTypeInformation
}
```