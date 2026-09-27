# Reporting marketing hebdomadaire

Le lundi matin, le point marketing est déjà dans votre boîte : trafic, référencement et publicité comparés à la semaine d'avant, avec une synthèse claire.

![Le workflow dans n8n](apercu.png)

## Comment il fonctionne

1. **Chaque lundi à 8 h.** La semaine passée est comparée à celle d'avant.
2. **Collecter les chiffres.** GA4, Search Console, et Google Ads si vous l'utilisez. Une source en panne ne bloque pas le rapport : elle y est signalée.
3. **Analyser.** Les calculs sont faits en code. Claude ne reçoit que des chiffres vérifiés.
4. **Envoyer.** Le rapport part par e-mail, la semaine est gardée.
5. **Rien à analyser.** Aucune source ne répond : une alerte part à la place.

Testé sur des données simulées.

## Pour l'installer

1. Dans Google Cloud, activez Google Analytics Data API et Search Console API.
2. Créez un identifiant « Google OAuth2 API » avec les scopes `analytics.readonly` et `webmasters.readonly`, et un identifiant Google Ads si vous l'utilisez.
3. Créez la table n8n « Reporting marketing historique » :

   | Colonne | Type |
   |---|---|
   | run_id, top_queries, summary | Texte |
   | period_start, period_end | Date |
   | sessions, users, key_events, engagement_rate, sessions_change | Nombre |
   | gsc_clicks, gsc_impressions, gsc_ctr, gsc_position, gsc_clicks_change | Nombre |
   | ads_cost, ads_clicks | Nombre |

4. Dans Configuration, indiquez votre site, votre propriété GA4, votre propriété Search Console, `google_ads_active` et l'e-mail du destinataire.
5. Créez un identifiant Anthropic et un identifiant Gmail.
6. Importez `workflow.json`, choisissez votre table dans les deux nœuds de table et publiez.

---

Un souci pour l'installer, ou une question ? Je suis disponible sur [elie.koudujob.com](https://elie.koudujob.com) 😉

**Elie LISSODA**
