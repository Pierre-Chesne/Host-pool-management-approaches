# "Host-pool-management-approaches"
<img width='800' src='./images/img_0-0.png'/><br><br>
Actuellement pour gérer le cycle de vie des **"Session hosts"** dans un **"Host Pool Azure virtual Desktop (AVD)"**, cela peut se faire avec plusieurs approches:
- Avec Microsoft Intune
- Avec la création de nouvelles images
- Avec la combinaison des deux

## Avec Microsoft Intune
L'intégration d’Azure Virtual Desktop (AVD) avec Microsoft Intune permet de gérer les machines virtuelles (Session hosts) de manière centralisée, en appliquant des stratégies de sécurité, des mises à jour et des configurations aux VMs. Microsoft Intune permet une gestion centralisée des VMs AVD sans nécessiter une **reconstruction régulière des images de VMs (hosts AVD)**.

## Avec la création de nouvelles images
La gestion des machines AVD avec de nouvelles images permet d'éviter une dette technique (mise à jour des applications) et de garantir des performances stables. Cela nécessite de recréer régulièrement des images de VMs (Session hosts AVD) pour appliquer les mises à jour et les applications. Cela peut être fait avec des outils comme **"Azure Image Builder ou Packer (HashiCorp)"** ou **"Azure DevOps/ GitHub / ..."**.


## Avec la combinaison des deux
Utiliser Intune si l'on veut une gestion continue et éviter de recréer les VMs fréquemment.<br>
Utiliser la création de nouvelles images si l'on veut garantir des performances stables et minimiser une dette technique sur le long terme.<br>
Il est possible de combiner les deux approches pour bénéficier des avantages de chacune. Utiliser Intune pour les petits changements et faire des nouvelles images tous les 3-6 mois pour une base propre testée et performante.<br>
C'est souvent cette option qui est recommandée et utilisée pour les environnements de production.<br>


## "Host-pool-management-approaches"
Dans le service **"Azure Virtual Desktop"**, les **"host pool"** sont des regroupements logiques de machines virtuelles **"Session hosts"** qui ont la même configuration et servent les mêmes "Workloads". Vous pouvez choisir l'une des deux approches de gestion des pools d'hôtes suivantes : standard et utilisation d'une configuration d'hôte de session (aperçu). Dans cet article, vous découvrirez chaque approche de gestion et les différences qui existent entre elles afin de vous aider à décider laquelle utiliser.

