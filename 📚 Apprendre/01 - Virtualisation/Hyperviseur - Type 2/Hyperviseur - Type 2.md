= hosted hypervisor
= hyperviseur hébergé

Adapté pour de petites infrastructures, pour une seule machine et faire des tests multiplateformes.

S'installe comme une application système et permet de créer des VM indépendantes de l'[[OS]] hôte. Il est donc considéré comme n’importe quelle application et n’a aucune priorité sur les ressources de l’hôte.

En revanche, chaque VM est autorisée, par l’hyperviseur, à utiliser une certaine quantité de ressources (définie au départ) et ne peut donc pas dépasser cette limite. L’OS hôte ne pourra donc pas être ralenti par les VM, si elles ont été configurées raisonnablement.

Les utilisations d’un hyperviseur de type 2 sont multiples. Ils sont assez faciles à mettre en place et très efficaces pour répondre aux besoins du type :
-   tester un OS sans formater votre machine physique ;
-   tester ou utiliser régulièrement une application sur un OS en particulier ;
-   simuler une 2e machine et faire des tests de communication simples ;
-   créer un petit réseau de plusieurs VM pour tester des protocoles réseau, des règles de pare-feu, configurer un serveur de supervision ou autre.

## Exemples
- Hyper V
- VMWare Workstation
- VirtualBox
