
### Procédure Complète de Mise en Place

#### Matériel Nécessaire
- **Routeur Dual-WAN** compatible avec deux connexions Internet (WAN) pour gérer à la fois la fibre et la 4G.
- **Box 4G** : Orange Airbox 4G Home.

#### Étapes de Configuration

1. **Connexion des Connexions Internet** :
   - Connectez votre connexion fibre optique au port WAN 1 du routeur Dual-WAN.
   - Connectez la box 4G au port WAN 2 du routeur.

2. **Accéder à l'Interface de Gestion du Routeur** :
   - Accédez à l'interface web de gestion du routeur en entrant son adresse IP dans un navigateur web.
   - Connectez-vous avec vos identifiants administrateur.

3. **Configurer le Basculement (Failover)** :
   - Recherchez les paramètres WAN dans l'interface de gestion.
   - Configurez WAN 1 comme connexion principale (fibre optique) et WAN 2 comme connexion de secours (box 4G).
   - Activez la fonctionnalité de basculement (failover). Dans la plupart des routeurs, il y a une option spécifique pour cela.

4. **Définir les Critères de Basculement** :
   - Configurez les critères de basculement, tels que la détection de la perte de connexion sur la fibre optique (ping, absence de réponse, etc.).
   - Assurez-vous que le basculement se fait automatiquement et instantanément dès que la connexion principale est perdue.

5. **Tester la Configuration** :
   - Déconnectez temporairement la connexion fibre optique pour vérifier que la box 4G prend le relais.
   - Assurez-vous que la connexion revient à la fibre une fois que celle-ci est rétablie.

6. **Documenter et Former** :
   - Documentez la configuration et les étapes de dépannage.
   - Formez le personnel technique sur la gestion du basculement et la résolution des problèmes éventuels.

### Conclusion
La mise en place d'un basculement automatique avec un routeur dual-WAN garantit que votre connexion 4G prendra immédiatement le relais en cas de coupure de la fibre optique, assurant ainsi une continuité de service essentielle pour les opérations de votre entreprise.
