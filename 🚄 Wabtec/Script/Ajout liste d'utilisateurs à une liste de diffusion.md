
``` powershell
#Installation du module d'accès à ExchangeOnlineManagement
Install-Module -Name ExchangeOnlineManagement

#Importer le module dans le script
Import-Module ExchangeOnlineManagement

#S'authentifier
Connect-ExchangeOnline -UserPrincipalName itadm_leroux@wabtec.com

#Import de la liste et ajout à la liste de diffusion
$import = Import-Csv "C:\temp\users_vad.csv"
$import | foreach { 
    try {
		write-host ajout de $_.email
		Add-DistributionGroupMember -Identity "FAV-users_vad@wabtec.com" -Member $_.email -ErrorAction Stop -ErrorVariable errorajout
    }
    catch { 
	    Write-Host "erreur:" $_.exception.message -ForegroundColor Red
	}
}
```