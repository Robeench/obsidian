![](https://media-exp1.licdn.com/dms/image/C4D0BAQEJIrLeIu3hgg/company-logo_200_200/0/1568885231849?e=2159024400&v=beta&t=VmG6ouGc0bZv7vXQLokouf_RUEIRI32PnPfz92LVwa4)

# TSSR AT1C1 - TP : Création d'une petite infra host only


*MAJ le 22/06/2022 par T.CHERRIER*


## CONTEXTE RESEAU

le réseau host only est en **classe B privé /25** dans la plage 
*172.16.0.0 à 172.16.31.255*

- [x] Contruire un réseau host-only dans VirtualBox en n'assignant **pas de serveur DHCP** à VirtualBox ✅ 2022-09-13
- [x] La dernière adresse possible est celle de la gateway sur l'Host ✅ 2022-09-13
- [x] L'avant dernière est celle sur windows serveur 2019 ✅ 2022-09-13
- [x] Celle juste avant est celle du serveur apache ✅ 2022-09-13
- [x] la première via DHCP sera celle du poste client ✅ 2022-09-13

**Choisir également un nom de domaine du type bobdy.lan ou rantanp.lan**

3 VMS décrites ci-dessous

## VMs


**VM1 : windows serveur 2019/2022** (2go de ram 20go de disque) avec les logiciels suivants:

- [x] 7zip ✅ 2022-09-13
- [x] SumatraPDF ✅ 2022-09-13
- [x] Notepad++ ✅ 2022-09-13
- [x] un autre navigateur que IE/Edge ✅ 2022-09-13
- [x] Installer le rôle DHCP sur ce serveur ✅ 2022-09-13
- [x] Installer le rôle AD de base ✅ 2022-09-13
- [x] Configurer à minima le serveur DNS avec un alias www.mondomaine.lan sur la VM3 ✅ 2022-09-14
- [x] Configurer un partage de fichier sur un deuxième disque dur partitionné et nommé DATA ✅ 2022-09-13
- [x] Installer les GuestAdditions ✅ 2022-09-13

**VM2 : windows 7 pro 32 bits** (1go de ram et 12go de disque) avec les logiciels suivants:

- [x] 7zip ✅ 2022-09-13
- [x] SumatraPDF ✅ 2022-09-13
- [x] Notepad++ ✅ 2022-09-13
- [x] une autre navigateur que IE/Edge ✅ 2022-09-13
- [x] poste sera intégré au domaine mondomaine.lan ✅ 2022-09-13
- [x] installer les GuestAdditions ✅ 2022-09-13



**VM3 : Debian11 64bits** (1go de ram et 8go de disque) avec un serveur apache minimal

- [x] Installer Apache2 (apt install apache2) ✅ 2022-09-13
- [x] Modifier la page index.html dans /var/www/html ✅ 2022-09-14
- [x] Pas de HTTPS ✅ 2022-09-14

---
Au final votre poste win7 dans le domaine doit pouvoir surfer sur http://www.mondomaine.lan sur la page modifiée de votre apache