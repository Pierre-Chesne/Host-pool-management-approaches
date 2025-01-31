# Host-pool-management-approaches
Actuellement pour gérer le cycle de vie des **hosts** dans un **Host Pool Azure virtual Desktop (AVD)**, cela peut se faire avec plusieurs approches:
- Avec Microsoft Intune
- Avec la création de nouvelles images
- Avec la combinaison des deux

## Avec Microsoft Intune
L'intégration d’Azure Virtual Desktop (AVD) avec Microsoft Intune permet de gérer les machines virtuelles (hosts) de manière centralisée, en appliquant des stratégies de sécurité, des mises à jour et des configurations aux VMs. Microsoft Intune permet une gestion centralisée des VMs AVD sans nécessiter une **reconstruction régulière des images de VMs (hosts AVD)**.

## Avec la création de nouvelles images
La gestion des machines AVD avec de nouvelles images permet d'éviter la dette technique (mise à jour des applications) et de garantir des performances stables. Cela nécessite de recréer régulièrement des images de VMs (hosts AVD) pour appliquer les mises à jour et les application. Cela peut être fait avec des outils comme **Azure Image Builder ou Packer (HashiCorp)** ou **Azure DevOps**.


## Avec la combinaison des deux
Utiliser Intune si l'on veut une gestion continue et éviter de recréer les VMs fréquemment.<br>
Utiliser la création de nouvelles images si l'on veut garantir des performances stables et minimiser une dette technique sur le long terme.<br>
Il est possible de combiner les deux approches pour bénéficier des avantages de chacune. Utiliser Intune pour les petits changements et une nouvelle image tous les 3-6 mois pour une base propre.<br>
C'est souvent cette option qui est recommandée et utilisée pour les environnements de production.
