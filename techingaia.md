**Rapport d'Intervention – Rétablissement de l'Accès aux Services Email et Backoffice**

---

**Client :** ADOMOS

**Date de l'Intervention :** Du 5 au 6 novembre 2024

---

### Objet de l'Intervention

Dans le cadre de cette mission, j’ai été sollicité pour restaurer l'accès aux services email et backoffice de votre infrastructure, actuellement indisponibles, afin de vous permettre de retrouver un fonctionnement opérationnel.

---

### Déroulement de l'Intervention

1. **Connexion et Diagnostic Initial**

   Après réception de l'archive technique et des clés d'accès fournies, j'ai tenté de me connecter aux serveurs suivants :

   - **Serveur de production** (`ps1`, `ns236904.ip-37-59-32.eu`) : Connexion réussie.
   - **Premier serveur de backup** (`pve2`, `ns3067913.ip-217-182-174.eu`) : Connexion échouée.
   - **Second serveur de backup** (`pve3`, `ns3107430.ip-54-37-87.eu`) : Connexion échouée.

   En l’absence de connexion aux serveurs de backup, j’ai constaté qu’il n’existait plus de copies de sauvegarde pour les services de production (et du serveur de comptabilité).

2. **Constat des Dysfonctionnements**

   Lors de la vérification des services essentiels, les observations suivantes ont été faites :

   - **Serveur de messagerie** (`https://mx.extranet-cgp.net`) : Connexion échouée.
   - **Serveur de backoffice** (`http://bo.adomos.com`) : Connexion échouée.

   Sur le serveur de production, j’ai identifié que le stockage des sauvegardes des machines virtuelles (VM) avait comme conséquence l'occupation de l’intégralité du disque de 2,4 To, bloquant ainsi plusieurs tâches en arrière-plan ainsi que le fonctionnement des machines virtuelles.

3. **Libération d'Espace Disque et Redémarrage**

   J’ai entrepris les actions suivantes pour remédier au manque d’espace disque :

   - Suppression des sauvegardes antérieures à 2024, permettant de libérer environ 450 Go.
   - Redémarrage du serveur de production pour réinitialiser les tâches suspendues.

4. **Redémarrage des Services**

   Après le redémarrage, j’ai procédé au relancement des machines virtuelles. Cependant, la VM du serveur de mail ne démarrait pas en raison de l’expiration du certificat du domaine `mx.extranet-cgp.net`. Pour contourner cette contrainte, j’ai désactivé la vérification de la validité du certificat au démarrage du service, permettant ainsi le redémarrage et la remise en route du service.

   À l'issue de ces interventions, les services email et backoffice ont été restaurés, et le serveur dispose actuellement de l’espace disque suffisant pour fonctionner de manière normale.

---

### Problèmes Identifiés et Préconisations

**1. Absence de Backup Externe du Serveur de Production :**

- **Impact** : La sécurité des données et la pérennité des services sont à risque sans copie de sauvegarde externe.
- **Préconisation** : Restaurer la liaison avec un serveur de backup déporté ou mettre en place une solution de sauvegarde externe afin d’assurer la protection des données.

**2. Rotation de l’Espace Disque :**

- **Impact** : Bien que non critique à court terme, l’espace disque pourrait de nouveau se saturer si la collecte et suppression des sauvegardes sur le serveur de production ne sont pas automatisées.
- **Préconisation** : Mettre en place un système de rotation des sauvegardes ou de collecte périodique pour éviter une saturation récurrente de l’espace disque.

**3. Gestion des Comptes de Messagerie :**

- **Impact** : Le nombre important de comptes email actifs augmente le risque de spam et de surcharge du serveur.
- **Préconisation** : Considérer une solution en mode SaaS pour la messagerie, tout en conservant le serveur actuel comme archive pour les anciens emails, facilitant ainsi la gestion des utilisateurs actifs et des risques liés au spam.

---

### Conclusion

L’intervention a permis de rétablir l'accès aux services critiques de votre infrastructure. Les préconisations listées ci-dessus visent à pérenniser ce rétablissement et à optimiser la sécurité et la gestion des ressources de votre infrastructure.

Je reste à votre disposition pour toute action supplémentaire ou pour répondre à vos questions sur les étapes de ce rapport.

---

**Signature** :  
Le 06/11/2024, David KEITA

## Tech in Gaïa
