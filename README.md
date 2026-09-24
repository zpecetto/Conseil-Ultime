# Conseil-Ultime

Assistant de loisirs n8n avec Telegram, Ollama, Data Tables et Google Drive. Le workflow fourni coordonne les recommandations de livres, musique, films, séries, jeux vidéo et jeux de société à partir des collections disponibles.

## Workflow

[Conseil Ultime.json](Workflow/Conseil%20Ultime.json) contient 42 nœuds : préparation de la demande, chargement des tables utiles, construction du contexte, outils spécialisés, statistiques en JavaScript, agent Ollama, mémoire de conversation et réponse Telegram découpée en messages.

| Outil spécialisé | Sources |
|---|---|
| Conseil livres | Tables BD, Roman et Audible |
| Conseil musique | Catalogue de fichiers Google Drive |
| Conseil films | Table Film |
| Conseil séries | Table Serie |
| Conseil jeux vidéo | Table Jeux vidéo |
| Conseil jeux de société | Table Jeux de société |

Les calculs et recherches structurés sont exécutés dans les outils Code. Les règles de recommandation distinguent possession, lecture/visionnage et souhaits selon les colonnes disponibles. Les métadonnées absentes des tables ne doivent pas être interprétées comme connues.

## Installation

1. Importer le JSON dans n8n et le laisser désactivé pendant la configuration.
2. Créer ou sélectionner les sept tables décrites dans [DataTables/README.md](DataTables/README.md). Les CSV livrés contiennent uniquement leurs en-têtes, sans données personnelles.
3. Reconnecter chaque nœud **Read ...** à sa table dans le même projet n8n.
4. Dans **Google Drive - Count files** et **Google Drive Tool**, renseigner le dossier du catalogue musical et les credentials Google Drive.
5. Configurer les credentials Ollama et disposer du modèle `qwen2.5:7b` repris dans l’export, ou adapter le nœud à votre modèle compatible avec les outils.
6. Configurer Telegram sur le déclencheur et sur **Send a text message**. La réponse utilise l’identifiant du chat de la demande.
7. Alimenter les tables avec les collecteurs correspondants avant de demander des recommandations fondées sur votre collection.
8. Vérifier une demande de statistiques, une recherche précise et une recommandation, puis activer le workflow.

Ce workflow complet conserve son **Telegram Trigger**. Le début planifié et la restauration du tunnel appartiennent aux collecteurs : les ajouter ici ne fournirait pas le message utilisateur attendu par l’assistant.

## Collecte des données

Utiliser BiblioBot, Trakt-Stats, Loadia-Stats et MyLudo-Stats, ou le workflow complet Ultime. Ce dépôt contient l’assistant, pas les collecteurs. La table DVD n’est pas consultée par cette version fournie de Conseil Ultime.

Google Drive et Telegram sont des services externes. Ollama peut exécuter le modèle localement ; cela ne rend pas les échanges avec ces services locaux.

## Anonymisation et vérification

Les références aux comptes, credentials, tables, dossiers privés, données épinglées et métadonnées d’instance ont été retirées ou remplacées par `YOUR_...`. L’export est désactivé.

JSON, connexions, références entre nœuds, syntaxe JavaScript et expressions ont été vérifiés localement. Aucune conversation Telegram ni inférence sur votre serveur Ollama n’a été exécutée. Le comportement du modèle et les accès réels restent à vérifier sur votre instance.
