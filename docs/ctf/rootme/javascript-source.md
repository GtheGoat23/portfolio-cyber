---
titre: "Root-Me – Javascript : Source"
platform: "Root-Me"
category: "Web-Client"
difficulty: "Facile"
score: "5"
---

## Objectif
Trouver le mot de passe.

## Contexte & Info Gathering
- Cible/URL : challenge Root-Me
- Observation : le code source contient des commentaires ou variables exposant le mot de passe.

## Démarche / Étapes
1. Ouvrir la page challenge.
2. Faire `Ctrl+U` (View Source) ou ouvrir DevTools -> Sources.
3. Rechercher le code.
4. Copier sa valeur, le noter comme preuve et le soumettre.

## Détails techniques
- Outils : navigateur, View Source, DevTools.
- Commandes : n/a (interface graphique).

## Root cause & Vulnérabilité
Données sensibles laissées dans le code source (commentaires/variables).  
**CWE-200 (Information Exposure)**.


## Contremesures / Mitigations
- Nettoyer le code avant déploiement.
- Gérer secrets côté serveur.

## Leçons apprises
- La lecture du code source reste la première étape d’un audit web.
