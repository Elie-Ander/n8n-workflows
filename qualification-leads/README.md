# Qualification de leads entrants

Chaque demande reçue par ton formulaire de contact est gardée, enrichie par le site du prospect, notée sur 100 et poussée dans HubSpot. Quand le lead est chaud, une tâche de rappel est créée et le commercial reçoit un e-mail avec la première phrase à dire.

![Canevas du workflow](apercu.png)

## Le problème

Les demandes entrantes arrivent toutes au même endroit, sans tri. Le commercial rappelle dans l'ordre d'arrivée plutôt que dans l'ordre de valeur, saisit chaque contact à la main dans le CRM, et les meilleures demandes attendent parfois plusieurs jours.

## Le résultat

- Chaque demande est enregistrée dans une table n8n avant tout traitement : rien ne se perd, même si une étape échoue ensuite.
- Le site du prospect est lu : titre, description, titre principal et un extrait du texte. Sans site renseigné, le domaine de l'e-mail professionnel sert de piste.
- Score sur 100 : la moitié vient de Claude, qui juge l'adéquation entre la demande et ton offre, l'autre de règles fixes (budget 25 points, délai 15, e-mail professionnel 10).
- Chaque lead est rangé en chaud, tiède ou froid. Le seuil du lead chaud se règle, 70 par défaut.
- Le contact est créé ou mis à jour dans HubSpot avec son entreprise, son poste, son site et son message.
- Lead chaud : tâche de rappel dans HubSpot et e-mail au commercial avec le résumé, les raisons du score, les points à vérifier et la première phrase à dire.
- Claude ou HubSpot en panne : le lead reste dans la table, le score repasse sur les règles seules et une alerte d'anomalie part.
- Les champs du formulaire sont traités comme des données, jamais comme des consignes : un prospect ne peut pas gonfler son score en écrivant des instructions.
- Le site n'est lu que s'il s'agit d'un domaine public : adresses IP et réseaux locaux sont refusés.

Testé sur des données simulées.

## Les nœuds

| Nœud | Rôle |
|---|---|
| Formulaire de contact | Nom, e-mail professionnel, entreprise, site, poste, taille, besoin, budget, délai et accord de recontact |
| Configuration | Ton offre, ton client idéal, le seuil du lead chaud, les e-mails du commercial et de l'administrateur |
| Normaliser la demande | Nettoie les champs, repère les e-mails personnels et le site à lire |
| Enregistrer la demande | Garde la demande brute dans la table Leads qualifies |
| Site à lire ?, Lire le site du prospect | Appelle le site seulement si c'est un domaine public |
| Extraire le contenu du site | Titre, description, titre principal et 2 500 caractères de texte |
| Qualifier avec Claude | Claude Opus 5 : note d'adéquation, résumé, raisons, risques, prochaine action et première phrase |
| Calculer le score | Ajoute les règles et range le lead en chaud, tiède ou froid |
| HubSpot : créer ou mettre à jour le contact | Fiche contact à jour |
| Préparer le suivi | Rédige la tâche, l'e-mail au commercial et l'alerte d'anomalie |
| Compléter la fiche du lead | Écrit le score, le segment, les raisons et l'identifiant HubSpot dans la table |
| Lead chaud ?, HubSpot : tâche de rappel, Alerter le commercial | Tâche et e-mail quand le score atteint le seuil |
| Anomalie ?, Signaler l'anomalie | E-mail à l'administrateur si Claude ou HubSpot a échoué |

## Configuration

1. **Table n8n** « Leads qualifies » avec ces colonnes :

   | Colonne | Type |
   |---|---|
   | submitted_at | Date |
   | full_name, email, company, website, job_title, company_size, need, budget, timeline | Texte |
   | score | Nombre |
   | segment, reasons, next_action, hubspot_id, error | Texte |
   | alert_sent | Booléen |

2. **Claude** : crée un identifiant « Anthropic » avec ta clé API.
3. **HubSpot** : crée une application privée avec les droits de lecture et d'écriture sur les contacts et les tâches, puis colle son jeton dans un identifiant « HubSpot App Token ».
4. **Gmail** : crée un identifiant Gmail OAuth2.
5. **Configuration** : remplis ton offre, ton client idéal, le seuil, les deux e-mails et, si tu veux un lien direct vers la fiche, l'identifiant de ton portail HubSpot.
6. **Import** : importe `workflow.json`, choisis ta table dans les 2 nœuds de table, rattache tes identifiants et publie. Partage ensuite l'adresse de production du formulaire, ou remplace-le par un Webhook relié au formulaire de ton site.

Chaque demande consomme un appel à Claude, facturé sur ton compte Anthropic.
