**Plate-forme :** Root-Me  
**Catégorie :** Client Web / Web-Serveur  
**Difficulté :** Moyen
**Score :** 10

## Objectif
Afficher le flag en contournant la vérification du hash lors de la redirection de l’URL.

## Contexte et collecte d'informations
- **Cible/URL :** Défi Root-Me CH52 (page web-serveur)  
- **Observation :** La page génère un hash pour sécuriser la redirection (`url=<URL>&h=<HASH>`), mais celui-ci reste identique même si l’URL change côté client.  

## Démarche / Étapes
1. Ouvrir Burp Suite et activer le **Proxy / Intercept**.  
2. Accéder à la page cible (ex. `https://facebook.com`) depuis le navigateur.  
3. Intercepter la requête avec Burp Suite.  
4. Modifier l’URL : remplacer `facebook.com` par `google.fr`.  
5. Noter que le **hash reste le même**.  
6. Calculer le hash MD5 de la nouvelle URL (`google.fr`) .  
7. Passer dans **Repeater**, envoyer la requête modifiée (`Send`).  
8. Le flag apparaît dans le code source retourné par le serveur.

## Détails techniques
- **Outils :** Burp Suite, Navigateur (Firefox/Chrome)  
- **Commandes clés :** Proxy Intercept, Repeater, modification des paramètres d’URL  
- **Technique :** Contournement de la logique côté serveur via manipulation d’URL et hash statique  

## Cause profonde et vulnérabilité
- Le serveur **ne valide pas correctement le hash** côté backend.  
- **CWE-295 / Logic Flaw côté serveur** : la sécurité repose sur une valeur côté client prévisible.  
- Contremesures : recalculer le hash côté serveur et valider toute redirection.

## Leçons apprises
- La sécurité côté client est insuffisante.  
- Burp Suite permet d’intercepter et de manipuler les requêtes pour tester la logique serveur.  
- Toujours vérifier la logique de validation côté serveur pour éviter des fuites de données.

