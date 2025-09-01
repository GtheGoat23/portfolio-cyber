# Rapport d'audit – Découverte du réseau local (Nmap)
 
**Auditeur :** Kabre Gerald  
**Scope :** Réseau virtuel 192.168.136.0/24  
**Méthodologie :** Reconnaissance initiale (OSSTMM/PTES)

---

## 1. Résumé exécutif
Un scan de découverte a été effectué sur le sous-réseau virtuel de la machine Kali.  
Résultats principaux :  
- 4 hôtes détectés sur le réseau.  
- Service DNS identifié en `192.168.136.2` (port 53 ouvert).  
- Les autres hôtes ont des ports filtrés ou fermés.  
- La machine locale (Kali) n’expose aucun service critique.

**Recommandation prioritaire :** analyser le service DNS et restreindre l'accès si nécessaire.

---

## 2. Contexte & Périmètre
- **Actifs évalués :** réseau local virtuel VMware (192.168.136.0/24)  
- **Contraintes/Assomptions :** environnement pédagogique (aucun système de production)  
- **Environnement :** Kali Linux (VM) – Nmap 7.95

---

## 3. Commande exécutée
```bash
sudo nmap -sV 192.168.136.0/24

4. Résultats (synthèse)
IP	Service détecté	Commentaire
192.168.136.1	Aucun (ports filtrés)	Gateway VMware
192.168.136.2	DNS (53/tcp)	Service DNS actif, à surveiller
192.168.136.254	Aucun (ports filtrés)	VMware internal
192.168.136.130	Aucun	VM Kali locale, pas de service exposé


5. Analyse & recommandations

Le service DNS en 192.168.136.2 est la piste principale : vérifier sa configuration (bind/named), la version, et rechercher des CVE liées si service exposé.

Les hôtes avec ports filtrés indiquent la présence d’un pare-feu ou d’un filtrage réseau ; vérifier les règles et les logs pour comprendre quelles connexions sont autorisées/filtrées.

Prochaines étapes recommandées : tests DNS (dig, dnsenum), scan plus fin sur la machine .2 (versions, scripts NSE), vérification des logs systèmes.


6. Annexes

Sortie brute du scan : docs/logs/nmap_scan.log                               
