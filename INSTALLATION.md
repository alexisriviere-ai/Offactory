# Installer OF FACTORY sur plusieurs PC

Version Windows 64 bits : **2.2.20**. Les installateurs sont distribués dans les [publications OF FACTORY](https://github.com/alexisriviere-ai/Offactory/releases).

## Sur chaque ordinateur

1. Télécharger **OF-Factory-Setup-2.2.20.exe** dans les fichiers de la publication, ou copier ce même fichier sur une clé USB.
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

Les étiquettes structurées affichent directement le chantier, le repère libre, les dimensions, les piquages et la mention Isolé / Non isolé. Le logo est agrandi de 10 %. Le compteur est masqué pour une quantité de 1 ; la désignation commerciale et le numéro OF répété en bas sont retirés.

Pour une quantité multiple, cocher **Un repère libre par plénum** afin de saisir un emplacement différent pour chaque exemplaire. Les compteurs **1/3, 2/3, 3/3** restent automatiques. Les nouveaux logos Midea, Mitsubishi Electric, Daikin, Toshiba et Mitsubishi Heavy Industries sont préparés en noir et blanc pour l’impression thermique.

Pour retirer un logo de la bibliothèque, cliquer sur sa corbeille dans le menu **Étiquettes**, puis confirmer la suppression.

## Création d’étiquettes sans nesting

Ouvrir **Création d’étiquettes** depuis le menu principal et choisir une source :

1. **Fichier d’étiquettes** : charger un Excel, CSV ou JSON. Depuis l’écran habituel des étiquettes du nesting, utiliser **Enregistrer le fichier Excel** ou **Enregistrer le fichier JSON** pour conserver le lot et ses repères individuels.
2. **Lecture d’un OF** : choisir un PDF contenant du texte, puis contrôler les quantités, dimensions, piquages et isolation. Les informations non reconnues restent à compléter. Cette lecture sert uniquement aux étiquettes et ne crée pas de pièces de fabrication. Les PDF scannés nécessitent une saisie ou une conversion préalable en texte.
3. **Saisie manuelle** : composer directement les étiquettes dans l’éditeur libre.

Le tableau permet de modifier ou supprimer les lignes, de valider les lignes complètes et de sélectionner uniquement celles qui sont prêtes. Le lot est enregistré automatiquement sur le PC et inclus dans les sauvegardes de l’atelier. Excel et JSON permettent de garder plusieurs lots.

### Textes et styles libres

Les nouvelles étiquettes manuelles ouvrent directement l’éditeur libre. Pour personnaliser une étiquette existante, ouvrir **Modifier** puis activer **Textes et styles libres**.

Tous les textes, y compris « Repère », « Dimensions », « Isolé » et le compteur, peuvent être remplacés ou supprimés. Les caractères spéciaux et les retours à la ligne sont conservés. Sélectionner des mots dans la zone de texte pour changer leur police, taille, **gras**, *italique* ou souligné ; sans sélection, le style s’applique au bloc entier. Les polices proposées sont des suggestions : un autre nom de police installée sur le PC peut être saisi.

Ajouter, dupliquer ou supprimer les blocs, régler leurs positions, dimensions et alignements, puis choisir si le logo doit apparaître. Les boutons **Insérer le repère**, **Insérer le numéro** et **Insérer le total** ajoutent des valeurs variables facultatives pour chaque exemplaire.

Le cadre orange indique la sélection et ne s’imprime pas. Un débordement dans le format **100 × 50 mm** doit être corrigé avant impression. L’aperçu et l’impression graphique conservent les styles choisis. Une police absente du PC est remplacée par le système.

Pour conserver la mise en forme, enregistrer le lot en **Excel ou JSON**. Garder la feuille **Mise en page** du fichier Excel ; un CSV ne conserve pas les styles libres. Sur un autre PC, choisir de nouveau le logo s’il manque dans sa bibliothèque.

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

## Assemblage chantier

Ouvrir **Assemblage chantier** depuis le menu principal ou le lien au-dessus des fiches de gaines rectangulaires.

1. Cliquer sur **Reprendre mes fiches**, ou importer leur PDF OF FACTORY ou leur export JSON. La quantité de chaque repère est conservée ; chaque exemplaire est placé séparément.
2. Créer un **Volume machine** aux dimensions réelles, puis ajouter ses raccords sur les faces locales X+/X−, Y+/Y− ou Z+/Z−. Les décalages sont mesurés depuis le centre de la face.
3. Sélectionner une pièce cible et son raccord libre, puis cliquer sur **Placer**. Un raccord compatible s’aimante automatiquement. Les points blancs indiquent les raccords libres ; les points pleins indiquent les liaisons.
4. Déplacer les pièces dans les vues ou saisir leur position X/Y/Z. Les pièces déjà raccordées se déplacent ensemble. Les rotations utilisent les axes du chantier par pas de 45° ou 90° ; une rotation qui ouvrirait un raccord est refusée. **Décrocher** permet de réorienter une pièce. Déverrouiller un volume fixé pour déplacer son ensemble.
5. Ajouter au besoin une gaine ou un coude rectangulaire, un accessoire circulaire, ou un piquage circulaire sur une gaine droite.
6. Vérifier les erreurs, les alertes et les raccords libres, puis exporter **Plan PDF**. Le PDF A3 vectoriel contient les quatre vues, les dimensions des pièces, les quantités, les liaisons et les contrôles.

La sauvegarde locale est automatique. **Sauver le projet** produit un JSON transportable contenant les fiches, les positions et les liaisons. Importer ce JSON pour reprendre un autre chantier ; une confirmation précède le remplacement du chantier ouvert. **Supprimer**, **Annuler** et **Rétablir** permettent de corriger le montage.

Cette première version reconnaît les PDF de fiches OF FACTORY contenant du texte, sans OCR ni déduction automatique du montage depuis un plan. Les accessoires créés dans l’assemblage apparaissent dans sa nomenclature, sans création automatique d’une fiche de fabrication. Les alertes de collision portent sur l’encombrement des pièces, hors cadres et isolation ; les profils de cadre 20/30 mm sont contrôlés séparément sur les raccords. Le piquage sur face garde une marge de 20 mm au bord d’une gaine droite. Limites : 2 000 fiches et 500 éléments placés.
