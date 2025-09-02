---
title: "Root-Me – Javascript : Authentication (2)"
platform: "Root-Me"
category: "Web-Client"
difficulty: "Moyen"
score: "10"
---

## Objectif
Identifier des identifiants stockés côté client mais difficiles à repérer.

## Contexte & Info Gathering
- Cible/URL : challenge Root-Me
- Observation : la logique d'authentification est dans un script JS, mais l'info n'est pas visible immédiatement (obfuscation/encodage simple).

## Démarche / Étapes
1. Ajouter à l'URL le 'login.js'
2. Télécharger le fichier JS 
3. Trouver le mot de passe dans le fichier JS
4. Récupérer identifiant/mot de passe et tenter la connexion.

## Root cause & Vulnérabilité
Secrets embarqués côté client, parfois masqués par obfuscation légère — contournable.
CWE-200.

## Contremesures / Mitigations
Ne pas stocker secrets côté client.
Utiliser méthodes d’authent sécurisées côté serveur.

## Leçons apprises
L'obfuscation côté client n'est pas une protection ; un attaquant peut facilement déobfusquer ou décoder.
