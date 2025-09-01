# Rapport d'audit – Configuration Burp Suite
 
**Auditeur :** Kabre Gerald  
**Scope :** Préparation de l'environnement d'audit applicatif (Burp Suite + Firefox)  
**Méthodologie :** Mise en place et validation d'outil

---

## 1. Résumé exécutif
Burp Suite a été configuré pour intercepter et analyser le trafic HTTP/HTTPS. Le proxy local fonctionne, le certificat CA a été importé dans Firefox, et les extensions utiles pour les tests sont installées.

---

## 2. Contexte & Périmètre
- **Actifs :** navigateur Firefox (sur VM Kali), Burp Suite Community  
- **Objectif :** préparer un environnement sûr pour effectuer des tests applicatifs (interception/modification de requêtes)

---

## 3. Étapes réalisées (configuration)
1. Configuration du proxy Firefox → `127.0.0.1:8080` (HTTP & HTTPS).  
2. Récupération du certificat CA via la page interne Burp (`http://burp`) et import dans Firefox :  
   - Firefox → Settings → Privacy & Security → Certificates → View Certificates → Authorities → Import → cocher **Trust this CA to identify websites**.  
3. Installation via Extender → BApp Store :  
   - Logger++ (journalisation des requêtes)  
   - Autorize (test contrôles d'accès)  
   - JWT Editor (manipulation tokens JWT)  
   - Jython : configuré  pour les extensions

---

## 4. Résultats
- Proxy Burp interceptant : confirmé.  
- HTTPS : pas d’erreur de certificat après import du CA.  
- Extensions : installées et prêtes à l'emploi pour tests (Logger++, Autorize, JWT Editor).

---

## 5. Analyse & recommandations
- Burp est prêt pour du test applicatif (scan DAST, manipulation de requêtes, tests d'accès). 

