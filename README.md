# Agent Minier

Agent de veille du secteur minier ivoirien : rechercher → vérifier → analyser →
synthétiser → citer les publications des compagnies qui exploitent en Côte
d'Ivoire, et produire un bulletin des résultats de leurs travaux.

## Contenu

| Fichier | Rôle |
|---|---|
| `compagnies.json` | Registre des opérateurs, actifs ivoiriens, URLs IR/newsroom, réseau(x) social(aux), notes de fiabilité. **Source de vérité** — à mettre à jour à chaque changement d'opérateur. |
| `etat.json` | État de veille : cutoff, historique des exécutions, sources couvertes, sources en échec, compagnies muettes. |
| `rapports/` | Bulletins produits (`AAAA-MM-JJ_bulletin-NN.md`). |
| `_work/` | Baux de travail : pages brutes récupérées, ledgers de citations. Jetable. |

## Lancer une veille à la main

> « Lance Agent Minier » / « Fais le bulletin minier de la semaine »

L'agent charge la skill `agent-minier`, lit le cutoff dans `etat.json`, collecte
les publications de la fenêtre, écrit le bulletin dans `rapports/`, vérifie les
citations, puis met l'état à jour.

## Mise à jour du registre

- Nouvelle mine ou changement d'opérateur → éditer `compagnies.json` (champ
  `actifs_ci`, `sites`, `note`), puis le signaler dans le bulletin suivant.
- Vérifier au moins une fois par trimestre qui exploite quoi : les cessions sont
  fréquentes (Tongon est passé de Barrick à Atlantic Group en décembre 2025).
- Ne pas ajouter une société sans au moins une source publique de ses résultats
  (newsroom, fil réglementaire ou presse spécialisée fiable).

## Automatisation

Un job cron « Agent Minier — bulletin hebdo » tourne le lundi à 8h00 (heure
locale de la machine) et livre le résumé dans la conversation d'origine. Pour le
modifier : demander la liste des jobs, puis mettre à jour la fréquence ou la
livraison.

## Limites connues

- LinkedIn et Facebook ne sont pas collectables de façon authentifiée : seuls les
  posts indexés sont visibles, et aucun chiffre n'en est tiré.
- Plusieurs sites de sociétés bloquent l'extraction directe (Endeavour, Tietto,
  Resolute, Perseus rapports, Barrick) : passer par GlobeNewswire, les annonces
  ASX/SEDAR+ ou la presse spécialisée, et déclarer le trou de couverture.
- Atlantic Group (Tongon), Tietto/Zhaojin (Abujar), SiNiCo, LEB, CML ne publient
  pas de comptes rendus trimestriels publics : leur suivi repose sur la presse
  locale et les rapports DGPE.

## Ce que l'agent ne fait pas

Pas de conseil en investissement, pas d'estimation de production non publiée,
pas d'attribution d'un chiffre groupe à un actif ivoirien.
