[[Protocole]], [[Active directory]]
# Lightweight Directory Access Protocol (LDAP) 
[[Protocole]] permettant de gérer des annuaires. Il repose sur le [[Modèle TCP IP]]. 

[[Port]] par défaut : 389 pour LDAP
									636 pour LDAP over SSL

Il contient tous les objets de chacune des classes : utilisateurs, ordinateurs, groupes ...
Un annuaire est un ensemble d'entrées, chacune dispose d'un identifiant unique. 

## Modèle de nommage
Identificateur unique global = GUID
Nom unique = Distinguished Name (DN)

exemple de DN : cn=florian,ou=system,ou=informatique,dc=it-connect,dc=local

- DN = nom complet de l'entry, ex : ou=users,dc=cogip,dc=fr
	- RDN (relative distinguished name) = partie du DN relative à l'entry supérieur
	- racine = base de l'arborescence

Ne pas utiliser d'espace. 

## Modèle fonctionnel
services fournit par l'annuaire (recherche, ajout ...)

### La base
DN à partir duquel on fait la recherche

### La portée (scope)
nombre de niveaux sur lesquels l'action va être effectuée

- sub = récursivement de la base sur la totalité de l'arborescence
- one = sur un seul niveau inférieur à la base spécifiée
- base = uniquement sur la base spécifiée

### Les filtres
permet de spécifier des critères de recherche
- égalité  :=
- approximation ~=
- supérieur ou égal >=
- inférieur ou égal <=
- ET :
- OU |
- NON !

``` bash
#combiner plusieurs éléments
(&(objectClass=person)(|(givenName=Jean-Christian)(mail=jranu*)))

#toutes les personnes ayant leur numéro de téléphone renseigné
&(&(objectclass=person)(telephoneNumber=*))

#toutes les personnes dont le nom commence par 'A' et n'habitant pas Paris
&(&(objectclass=person)(cn=A*)(!(l=Paris)))

#toutes les personnes dont le nom ressemble à Febvre (Faivre, Fèvre, Lefebvre, ...)
&(&(objectclass=person)(cn~=febre))
(&(objectclass=person)(cn=*f*vre))

```

### Les opérations

## Modèle d'information

# Ressources 
https://openclassrooms.com/fr/courses/2257706-presentation-du-concept-dannuaire-ldap/
