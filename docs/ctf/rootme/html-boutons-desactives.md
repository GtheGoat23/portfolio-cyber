---
titre: "Root-Me – HTML : Boutons désactivés"
platform: "Root-Me"
category: "Web-Client"
difficulty: "Facile"
score: "5"
---

## Objectif
Contourner un formulaire HTML dont les champs et le bouton sont désactivés côté client pour trouver le mot de passe.

## Contexte & Info Gathering
- Cible/URL : challenge Root-Me (page formulaire)
- Observation : le champ input et le bouton de soumission ont l'attribut `disabled` dans le DOM.

## Démarche / Étapes
1. Ouvrir la page challenge dans le navigateur.
2. Ouvrir DevTools (Inspect Element).
3. Identifier l'élément `<input>` et le bouton `<button>` qui possèdent `disabled`.
4. Dans la console ou panel Elements, supprimer l'attribut `disabled` et le remplacer par enabled
Soumettre → le serveur renvoie le mot de passe.

## Détails techniques
Outils : Navigateur (Firefox/Chrome), DevTools
Commandes clés : modification DOM via console.

## Root cause & Vulnérabilité
Sécurité implémentée côté client seulement. L'attribut disabled n'empêche pas une requête valide d'être envoyée au serveur.
CWE-693 / CWE-598 (server trusts client-side controls).
Contremesures / Mitigations
Toujours vérifier et valider côté serveur.
Rejeter les entrées non autorisées côté backend.

## Leçons apprises
Ne pas se fier aux protections côté client.
