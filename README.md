# Workflows n8n

Des automatisations n8n construites pour de vrais besoins marketing : visibilité dans les réponses des IA, reporting, analyse de données, qualification de leads et prospection.

Chaque workflow est livré prêt à importer, documenté, et testé en conditions réelles.

## Templates

| Workflow | Ce qu'il fait | Statut |
|---|---|---|
| Veille GEO | Suit les citations d'une marque dans ChatGPT, Claude, Perplexity et Gemini, et alerte quand elles changent | À venir |
| Reporting marketing hebdomadaire | Compare chaque lundi GA4, Search Console et Google Ads à la semaine précédente, fait rédiger la synthèse par Claude et l'envoie par e-mail | À venir |
| Assistant marketing | Un chat où Claude interroge lui-même GA4 et Search Console, puis répond avec la période et la source de chaque chiffre | À venir |
| Qualification de leads | Lit le site du prospect, note chaque demande sur 100, crée la fiche HubSpot et alerte le commercial quand le lead est chaud | À venir |
| Recherche de prospects | Trouve de vraies entreprises qui correspondent à une cible, vérifie leur site et range chaque prospect dans Notion avec une phrase d'approche | À venir |

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
