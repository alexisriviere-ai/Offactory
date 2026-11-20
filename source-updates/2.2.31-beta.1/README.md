# OFactory 2.2.31-beta.1 — compte rendu de développement

Base : copie locale des sources 2.2.30, provenant du dossier de travail `workshop-2.2.13` (son nom historique ne correspond plus à la version du package). Le dépôt GitHub public `alexisriviere-ai/Offactory`, examiné à partir du commit `483418b`, contient la distribution et sa documentation, pas les sources de l’application. La branche de revue fournit donc un **correctif source applicable à la base 2.2.30**, avec contrôle préalable, plutôt qu’une publication intégrale des sources, des catalogues ou des matrices commerciales.

## Fonctionnalités réalisées

- Formulaire commun aux deux modules : client existant ou nouveau, chantier existant ou nouveau et nom facultatif de fabrication. Entrée et bouton utilisent le même traitement. Échap annule. La fenêtre reste ouverte en cas d’échec. La transaction serveur et son identifiant de requête empêchent les créations répétées.
- Registre persistant commun clients → chantiers → fabrications ; filtrage par client et chantier, dates de création et de modification visibles. Plusieurs chantiers par client et plusieurs fabrications par chantier. Les noms identiques normalisés sont réutilisés ; une case explicite autorise une raison sociale réellement distincte et les homonymes sont différenciés par un extrait d’identifiant.
- Les deux modules ouvrent les mêmes fabrications. Le premier passage vers Assemblage reprend les fiches et leurs identifiants. La réouverture actualise l’inventaire et son ordre ; les pièces déjà placées, leurs positions, dimensions et connexions ne sont pas recalculées automatiquement.
- Boutons gauche/droite pour la pièce sélectionnée. Le tableau sauvegardé porte l’ordre et les exports PDF, JSON, CSV et inventaires le suivent. Aucune cote n’est changée et aucun raccord n’est créé par le déplacement.
- Contrôle dimensionnel facultatif BÊTA séparé des calculs de fabrication : coude transformé possible, sections incompatibles sur une liaison explicitement enregistrée, section très atypique parmi un groupe suffisamment homogène de gaines droites. Détails, cotes et champs à vérifier ; pictogrammes ; avertissements ignorables ; état daté conservé. Une modification dimensionnelle invalide le contrôle. Dans Assemblage, une modification des raccords l’invalide également.
- Export supplémentaire de vues statiques par pièce, A4 paysage, entièrement vectoriel et compressé : trois pièces simples ou deux pièces complexes par page ; trois ou quatre vues selon la famille. Géométries partagées avec Assemblage, notamment pour les profils de coudes et les transitions rectangle/rond. Les traits de facettisation lisses des coudes ne sont pas imprimés comme des plis.
- Les fiches détaillées conservent leurs cotes et leur composition. Client, chantier et dates sont ajoutés aux documents ; le CSV achat reçoit aussi les identités. Aucun objet 3D interactif, capture haute résolution ou image lourde n’est intégré.

## Persistance et migration

La base reste `data/database.json`. Le registre ajoute `OfClients`, `OfSites`, `OfFabrications` et `OrganizationVersion`, sans supprimer les anciennes collections. Les relations utilisent des UUID et les fabrications possèdent des liens vers les identifiants et clés des documents de chaque module. Les documents nouvellement rattachés portent aussi `organization` pour les exports JSON.

La migration est idempotente et réalisée dans la file de transactions existante, avec écriture temporaire puis renommage atomique. Avant la première transaction migrée, une copie non écrasable du fichier précédent est créée : `data/database.before-organization-v1.json`. Les sauvegardes complètes de l’atelier conservent les nouvelles données.

Les anciennes affaires sont conservées séparément et marquées « À attribuer ». Deux anciennes clés `main`, une par module, ne sont jamais supposées être la même fabrication. Aucune identité client ou chantier n’est déduite d’un ancien libellé. Une date ancienne connue est conservée ; une date absente reste inconnue. Le bouton « Attribuer client / chantier » permet la correction manuelle et enregistre d’abord les modifications en attente. Les anciennes pièces et leurs caractéristiques ne sont pas réécrites par la migration.

## Principaux fichiers

| Fichiers | Rôle |
| --- | --- |
| `server/work-organization.mjs`, `server/local-api.mjs` | Migration, registre, transactions, liaison des modules et création idempotente |
| `public/gaine-rectangulaire/organization.mjs`, `organization.css` | Navigation et formulaire partagés |
| `public/gaine-rectangulaire/app.mjs`, `index.html` | Intégration des affaires, ordre manuel et interface BÊTA |
| `public/gaine-rectangulaire/part-order.mjs`, `coherence.mjs` | Modules indépendants d’ordre et de contrôle |
| `src/pages/AssemblyWorkshop.jsx`, `RectangularDuct.jsx` | Intégration Assemblage et échange sécurisé avec le module embarqué |
| `src/lib/assembly/part-pdf.mjs` | Nouvel export de vues isolées utilisant le moteur existant |
| `src/lib/assembly/model.mjs`, `pdf.mjs` | Conservation des identités et de l’ordre ; en-têtes |
| `public/gaine-rectangulaire/engine.mjs`, `purchase-ui.mjs` | Ajout des identités aux documents, sans modification des formules |
| `server/work-organization.test.mjs`, `scripts/test-organization-ui.mjs`, `scripts/audit-test-pdfs.py` | Tests et contrôle des PDF |
| `package.json`, `package-lock.json` | Version de travail 2.2.31-beta.1 ; aucune dépendance de production ajoutée |

## Validation effectuée

- `npm test` : **249 tests réussis**, dont 243 tests existants et 6 nouveaux tests regroupant les cas de migration, dates, créations répétées, ordre, contrôle dimensionnel et PDF.
- Tests ciblés gaines/assemblage/organisation : **29 réussis**.
- `npm run build` : compilation réussie. Avertissements Vite de taille des bundles et d’imports statiques/dynamiques conservés ; aucun échec de compilation.
- `npm run lint` : réussi.
- Tests réels dans Edge sans fenêtre, sur une base temporaire : **14 scénarios réussis**, aucune erreur JavaScript. Entrée dans les deux modules, souris, Échap, validations répétées, échec de sauvegarde simulé et reprise, plusieurs chantiers/fabrications, avertissement ignoré, attribution manuelle d’une ancienne affaire, ordre et dates après rechargement, liens communs entre modules et téléchargement effectif des deux PDF.
- Audit des cinq PDF de test : pages contenant texte et tracés vectoriels, aucune image raster, pas de page blanche ou texte hors page détecté, repères de l’export navigateur dans l’ordre coude puis gaine. Les bornes numériques de toutes les vues de l’échantillon sont également testées. Toutes les pages des exemples par famille ont été rendues ; les mises en page simples, complexes et détaillées ont été revues visuellement.

| PDF de test | Pièces | Pages | Octets | Taille décimale approximative |
| --- | ---: | ---: | ---: | ---: |
| Vues 3D, 12 familles | 12 | 5 | 36 636 | 36,6 ko |
| Vues 3D, lot de 100 pièces complexes | 100 | 50 | 772 519 | 0,773 Mo |
| Fiches détaillées, 12 familles | 12 | 12 | 41 282 | 41,3 ko |
| Vues 3D téléchargées par l’interface | 2 | 1 | 10 628 | 10,6 ko |
| Fiches détaillées téléchargées par l’interface | 2 | 2 | 7 949 | 7,9 ko |

Les mesures peuvent varier légèrement avec la date d’édition et les libellés. Aucun test d’impression sur une imprimante physique ni d’envoi à un serveur de messagerie n’a été effectué.

## Limites de la BÊTA

Un coude de sections différentes est une **suspicion**, car le modèle ne distingue pas une intention « égal » d’une intention « transformé ». Une incompatibilité de sections n’est signalée comme telle que sur une liaison connue, avec les sections fournies par le moteur d’assemblage et sa tolérance existante. L’ordre du listing n’est jamais utilisé pour inventer une connexion.

Le contrôle atypique se limite aux gaines droites : au moins cinq éléments, dont au moins 75 % proches de la surface médiane ; seuls les rapports extrêmes de surface supérieurs à neuf sont suggérés. Aucun débit, dimensionnement aéraulique, supportage ou conformité réglementaire n’est déduit. Les plans PDF sont des représentations de compréhension, sans calcul d’occultation photoréaliste. La vérification est un état à un instant donné : après une modification de l’assemblage dans un autre écran, relancer le contrôle dans Fabrication pour y examiner les nouvelles connexions.

Une ancienne fabrication et un ancien assemblage restent deux archives distinctes tant qu’un lien explicite n’a pas été établi. Leur attribution au même client/chantier ne fusionne pas leurs contenus. La reprise d’une fabrication dans Assemblage conserve les anciens assemblages séparés et ne les écrase pas.

## Reproduire les vérifications

Depuis les sources de l’application après application du correctif :

```powershell
npm ci
npm test
npm run build
npm run lint
```

Pour le navigateur, installer Playwright dans l’environnement de développement, puis exécuter `node scripts/test-organization-ui.mjs`. Le script accepte `OF_PLAYWRIGHT_MODULE` (chemin vers `playwright/index.mjs`) et `OF_BROWSER_EXECUTABLE` (chemin vers Edge ou Chromium). Exemple Windows :

```powershell
$env:OF_BROWSER_EXECUTABLE = 'C:\Program Files (x86)\Microsoft\Edge\Application\msedge.exe'
node scripts/test-organization-ui.mjs
```

Pour l’audit complémentaire : installer PyMuPDF dans l’environnement de test, puis `python scripts/audit-test-pdfs.py`. Les PDF et résultats sont générés dans `test-artifacts/`, avec uniquement des données fictives. Ces dépendances de test ne sont pas intégrées au logiciel Windows.

## Préparation et déploiement Windows

1. **Faire une copie du dossier complet des sources 2.2.30**, puis appliquer le correctif de la branche de revue avec `git apply --check chemin\ofactory-2.2.31-beta.1.patch`, puis `git apply chemin\ofactory-2.2.31-beta.1.patch`. Arrêter si le contrôle signale une base différente ; ne pas forcer une application partielle. Ne pas appliquer ce patch au petit dépôt de distribution seul.
2. Exécuter les tests et la compilation ci-dessus dans cette copie. Le code modifié est déjà disponible dans la copie de développement livrée avec le rapport.
3. Sur le poste de construction Windows, exécuter `npm run dist:win` après validation de la BÊTA. Cette commande prépare un installateur **sans publication** (`--publish never` dans le script existant). L’installateur n’a pas été fabriqué pendant cette mission.
4. Sur un poste pilote, fermer OFactory et sauvegarder `%APPDATA%\OFFactory\data` et le dossier de sauvegardes complet. Installer la BÊTA manuellement ; conserver le même dossier de données. Vérifier les affaires migrées puis attribuer leurs clients/chantiers lorsque nécessaire. Contrôler une impression réelle à l’échelle usuelle.
5. Faire valider le poste pilote et la BÊTA avant toute distribution aux autres postes. Les bases restent locales à chaque PC ; cette évolution ne crée pas de synchronisation réseau.
6. Pour un retour arrière, fermer l’application et restaurer la sauvegarde complète prise avant essai. Ne pas remplacer seulement la base par l’instantané de migration si des fabrications ont été ajoutées depuis : conserver aussi ces nouvelles données pour leur récupération.

Aucune release GitHub, mise à jour automatique de production, installation sur un poste utilisateur ou fusion sur `main` n’est effectuée par ce correctif.
