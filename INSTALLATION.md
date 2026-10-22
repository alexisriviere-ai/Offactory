# Installer OF FACTORY sur plusieurs PC

Version Windows 64 bits : **2.2.17**. Les installateurs sont distribués dans les [publications OF FACTORY](https://github.com/alexisriviere-ai/Offactory/releases).

## Sur chaque ordinateur

1. Télécharger **OF-Factory-Setup-2.2.17.exe** dans les fichiers de la publication, ou copier ce même fichier sur une clé USB.
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

Les étiquettes affichent directement le chantier, le repère libre, les dimensions, les piquages et la mention Isolé / Non isolé. Le logo est agrandi de 10 %. Le compteur est masqué pour une quantité de 1 ; la désignation commerciale et le numéro OF répété en bas sont retirés.

Pour une quantité multiple, cocher **Un repère libre par plénum** afin de saisir un emplacement différent pour chaque exemplaire. Les compteurs **1/3, 2/3, 3/3** restent automatiques. Les nouveaux logos Midea, Mitsubishi Electric, Daikin, Toshiba et Mitsubishi Heavy Industries sont préparés en noir et blanc pour l’impression thermique.

Pour retirer un logo de la bibliothèque, cliquer sur sa corbeille dans le menu **Étiquettes**, puis confirmer la suppression.

## Retrait de l’isolant

Les consignes de retrait sont appliquées automatiquement. Pour un besoin particulier, cocher **Modifier la valeur de retrait** et saisir la cote en millimètres dans le configurateur ou les plaques d’isolant du panier. Décocher la case pour retrouver la consigne automatique.

## Tôle 6000 × 1500

Ce format représente deux tôles de **3000 × 1500 mm** jointives. Le placement respecte chaque tôle physique et empêche toute pièce de chevaucher la jonction à **3000 mm**. La séparation est visible dans les aperçus et les plans PDF.

## Gaine rectangulaire

Dans le menu principal, ouvrir **Gaine rectangulaire**, choisir la famille de pièce puis saisir ses dimensions. Les vues se recalculent automatiquement. Les coudes proposent des talons droits et un rayon intérieur réglable ; **R = 0** conserve un angle intérieur droit avec un extérieur courbe.

Ajouter, dupliquer ou supprimer les pièces selon le besoin. **Exporter le PDF** produit une page par repère, avec sa quantité, dans un fichier vectoriel compressé. Le poids du fichier est affiché avant export. Les pièces sont enregistrées dans l’atelier et incluses dans ses sauvegardes.

Les familles proposées comprennent aussi **Manchette souple** (largeur A, hauteur B, profondeur P), **Bouchon rectangulaire**, **Bouchon grillagé** et **Piquage rectangulaire**. Pour les bouchons, régler A, B et la hauteur HT, fixée à 30 mm par défaut ; le fond grillagé propose une maille réglable. Pour le piquage, régler A, B, la profondeur C et le bord tombé BT, fixé à 20 mm par défaut. **P1** est un type de cadre / profil, sélectionnable dans Cadre 1.

Les cadres sélectionnés sont dessinés en perspective. Les transformations rectangle / rond portent les cotes C/F en face, D/G en dessus et les quatre repères en isométrie. Pour les coudes transformés, l’arrondi extérieur rejoint une partie droite ; les talons D/E et le rayon intérieur restent réglables.

## Prix de vente installateur

Dans les configurateurs **Gainable** et **Grille**, le pied de page affiche le **prix installateur unitaire HT**. Le montant suit les dimensions, les piquages, le bord tombé, l’isolation intérieure et l’épaisseur de tôle. La quantité saisie en haut de l’écran détermine le total.

L’épaisseur choisie en pied de page est aussi celle de la fabrication. Le prix de vente est sauvegardé avec le plénum et recalculé à sa réouverture. Le calcul utilise les tarifs de vente directement, sans classeur Excel à ouvrir ni prix de revient intégré.

Pour un évasement en largeur, la matière est facturée sur les dimensions maximales, chutes comprises, et la part main-d’œuvre est majorée de **20 %**. Le barème couvre le galva **0,6 / 0,7 / 0,8 / 1,2 / 1,5 mm** ; les autres épaisseurs affichent **Prix à confirmer**.
