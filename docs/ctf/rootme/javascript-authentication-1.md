---
title: "Root-Me – Javascript : Authentication (1)"
platform: "Root-Me"
category: "Web-Client"
difficulty: "Facile"
score: "5"
---

## Objectif
Trouver identifiant/mot de passe.

## Contexte & Info Gathering
- Cible/URL : challenge Root-Me (page login)
- Observation : la page charge un fichier JS (ex: login.js) qui peut contenir la logique d'authentification.

## Démarche / Étapes
1. Ouvrir la page et ajouter à l’URL ‘login.js’.
2. Télécharger/ouvrir le fichier JS :
Extraire l’identifiant / mot de passe trouvés dans le fichier JS et les utiliser sur le formulaire.

## Détails techniques
Outils : navigateur, curl/wget, éditeur/less

## Root cause & Vulnérabilité
Mauvaise gestion des secrets : données sensibles embarquées dans un fichier client accessible publiquement.
CWE-200 (Information Exposure).

## Contremesures / Mitigations
Ne jamais stocker secrets/crédentiels côté client.
Valider authentification côté serveur et utiliser authentification sécurisée.

## Leçons apprises
Toujours vérifier les scripts chargés par la page ; tout fichier JS côté client est visible par l'attaquant.
