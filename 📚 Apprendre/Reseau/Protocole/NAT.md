
# Network Address Translation (NAT)
![[Capture d’écran 2022-05-05 114652.png]]

On utilise le NAT pour économiser le nombre d'adresses [[IPv4]].
On utilise des adresses [[IP]] privées pour les communications en interne et des adresses publiques seulement pour communiquer avec internet. Dans l'image, on économise 3 adresses [[IP]] publiques. 

## Port Address Translation (PAT)

![[Capture d’écran 2022-05-05 115156.png]]

La passerelle alloue dynamiquement un [[port]] à chaque communication pour qu'au retour, les réponses sur chaque [[port]] dédié sera renvoyé à la bonne machine. 