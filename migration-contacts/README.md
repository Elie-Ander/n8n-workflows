# Migration de contacts entre deux outils

Reprend des contacts d'un outil pour les écrire dans un autre : correspondance des champs, nettoyage, contrôles, test à blanc puis import réel, avec un rapport d'écarts à chaque passage.

![Canevas du workflow](apercu.png)

## Le problème

Changer de CRM ou d'outil d'emailing, c'est des milliers de contacts à déplacer. Un export puis un import bruts recopient toutes les erreurs : e-mails invalides, téléphones dans tous les formats, doublons, consentements illisibles. Une fois importés, les contacts sales sont difficiles à retirer.

## Le résultat

- Correspondance des champs décrite en JSON, modifiable sans toucher au code.
- E-mails normalisés et validés, téléphones au format international selon le pays (France, Belgique, Suisse, Luxembourg, Espagne, Italie, Allemagne), dates au format ISO.
- Consentements e-mail et SMS relus (oui, non, 1, 0, true, false) : une valeur illisible vaut refus, jamais accord.
- Doublons repérés sur l'e-mail, champs obligatoires contrôlés, champs de la source non repris signalés.
- Mode test : tout est contrôlé et simulé, rien n'est écrit. Mode réel : écriture dans la cible, avec mise à jour quand l'e-mail existe déjà.
- Un rapport à chaque passage : total, valides, rejetés avec leur motif, doublons et champs non repris.

Testé sur 12 contacts d'essai volontairement sales : 8 migrés, 4 rejetés avec leur motif, 1 doublon repéré.

## Les nœuds

| Nœud | Rôle |
|---|---|
| Lancer la migration | Lancement à la main |
| Configuration | Mode test ou réel, correspondance des champs, champs obligatoires, pays par défaut |
| Lire la source | Les contacts à migrer, 500 au plus par passage |
| Preparer et controler | Correspondance, nettoyage et contrôles, un statut et un motif par contact |
| Contacts valides | Ne laisse passer que les contacts valides |
| Ecrire dans la cible | Création ou mise à jour sur l'e-mail, simulée en mode test |
| Construire le rapport, Ecrire le rapport | Bilan du passage dans une table |

## Configuration

1. **Trois tables n8n** :

   | Table | Colonnes |
   |---|---|
   | Migration contacts source | external_id, prenom, nom, email, telephone, pays, optin_email, optin_sms, langue, date_inscription, segment |
   | Migration contacts cible | external_id, first_name, last_name, email, phone, country, email_subscribed, sms_subscribed, language, created_at, segment, run_id |
   | Migration rapport | run_id, run_at, mode, total, valides, rejetes, doublons, champs_non_mappes, details |

2. **Configuration** : `mode` (test ou reel), `mapping` (colonne source vers colonne cible), `champs_obligatoires` et `pays_defaut`.
3. **Import** : importe `workflow.json` et choisis tes tables dans les 3 nœuds de table. Aucun identifiant externe n'est nécessaire.
4. **Avec de vrais outils** : remplace « Lire la source » par le nœud de l'outil d'origine (HubSpot, Mailchimp, Brevo, fichier CSV) et « Ecrire dans la cible » par celui de l'outil d'arrivée. Les contrôles restent les mêmes.
5. Lance d'abord en mode test, lis le rapport, puis passe en `reel`.
