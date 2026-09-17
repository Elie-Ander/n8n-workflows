# Veille GEO

Tu poses les questions de tes clients à ChatGPT, Claude, Perplexity et Gemini, recherche web activée. La veille mesure si ta marque et tes concurrents sont cités, dans quel ordre et avec quelles sources, puis compare chaque passage au précédent. Chaque réponse arrive dans Notion.

## Le problème

Quand un client demande conseil à une IA, elle ne lui donne pas une page de liens : elle nomme quelques marques. Une marque absente de ces réponses sort du choix du client, et les outils SEO classiques ne le mesurent pas. Les réponses changent aussi d'un jour à l'autre : un seul test ne suffit pas.

## Le résultat

- Les 4 IA interrogées avec recherche web, sur tes propres questions.
- Pour chaque réponse : les marques citées et leur ordre de mention, le rang de chaque site dans les sources, les concurrents présents et la réponse complète.
- Un statut par réponse : visible, absent, apparu ou disparu, comparé au passage précédent.
- Une ligne par réponse dans Notion, et l'historique complet dans une table n8n.
- Une IA indisponible passe en erreur sans bloquer les autres.

Testé en conditions réelles : n8n face à Make et Zapier, 3 questions posées aux 4 IA, 12 réponses analysées en 4 minutes.

## Les nœuds

| Nœud | Rôle |
|---|---|
| Chaque lundi à 8 h, Lancer maintenant | Passage automatique chaque semaine, ou lancement à la main |
| Configuration | Ta marque, ses variantes, son domaine, tes concurrents et tes questions |
| Préparer les requêtes | Une requête par question |
| Interroger Perplexity | Agent API, préréglage rapide, recherche web |
| Interroger ChatGPT | GPT-5 mini avec la recherche web |
| Interroger Gemini | Gemini 2.5 Flash avec la recherche Google, 5 tentatives si le service ne répond pas |
| Interroger Claude | Claude Sonnet 5, 5 recherches web au plus par question |
| Étiqueter, Rassembler les réponses | Rattache chaque réponse à son IA et à sa question, puis les réunit |
| Analyser les réponses | Repère les marques, leur ordre de mention et le rang de leur site dans les sources |
| Lire l'historique, Comparer au passage précédent | Calcule le statut de chaque réponse |
| Enregistrer les résultats | Garde l'historique dans une table n8n |
| Écrire dans Notion | Une ligne par réponse, la réponse complète dans la page |

## Configuration

1. **Configuration** : dans le nœud du même nom, renseigne :
   - `brand`, `aliases`, `domains` : ta marque, ses autres écritures séparées par des virgules, son domaine ;
   - `competitors` : un concurrent par ligne, au format `Nom | domaine | variantes` ;
   - `prompts` : une question par ligne, formulée comme tes clients la posent.

   Les noms de 4 caractères ou moins sont comparés en respectant les majuscules, pour que « Make » ne soit pas confondu avec le mot anglais « make ».

2. **Table n8n** : crée une table de données nommée `Veille GEO resultats` avec ces colonnes :

   | Colonne | Type |
   |---|---|
   | run_id, brand, engine, prompt, competitors_mentioned, status, answer_excerpt, sources, error | Texte |
   | run_at | Date |
   | mentioned, cited | Booléen |
   | citation_rank | Nombre |

3. **Base Notion** avec ces colonnes, noms et types exacts :

   | Colonne | Type |
   |---|---|
   | Titre | Titre |
   | Moteur | Sélection : ChatGPT, Claude, Perplexity, Gemini |
   | Statut | Sélection : visible, apparu, absent, disparu, erreur |
   | Marque citée | Case à cocher |
   | Position, Rang dans les sources | Nombre |
   | Question, Ordre de mention, Détail par marque, Concurrents cités, Sources, Erreur | Texte |
   | Date | Date |

4. **Connexion Notion** : crée une intégration interne dans Notion, ajoute-la à la page qui contient la base, puis colle son jeton dans un identifiant « Notion API » de n8n.
5. **Les 4 IA** : crée un identifiant pour chacune, avec ta propre clé :
   - « Anthropic », avec la recherche web autorisée dans la console Anthropic ;
   - « OpenAI » ;
   - « Perplexity API », clé créée sur console.perplexity.ai ;
   - « Google Gemini (PaLM) API », clé créée sur Google AI Studio.
6. **Import** : importe `workflow.json`, choisis ta table dans les nœuds « Lire l'historique » et « Enregistrer les résultats », ta base dans « Écrire dans Notion », puis rattache tes identifiants.
7. **Premier passage** : lance « Lancer maintenant ». Publie ensuite le workflow pour le passage du lundi.

Chaque passage consomme des tokens et des recherches web, facturés par chaque fournisseur d'IA. Les réponses des IA varient d'un passage à l'autre : la veille prend tout son sens quand on la suit dans la durée.
