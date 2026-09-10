# Workflows n8n

Des automatisations n8n construites pour de vrais besoins marketing : visibilité dans les réponses des IA, reporting, qualification de leads, production de contenu.

Chaque workflow est livré prêt à importer, documenté, et testé en conditions réelles.

## Templates

| Workflow | Ce qu'il fait | Statut |
|---|---|---|
| Veille GEO | Suit les citations d'une marque dans ChatGPT, Perplexity et Gemini, et alerte quand elles changent | En préparation |

## Structure

Chaque workflow a son propre dossier :

```
nom-du-workflow/
├── README.md       le problème, le résultat, les nœuds utilisés, la configuration
├── workflow.json   le workflow exporté, sans aucune clé
└── apercu.png      une capture du canevas
```

## Importer un workflow

1. Télécharge le fichier `workflow.json` du dossier qui t'intéresse.
2. Dans n8n, ouvre un nouveau workflow, puis le menu **Import from File**.
3. Crée tes propres identifiants : aucun n'est inclus, par sécurité.

## Sécurité

Aucun fichier de ce dépôt ne contient de clé d'API, de jeton ou d'identifiant. Chaque workflow indique les identifiants à créer de ton côté.

## Auteur

**Élie Lissoda**, SEO & GEO et automatisation marketing, Lyon.
[LinkedIn](https://www.linkedin.com/in/elie-lissoda) · [koudujob.com](https://koudujob.com)
