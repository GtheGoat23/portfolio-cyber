
cd ~/Bureau/cyber/portfolio_starter/portfolio_starter
mkdir -p docs/ctf/rootme
cat > docs/ctf/rootme/rootme-http-mot-de-passe-faible.md <<'EOF'
# Root-Me – HTTP : Mot de passe faible
**Plate-forme :** Root-Me  
**Catégorie :** Web-Serveur / HTTP  
**Difficulté :** Moyen
**Score :** 10  

## Objectif
Accéder au site protégé en contournant l’authentification grâce à des identifiants par défaut.

## Contexte et collecte d'informations
- **Cible/URL :** Défi Root-Me « Mot de passe faible ».  
- **Observation :** La ressource est protégée par **HTTP Basic Auth** (header `Authorization`).  
- En interceptant la requête, on peut **décoder la valeur Base64** pour lire les identifiants transmis.

## Démarche / Étapes
1. Se connecter au site du challenge dans le navigateur.  
2. Dans **Burp Suite**, intercepter la requête (Proxy → HTTP history).  
3. Ouvrir la requête dans **Repeater** et noter le header :
Authorization: Basic <base64(user:password)>
4. **Décoder** la valeur Base64 pour révéler `user:password` essayés automatiquement par le client → accès refusé.  
5. **Remplacer** ces identifiants par des **identifiants par défaut** `admin:admin`.  
- Récoder en Base64 (ex. `admin:admin` → `YWRtaW46YWRtaW4=`) et remettre la valeur dans `Authorization`.  
6. **Envoyer** la requête modifiée depuis Repeater → accès accordé / mot de passe du challenge obtenu.

## Détails techniques
- **Outils :** Burp Suite (Proxy, Repeater), encodeur/décodeur Base64 intégré.  
- **Actions clés :** Décodage/encodage Base64, modification du header `Authorization`.  

## Cause profonde et vulnérabilité
1. **Identifiants par défaut** non changés (`admin:admin`). → **CWE-521: Weak Password Requirements**.  
2. **Exposition d’informations sensibles** dans les requêtes (Basic Auth décodable ; et si des paramètres sensibles passent en GET, ils finissent dans l’URL, l’historique et les logs). → **CWE-598: Use of GET for Sensitive Data**.  

### Contremesures
- Supprimer/renforcer les credentials par défaut, exiger des mots de passe forts, limiter les tentatives.  
- **Ne jamais** envoyer de données sensibles en GET ; préférer POST et surtout **HTTPS**.  
- Remplacer Basic Auth par un mécanisme robuste (sessions, tokens) et activer TLS strict.

## Leçons apprises
- **Basic Auth ≠ chiffrement** : sans TLS, la valeur Base64 est triviale à lire.  
- Les **mots de passe par défaut** restent une porte d’entrée classique.  
- Éviter d’exposer des identifiants dans les URLs et logs.
