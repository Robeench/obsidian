XML = fichier de réponse généré
ADK = logiciel qui sert à déployer les installations silencieuses

importer un catalogue via l'ISO de windows 

déclarer les disques (on commence par 0)
partition du disque et format, c'est différent. 
 
Utilisation de Ventoy

# Installation ADK
[Installation ADK sur mon poste](https://docs.microsoft.com/en-us/windows-hardware/get-started/adk-install)

# Compression ISO
Compresser mon ISO avec 7zip
Si le fichier install est en .esd, besoin de le convertir en .wim
[Convertir un fichier ESD en WIM](https://rdr-it.com/convertir-un-fichier-esd-en-wim/)

# Installation Windows 10

# Création du fichier .xml
Assistant gestion d'installation
	- joindre fichier install.wim de l'iso concerné

[Create unattend media installation W10](https://www.windowscentral.com/how-create-unattended-media-do-automated-installation-windows-10)

[Automatiser installation windows](https://www.nextinpact.com/article/29373/107276-automatisons-installation-windows-10-unattended)

[Création automatisée d'un fichier unattend](https://www.windowsafg.com/win10x86_x64_uefi.html)

https://docs.microsoft.com/fr-fr/windows-hardware/customize/desktop/unattend/microsoft-windows-setup-diskconfiguration-disk-createpartitions-createpartition-type

Créer les partitions dans l'ordre : 
- WinRE
- System
- MSR
- Windows

InstallFrom = 
![[VM_60Go.xml_-_Windows_System_Image_Manager_2.jpg]]

[Unattend install W10](https://www.tenforums.com/tutorials/96683-create-media-automated-unattended-install-windows-10-a.html)

Créer un compte administrateur : 
Group = Administrators
créer un compte local : 
Group = Users