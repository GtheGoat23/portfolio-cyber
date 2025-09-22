Titre :  Root-Me – UUDecode : Cryptanalyse (1)
Plate-forme : Root me 
Catégorie : Cryptanalyse
Difficulté : facile
Score : 5


Objectif
Décoder un fichier encodé en UU (UUEncode / uudecode) pour extraire la chaîne/secret caché.

Contexte et collecte d'informations
Cible/URL : défi Root-Me (bloc uuencode fourni)
Observation : le fichier contient un bloc UU classique (en-tête "begin <mode> <filename>" et "end"). Le contenu décodé semble contenir un mot de passe ou une indication.

Démarche / Étapes
1. Sauvegarder le bloc UU tel quel dans un fichier local (ex : challenge.uu).  
2. Utiliser un outil de décodage UU :
   - Python :
     ```python
     import uu
     uu.decode('challenge.uu', 'decoded.txt')
     ```
3. Ouvrir `decoded.txt` pour lire le texte résultant.  


Résultat observé
Le décodage produit le texte :
Détails techniques
Outils : `uudecode` (commande), module Python `uu`, éditeur de texte (vim, nano, VSCode).  
Format : UUEncode — encodage 6 bits en caractères imprimables, prédécesseur de certains autres formats d’encodage texte.

Cause profonde et vulnérabilité
Il ne s'agit pas d'une vulnérabilité serveur dans ce cas mais d'un exercice de récupération d'information embarquée. L’analyse montre l’importance de reconnaître les formats d’encodage/encapsulation courants (UU, Base64, etc.). Si des secrets sont distribués en clair encodé dans des ressources accessibles, cela constitue une **exposition d’informations sensibles** (CWE-200).

Contre-mesures / Atténuations
- Ne pas stocker de mots de passe/secrets dans des ressources accessibles au client, même encodés.  
- Traiter l’encodage comme une simple transformation de transport, pas comme un chiffrement.  
- Pour les vrais secrets : utiliser un gestionnaire de secrets, chiffrement côté serveur et protocoles d’authentification sûrs.

Leçons apprises
- Savoir identifier rapidement le format d’encodage permet de gagner du temps.  
- UUencode est encore rencontré dans certains CTFs/archives : garder en tête `uudecode` et le module Python `uu`.  
- L'encodage ≠ chiffrement : ne pas confondre.

