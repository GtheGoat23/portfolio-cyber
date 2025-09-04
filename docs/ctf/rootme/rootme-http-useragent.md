
# Root-Me – HTTP : User-Agent
**Plate-forme :** Root-Me  
**Catégorie :** Web-Serveur / HTTP  
**Difficulté :** Moyen 
**Score :** 10  

## Objectif
Exploiter le header HTTP `User-Agent` pour contourner le filtrage et obtenir le mot de passe.

## Contexte et collecte d'informations
- **Cible/URL :** Défi Root-Me HTTP – User-Agent (serveur ch2)  
- **Observation :** La page semble vérifier la valeur du header `User-Agent`.  
- En consultant l’historique des requêtes interceptées, on remarque que la réponse varie selon le client déclaré.  

## Démarche / Étapes
1. Se connecter au site du challenge depuis le navigateur.  
2. Dans Burp Suite, ouvrir l’**Historique HTTP** pour observer la requête envoyée.  
3. Sélectionner cette requête et l’envoyer dans **Repeater**.  
4. Modifier le header `User-Agent` en remplaçant sa valeur par `admin`.  
5. Relancer la requête.  
6. La réponse renvoie directement le mot de passe.

## Détails techniques
- **Outils :** Burp Suite (Proxy, Repeater)  
- **Commandes clés :** Modification des headers HTTP  
- **Technique :** Usurpation de l’`User-Agent` pour simuler l’accès administrateur  

## Cause profonde et vulnérabilité
- Le serveur se base uniquement sur la valeur du header `User-Agent` pour autoriser l’accès.  
- **CWE-290 : Authentication Bypass Using Spoofing**  
- Contremesures :  
  - Ne pas utiliser les en-têtes HTTP comme mécanisme d’authentification.  
  - Implémenter une authentification serveur robuste (sessions, tokens).  

## Leçons apprises
- Les en-têtes HTTP sont **facilement manipulables** avec des outils comme Burp Suite.  
- Il ne faut jamais se fier à des valeurs fournies par le client pour contrôler l’accès.  
- Ce type de challenge illustre une **faille logique triviale**, mais encore fréquente sur des applis mal sécurisées.

