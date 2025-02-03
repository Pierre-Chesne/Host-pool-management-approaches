# "Host-pool-management-approaches"
<img width='800' src='./images/img_0-0.png'/><br><br>
Actuellement pour gérer le cycle de vie des **"Session hosts"** dans un **"Host Pool Azure virtual Desktop (AVD)"**, cela peut se faire avec plusieurs approches:
- Avec Microsoft Intune
- Avec la création de nouvelles images
- Avec la combinaison des deux

## Avec Microsoft Intune
L'intégration d’Azure Virtual Desktop (AVD) avec Microsoft Intune permet de gérer les machines virtuelles (Session hosts) de manière centralisée, en appliquant des stratégies de sécurité, des mises à jour et des configurations aux VMs. Microsoft Intune permet une gestion centralisée des VMs AVD sans nécessiter une **reconstruction régulière des images de VMs (hosts AVD)**.

## Avec la création de nouvelles images
La gestion des mises à jour des machines AVD avec de nouvelles images permet d'éviter une dette technique (mise à jour des applications) et de garantir des performances stables. Cela nécessite de recréer régulièrement des images de VMs (Session hosts AVD) pour appliquer les mises à jour et les applications. Cela peut être fait avec des outils comme **"Azure Image Builder ou Packer (HashiCorp)"** et des chaînes de déploiement tel que **"Azure DevOps/ GitHub / ..."**.<br><br>
Avec cette approche, on est obligé de gérer les mises à jour des sessions hosts soit en **créant un nouveau "Host pool"** avec les nouvelles images ou soit **en ajoutant des nouveaux "Session host" à un "Host pool"** avec les nouvelles images.<br><br>
**Création d'un nouveau "Host pool"**:<br>
- Crétion d'une nouvelle image en la stockant dans **"Azure Compute Gallery"**
- Redéploiement d'un "Host pool" avec la nouvelle image
- Nettoyage de l'Entra ID ou de l'Acive Directory (comptes machine)
- Re création d'**Application group & "Assignments"**

**En ajoutant des nouveaux "Session host" à un "Host pool"**:<br>
- Crétion d'une nouvelle image en la stockant dans **"Azure Compute Gallery"**
- Génération d'une nouvelle clé au niveau du **"Host pool"** pour l'ajout des nouveaux **Session host**
- Déploiement des nouveaux **Session host**
- Jouer avec le "Drain mode"
- Une fois les nouveaux **Session host** déployés il faudra nettoyage de l'Entra ID ou de l'Acive Directory (comptes machine)


## Avec la combinaison des deux
Utiliser Intune si l'on veut une gestion continue et éviter de recréer les VMs fréquemment.<br>
Utiliser la création de nouvelles images si l'on veut garantir des performances stables et minimiser une dette technique sur le long terme.<br>
Il est possible de combiner les deux approches pour bénéficier des avantages de chacune. Utiliser Intune pour les petits changements et faire des nouvelles **images tous les 3-6 mois** pour une base propre testée et performante.<br>
C'est souvent cette option qui est recommandée et utilisée pour les environnements de production.<br>


## "Host-pool-management-approaches"
Microsoft propose maintenant une nouvelle fonctionnalité dans **"Azure Virtual Desktop"** pour le déploiement des "Host pool" et surtout pour la gestion du cycle de vie des **Session host**. Cette nouvelle fonctionnalité **"Host pool management approaches"** est encore en **preview** et ne fonctionne uniquement dans un environnement **"Domaine Active Directory ou Microsoft Entra Domain Services"**. Egalement, **elle n'est supporté qu'en mode "Pooled" pour "Host pool"**.<br><br>
Les prérequis pour déployer cette nouvelle fonctionnalité:<br>
- Active Directory avec Entra Domain Services ou domaine ADDS et des permissions spécifiques sur l’OU ( des "Session host)" dans le cas ADDS
- Uniquement des systèmes d'exploitation Windows 10/11 en Gen 2
- KeyVault pour stocker les login et mot de passe (compte pour mettre les machines session host dans le domaine ainsi compte admin local session host). Ainsi il faudra autoriser le déploiement de « template ARM » au niveau du KeyVault
- Rôles:
    - "Desktop Virtualization Virtual Machine Contributor" pour le principal de service AVD
    - "KeyVault secret user" pour le principal de service AVD
    - "KeyVault administrator" pour l’administrateur sécurité en charge de gérer les secrets
    - Propriétaire ou contributeur sur le groupe de ressources ou la souscription hébergeant les hôtes de sessions
    
    Pour déployer et gérer le cycle de vie avec cette nouvelle fonctionnalité **"Host pool management approaches"**, c'est très simple <br>
    Dans l'assitant pour créer un nouveau Host pool, on voit la nouvelle fonctionnalité<br><br>
    <img width='800' src='./images/img_0-1.png'/><br><br>
    On choisit l'image (MarketPlace ou une image dans une Gallery)<br><br>
    <img width='800' src='./images/img_0-2.png'/><br><br>




 

