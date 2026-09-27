# Workflows n8n

Je m'appelle Elie LISSODA et je construis des automatisations marketing et commerciales avec n8n et l'IA. Voici quinze workflows que j'ai conçus pour de vrais besoins : être cité par les IA, suivre ses chiffres sans y passer la matinée, trouver et relancer des prospects, garder un CRM propre, lire des factures, surveiller ses automatisations.

Chacun est prêt à importer. Dans n8n, des notes de couleur expliquent chaque étape. Sur GitHub, le README du dossier dit ce qu'il fait, comment l'installer, et ce qui a été testé.

## Les workflows

### Visibilité SEO et GEO

| Workflow | Ce qu'il fait | Outils |
|---|---|---|
| [Veille GEO](veille-geo/) | Mesure comment ChatGPT, Claude, Perplexity et Gemini citent une marque et ses concurrents, compare chaque passage au précédent et range les réponses dans Notion | ChatGPT, Claude, Perplexity, Gemini, Notion |
| [Audit SEO et GEO d'une page](audit-seo-geo/) | Note une page sur 100 (SEO, lisibilité par les IA, signaux GEO) et fait rédiger les actions prioritaires | Claude |
| [Usine de contenu GEO](usine-contenu-geo/) | Transforme une question en article sourcé, noté, corrigé et vérifié, puis le dépose en brouillon | Perplexity, ChatGPT, Claude, Gemini, WordPress, Notion |

### Marketing et pilotage

| Workflow | Ce qu'il fait | Outils |
|---|---|---|
| [Reporting marketing hebdomadaire](reporting-marketing-hebdo/) | Compare chaque lundi GA4, Search Console et Google Ads à la semaine précédente, fait rédiger la synthèse et l'envoie par e-mail | GA4, Search Console, Google Ads, Claude, Gmail |
| [Assistant marketing](assistant-marketing/) | Un chat où Claude interroge lui-même GA4 et Search Console, puis répond avec la période et la source de chaque chiffre | Agent Claude, GA4, Search Console |
| [Mesure du temps gagné](temps-gagne/) | Chiffre chaque mois les heures et les euros économisés par les automatisations, workflow par workflow | API n8n, Gmail |

### Ventes et CRM

| Workflow | Ce qu'il fait | Outils |
|---|---|---|
| [Qualification de leads](qualification-leads/) | Lit le site du prospect, note chaque demande sur 100, crée la fiche HubSpot et alerte le commercial quand le lead est chaud | Claude, HubSpot, Gmail |
| [Recherche de prospects](recherche-prospects/) | Trouve de vraies entreprises qui correspondent à une cible, vérifie leur site et range chaque prospect dans Notion avec une phrase d'approche | Claude, Notion |
| [Signaux d'achat](signaux-achat/) | Repère chaque semaine les comptes qui lèvent des fonds, recrutent ou changent de dirigeant, les note et crée la tâche dans HubSpot | Perplexity, Claude, HubSpot, Telegram |
| [Relances personnalisées par IA](relances-personnalisees/) | Écrit une séquence de trois messages pour chaque prospect et l'arrête dès qu'il répond | Claude, Gmail, Telegram |
| [Qualité des données CRM](qualite-donnees-crm/) | Remet en forme e-mails et téléphones, regroupe les doublons, note la base sur 100 et corrige HubSpot par lots | HubSpot, Gmail |
| [Migration de contacts](migration-contacts/) | Déplace des contacts d'un outil à l'autre : champs mis en correspondance, données nettoyées, consentements relus, test à blanc et rapport d'écarts | Tables n8n |

### Documents, IA et fiabilité

| Workflow | Ce qu'il fait | Outils |
|---|---|---|
| [Extraction de factures et de devis](extraction-documents/) | Extrait les données d'un PDF, recontrôle montants, SIRET et IBAN, repère les doublons et n'alerte que si un regard humain est nécessaire | Claude, Telegram |
| [Assistant RAG sur documents internes](assistant-rag/) | Répond aux questions des équipes à partir des documents de l'entreprise et cite chaque source | Agent Claude, OpenAI (vecteurs) |
| [Surveillance des workflows](surveillance-workflows/) | Classe chaque erreur, relance les pannes passagères, évite les alertes en double et envoie un bilan chaque matin | API n8n, Telegram |

## Importer un workflow

1. Téléchargez le fichier `workflow.json` du dossier qui vous intéresse.
2. Dans n8n, ouvrez un nouveau workflow, puis le menu **Import from File**.
3. Créez vos identifiants et vos tables : aucun n'est inclus. Le README du dossier donne la liste.

Les workflows sont construits sur une version récente de n8n. Si un nœud s'affiche avec un point d'interrogation, mettez votre n8n à jour.

## Sécurité

Aucun fichier de ce dépôt ne contient de clé, de jeton, d'identifiant de connexion ni d'adresse d'instance. Chaque export est nettoyé, puis contrôlé automatiquement avant d'être publié.

---

Un souci pour installer un workflow, ou une idée d'automatisation pour votre équipe ? Je suis disponible sur [elie.koudujob.com](https://elie.koudujob.com) 😉

**Elie LISSODA**  
SEO & GEO et automatisation marketing, Lyon  
Certifié n8n Foundations & Workflow Automation et HubSpot Revenue Operations (2026)
