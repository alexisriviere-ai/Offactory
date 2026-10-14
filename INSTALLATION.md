# Installer OF FACTORY sur plusieurs PC

Version Windows 64 bits : **2.2.10**. Les installateurs sont distribués dans les [publications OF FACTORY](https://github.com/alexisriviere-ai/Offactory/releases).

## Sur chaque ordinateur

1. Télécharger **OF-Factory-Setup-2.2.10.exe** dans les fichiers de la publication, ou copier ce même fichier sur une clé USB.
2. Ouvrir le fichier et terminer l’installation. Aucun Node.js ni Python n’est nécessaire.
3. Lancer **OF FACTORY** depuis le raccourci du Bureau ou le menu Démarrer.
4. L’atelier s’ouvre directement sans PIN. Pour reprendre une version locale existante, importer son atelier avant de commencer à créer des chantiers.

Chaque PC garde ses propres chantiers, panier, réglages, logos et documents. Les données ne se synchronisent pas.

Cet installateur ne possède pas de certificat de signature Windows. Windows peut afficher un avertissement de provenance ; la publication de référence est celle de ce dépôt.

## Reprendre un atelier existant

Avant de créer un nouveau nom/PIN, ouvrir **Fichier → Importer mon atelier existant…**, puis choisir le dossier **data** de la version locale OF FACTORY. L’import reprend le profil, les chantiers, le panier, les réglages, les logos, les repères et les documents. Le dossier d’origine est conservé.

Pour démarrer les autres PC avec une copie du même atelier, copier le dossier **data** complet sur une clé USB et importer cette copie avant leur première utilisation. Chaque PC travaille ensuite indépendamment. Un atelier déjà initialisé ne sera pas remplacé par cet import initial.

## Mises à jour

OF FACTORY recherche les nouvelles versions au démarrage puis toutes les quatre heures. Le téléchargement se fait en arrière-plan. Une indication apparaît lorsqu’une mise à jour est prête : enregistrer les pièces en cours puis cliquer sur **Installer et redémarrer**, ou fermer normalement l’application.

**Aide → Rechercher une mise à jour** lance une vérification immédiate. OF FACTORY reste utilisable hors connexion.

Les données restent dans `%APPDATA%\OFFactory\data`. Une sauvegarde est créée avant une mise à jour dans `%APPDATA%\OFFactory\sauvegardes`. Le menu **Fichier** permet d’ouvrir ces dossiers.

## Étiquettes Zebra

Installer le pilote Windows ZPL de la Zebra GX430T et brancher l’imprimante en USB sur le même PC qu’OF FACTORY. Dans **Étiquettes**, choisir le logo et l’imprimante, puis vérifier les repères avant l’impression sur des étiquettes de **100 × 50 mm**.
