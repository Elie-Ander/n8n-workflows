# Recherche de prospects

Tu décris une cible dans un formulaire. Claude cherche sur le web de vraies entreprises qui y correspondent, chaque site est vérifié, et chaque prospect arrive dans Notion avec un signal vérifiable, sa source et une phrase d'approche.

## Le problème

Trouver des prospects qualifiés prend des heures : chercher, ouvrir chaque site, noter pourquoi l'entreprise vaut le coup, écrire une accroche. Les fichiers achetés vieillissent vite, et une IA sans recherche web invente parfois des entreprises.

## Le résultat

- Des entreprises trouvées dans de vrais résultats de recherche, chacune avec son site officiel.
- Pour chaque prospect : ville, secteur, signal avec l'URL qui le prouve, décideur quand il est publié, pertinence de 1 à 5, raison du choix et première phrase d'approche.
- Chaque site est appelé. S'il ne répond pas ou ne cite pas l'entreprise, la fiche arrive en « Site à vérifier ».
- Les domaines déjà dans Notion sont écartés : une nouvelle recherche n'ajoute que de nouveaux prospects.
- Aucun e-mail ni téléphone n'est collecté.

Testé en conditions réelles : 5 agences immobilières indépendantes de Lyon trouvées, vérifiées et rangées dans Notion en une minute.

## Les nœuds

| Nœud | Rôle |
|---|---|
| Décrire la cible | Formulaire réservé aux comptes de ton n8n : type d'entreprise, zone, taille, signal, offre, nombre de prospects |
| Lire les prospects déjà dans Notion | Récupère les domaines déjà en base pour éviter les doublons |
| Préparer la recherche | Nettoie les champs et construit la liste des domaines à exclure |
| Chercher avec Claude | Claude Sonnet 5 avec la recherche web (20 recherches au plus), réponse en JSON |
| Lister les prospects | Écarte annuaires, réseaux sociaux et doublons, ou crée une fiche « Erreur » qui explique pourquoi |
| Vérifier le site | Appelle le site officiel de chaque prospect |
| Noter la vérification | Donne le statut « À contacter » ou « Site à vérifier » |
| Créer la fiche dans Notion | Remplit les colonnes et ajoute le détail de la vérification dans la fiche |

## Configuration

1. **Base Notion** avec ces colonnes, noms et types exacts :

   | Colonne | Type |
   |---|---|
   | Nom | Titre |
   | Statut | Sélection : À contacter, Site à vérifier, Contacté, Erreur |
   | Pertinence | Nombre |
   | Site, Source | URL |
   | Ville, Secteur, Signal, Décideur, Pourquoi, Angle, Recherche | Texte |
   | Date de recherche | Date |

2. **Connexion Notion** : crée une intégration interne dans Notion, ajoute-la à la page qui contient la base, puis colle son jeton dans un identifiant « Notion API » de n8n.
3. **Claude** : crée un identifiant « Anthropic » avec ta clé API. La recherche web doit être autorisée dans la console Anthropic.
4. **Import** : importe `workflow.json`, choisis ta base dans les 2 nœuds Notion et rattache tes identifiants.
5. **Publication** : publie le workflow. Le formulaire a alors son adresse, accessible aux seuls comptes de ton n8n.

Chaque recherche consomme des tokens Claude et des recherches web, facturés sur ton compte Anthropic.
