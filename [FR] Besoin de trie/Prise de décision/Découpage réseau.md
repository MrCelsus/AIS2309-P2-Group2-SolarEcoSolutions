
| Decoupage VLAN 10.100.ID_Vlan.x/24 | ADRESSE RESEAU | BROADCAST   | Début de plage | Fin de plage  |
| ---------------------------------- | -------------- | ----------- | -------------- | ------------- |
| **LAN**                            |                |             |                |               |
| R&D                                | 1              | 10.110.1.0  | 10.110.1.1     | 10.110.1.254  |
| DG                                 | 2              | 10.110.2.0  | 10.110.2.1     | 10.110.2.254  |
| DAF                                | 3              | 10.110.3.0  | 10.110.3.1     | 10.110.3.254  |
| Commerciaux                        | 4              | 10.110.4.0  | 10.110.4.1     | 10.110.4.254  |
| IT                                 | 5              | 10.110.5.0  | 10.110.5.1     | 10.110.5.254  |
| Production                         | 6              | 10.110.6.0  | 10.110.6.1     | 10.110.6.254  |
| Logistique Expédition              | 7              | 10.110.7.0  | 10.110.7.1     | 10.110.7.254  |
| Maintenance                        | 8              | 10.110.8.0  | 10.110.8.1     | 10.110.8.254  |
| Atelier                            | 9              | 10.110.9.0  | 10.110.9.1     | 10.110.9.254  |
| DMZ                                | 10             | 10.110.10.0 | 10.110.10.1    | 10.110.10.254 |
| Serveurs                           | 11             | 10.110.11.0 | 10.110.11.1    | 10.110.11.254 |
| Imprimante                         | 12             | 10.110.12.0 | 10.110.12.1    | 10.110.12.254 |
| Equipement réseau                  | 13             | 10.110.13.0 | 10.110.13.1    | 10.110.13.254 |
| Admin                              | 14             | 10.110.14.0 | 10.110.14.1    | 10.110.14.254 |
| **Réseau WIFI**                    |                |             |                |               |
| R&D Wifi                           | 15             | 10.110.15.0 | 10.110.15.1    | 10.110.15.254 |
| DG Wifi                            | 16             | 10.110.16.0 | 10.110.16.1    | 10.110.16.254 |
| DAF Wifi                           | 17             | 10.110.17.0 | 10.110.17.1    | 10.110.17.254 |
| Commerciaux Wifi                   | 18             | 10.110.18.0 | 10.110.18.1    | 10.110.18.254 |
| IT Wifi                            | 19             | 10.110.19.0 | 10.110.19.1    | 10.110.19.254 |
| Production Wifi                    | 20             | 10.110.20.0 | 10.110.20.1    | 10.110.20.254 |
| Logistique Expédition Wifi         | 21             | 10.110.21.0 | 10.110.21.1    | 10.110.21.254 |
| Maintenance Wifi                   | 22             | 10.110.22.0 | 10.110.22.1    | 10.110.22.254 |
| Atelier Wifi                       | 23             | 10.110.23.0 | 10.110.23.1    | 10.110.23.254 |
| DMZ Wifi                           | 24             | 10.110.24.0 | 10.110.24.1    | 10.110.24.254 |
| Serveurs Wifi                      | 25             | 10.110.25.0 | 10.110.25.1    | 10.110.25.254 |
| Imprimante Wifi                    | 26             | 10.110.26.0 | 10.110.26.1    | 10.110.26.254 |
| Equipement réseau Wifi             | 27             | 10.110.27.0 | 10.110.27.1    | 10.110.27.254 |
| Admin Wifi                         | 28             | 10.110.28.0 | 10.110.28.1    | 10.110.28.254 |
| **Réseau WIFI INVITE**             |                |             |                |               |
| WiFi Guest                         | 29             | 10.110.29.0 | 10.110.29.1    | 10.110.29.254 |
### Explication du choix du découpage VLAN

1. **Séparation des départements** :
   Chaque département a son propre VLAN. Cela permet d'isoler le trafic réseau, réduisant ainsi les risques de collision de données et améliorant la sécurité. Par exemple, les données sensibles du département IT sont séparées de celles du département commercial.

2. **Amélioration de la sécurité** :
   En isolant les réseaux des différents départements, il est plus facile de mettre en place des politiques de sécurité spécifiques à chaque VLAN. Par exemple, le VLAN des serveurs peut avoir des règles de pare-feu strictes pour protéger les données critiques.

3. **Gestion simplifiée** :
   L'utilisation de VLANs permet une gestion plus facile et plus efficace du réseau. Chaque VLAN peut être administré de manière indépendante, ce qui simplifie le dépannage et la maintenance.

4. **Performance du réseau** :
   Le découpage en VLANs réduit la taille des domaines de broadcast, ce qui diminue la quantité de trafic de diffusion sur le réseau et améliore les performances globales.

5. **Flexibilité** :
   L'utilisation de VLANs offre une grande flexibilité en termes de configuration du réseau. Les utilisateurs et les ressources peuvent être déplacés facilement d'un VLAN à un autre sans avoir besoin de reconfigurer physiquement le réseau.

6. **Réseaux WiFi dédiés** :
   La séparation des réseaux WiFi pour chaque département assure que le trafic sans fil est également isolé, offrant une meilleure performance et sécurité pour les utilisateurs WiFi.

7. **Réseau invité** :
   Un VLAN séparé pour les invités (WiFi Guest) permet de fournir un accès internet aux visiteurs sans compromettre la sécurité du réseau interne.

En résumé, le découpage en VLAN tel que présenté dans le tableau permet une gestion optimale du réseau en termes de sécurité, performance, flexibilité et maintenance.
