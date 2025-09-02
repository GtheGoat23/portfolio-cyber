---
title: "Root-Me – Javascript : Obfuscation (1)"
platform: "Root-Me"
category: "Web-Client"
difficulty: "Moyen"
score: "10"
---

## Objectif
Trouver et déchiffrer un mot de passe encodé/obfusqué dans le code client.

## Contexte & Info Gathering
- Cible/URL : challenge Root-Me
- Observation : le script JS est obfusqué (noms de variables incompréhensibles, chaînes encodées).

## Démarche / Étapes
1. Récupérer le script obfusqué .
2. Isoler la chaîne encodée et la décoder :

## Root cause & Vulnérabilité
Utilisation d'obfuscation faible pour masquer des secrets côté client. Non sécurisée pour protéger des secrets.
CWE-200.



## Contremesures / Mitigations
Les secrets doivent être stockés côté serveur.
Si obfuscation utilisée pour IP/URL, accompagner de contrôles serveur.

## Leçons apprises
Savoir utiliser des outils de décodage pour permettre d'analyser rapidement du JS obfusqué.
