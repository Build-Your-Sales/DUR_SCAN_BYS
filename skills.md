---
name: analyse-dur
description: Analyse une entreprise à partir de son site web et de ses offres, puis produit un scoring DUR (Douloureux, Urgent, Reconnu) du problème que résout son offre, au format JSON strict. Utilise ce skill dès que l'utilisateur veut qualifier, analyser, scorer ou "lire" une entreprise, un prospect ou un site web ; évaluer si un problème/une offre est "DUR" ou vendable ; reconstituer l'ICP, le positionnement ou la motion GTM d'une boîte ; prioriser ou trier une liste de prospection B2B ; ou décider si une cible est chaude pour une offre donnée (mode "fit prospect") — même si l'utilisateur ne dit pas explicitement "DUR". Déclenche-le aussi sur des formulations comme "analyse cette boîte", "qualifie ce prospect", "que vaut ce marché", "est-ce une bonne cible", "score ce site".
---

# Analyse d'entreprise & Scoring DUR

Analyse n'importe quelle entreprise à partir de son site web et de ses offres, et produis une **analyse DUR** (Douloureux · Urgent · Reconnu) du problème que résout son offre. Lis le site **comme un dossier, pas comme une brochure** : reste factuel, critique, et ne te laisse jamais berner par le marketing de la page d'accueil.

## Entrées attendues

Récupère (ou demande) les éléments suivants. **Privilégie le texte scrapé du site** à la simple URL : plus il y a de matière brute, meilleure est l'analyse.

```
NOM_ENTREPRISE       # nom de la boîte
URL                  # site web
CONTENU_SITE         # texte scrapé : hero, pricing, features, cas clients, à propos, careers, doc…
OFFRES               # descriptif des offres si connu (sinon : à déduire du site)
SIGNAUX_ADDITIONNELS # optionnel : LinkedIn, actus, levées, recrutements, avis…
MON_OFFRE            # optionnel : n'active l'extension "fit prospect" (§Extension) que si renseigné
```

Si une information manque, ne l'invente pas : marque-la `"non déterminable depuis les sources"`.

## Le cadre DUR

Le DUR mesure si un problème vaut la peine qu'on construise une offre (ou un message de prospection) autour. Un problème n'est **vendable** que s'il est :

- **Douloureux (D)** — il crée une douleur *réelle* : financière, opérationnelle, de process, humaine ou émotionnelle. Plus l'impact business est **chiffrable et ressenti**, plus D est fort. Un simple *nice-to-have* → D faible.
- **Urgent (U)** — il appelle une résolution *immédiate*. Un **déclencheur** (échéance, contrainte réglementaire, perte active, pression du board, renouvellement de contrat, incident) crée l'urgence. Sans déclencheur, la cible procrastine → U faible.
- **Reconnu (R)** — la cible a **déjà conscience** du problème et le formule. S'il faut d'abord la convaincre que le problème existe, R est faible (et le cycle de vente s'allonge). ⚠️ Piège fréquent : le **« reconnu mais mal attribué »** — la cible sent le symptôme mais se trompe sur la cause.

**Règle d'or** : plus D, U et R sont élevés *simultanément*, plus le marché est mûr et le cycle court.

## Méthode (raisonne étape par étape, en interne, AVANT de produire le JSON)

### Étape 1 — Reconstituer l'entreprise depuis le site
Lis le site comme un dossier. Points de lecture → ce qu'ils révèlent :

| Élément du site | Ce que ça trahit |
|---|---|
| **Hero (H1 + sous-titre)** | La catégorie revendiquée, le problème mis « au-dessus de la ligne de flottaison », l'audience nommée |
| **Page pricing** (public / partiel / caché) | La motion : *self-serve* (volume), *sales-led* (qualification), *enterprise* (deals custom) |
| **Hiérarchie des CTA** (« Essai gratuit » vs « Demander une démo » vs « Contacter ») | Product-led, sales-led ou hybride |
| **Pages produit / features** | Ce qu'ils **shippent** réellement vs ce qu'ils *claiment* |
| **Intégrations** | L'écosystème sur lequel ils parient (et les absences révélatrices) |
| **Cas clients / témoignages / logos** | Traction réelle, secteurs et tailles servis, **langage de douleur** utilisé par les clients |
| **Page careers / recrutements** | Croissance et priorités : qui ils recrutent = où ils investissent |
| **Profondeur doc / changelog** | Maturité produit et cadence de livraison |
| **Pages comparatives (« Nous vs X »)** | Concurrents qu'ils affrontent et sur quels arguments |

→ Déduis : **que** vend l'entreprise, **à qui** (ICP : secteur, taille, rôle), **comment** (motion), et son **stade** de maturité.

### Étape 2 — Identifier le problème central
Formule le(s) problème(s) que l'offre résout **pour le client** (pas les features). Un pain point n'est pas « il manque telle feature » mais la **raison sous-jacente**. Classe chaque problème par catégorie : `financier` · `productivité/opérationnel` · `process` · `humain/people` · `support/risque`.

### Étape 3 — Noter le DUR
Pour chaque dimension, note de **0 à 5** selon la rubrique ci-dessous, en **citant l'indice** qui justifie la note. Distingue toujours ce qui est **prouvé** (présent dans les sources) de ce qui est **inféré** (hypothèse + niveau de confiance).

### Étape 4 — Synthèse
Score composite, verdict, **maillon faible** (D, U ou R), et un **angle d'accroche** : comment reformuler le problème à cette cible pour **maximiser le Reconnu** et remonter l'Urgent.

## Rubrique de scoring (0–5 par dimension)

**Douloureux** — `0–1` nice-to-have, aucune douleur claire · `2–3` gêne réelle mais non critique / impact peu chiffrable · `4–5` douleur forte, impact business chiffrable ou existentiel.

**Urgent** — `0–1` aucune urgence, « un jour » · `2–3` souhaitable à moyen terme, pas de déclencheur · `4–5` déclencheur actif (perte, échéance, réglementation, pression) → résolution immédiate.

**Reconnu** — `0–1` la cible ne sait pas qu'elle a le problème · `2–3` conscience partielle ou cause mal attribuée · `4–5` problème clairement identifié et formulé par la cible.

**Score composite** = D + U + R (sur 15). **Verdict** : `≥ 12` → fort · `7–11` → moyen · `≤ 6` → faible.

## Règles (garde-fous)

- Base **chaque affirmation** sur un élément fourni. Ce qui n'est pas prouvé est marqué `hypothèse` avec une confiance (`élevée` / `moyenne` / `faible`).
- **N'invente jamais** de chiffres, de clients, de faits. Info manquante → `"non déterminable depuis les sources"`.
- Ne confonds pas ce que l'entreprise **dit** résoudre avec la **douleur réelle** du client. Reste critique.
- Reste factuel et neutre : **pas de flatterie**, pas de superlatifs gratuits.
- Langue de sortie : **français**. Sortie = **JSON strict, aucun texte hors JSON**.

## Sortie — JSON strict

```json
{
  "entreprise": {
    "nom": "string",
    "url": "string",
    "categorie_revendiquee": "string",
    "resume_1_ligne": "vend [quoi] à [qui] pour [résultat]"
  },
  "profil": {
    "offres": ["string"],
    "icp": {
      "secteurs": ["string"],
      "taille_entreprise": "string",
      "roles_cibles": ["string"]
    },
    "motion_gtm": "self-serve | sales-led | hybride | enterprise | indéterminé",
    "maturite": "early | croissance | établie | indéterminé",
    "signaux_lus": ["indice concret relevé sur le site"]
  },
  "problemes": [
    {
      "probleme": "formulé côté client, pas feature",
      "categorie": "financier | productivité | process | humain | support/risque",
      "statut": "preuve | hypothèse",
      "confiance": "élevée | moyenne | faible"
    }
  ],
  "analyse_dur": {
    "probleme_central": "string",
    "douloureux": { "score": 0, "justification": "string (avec indice)" },
    "urgent":     { "score": 0, "justification": "string (avec indice)" },
    "reconnu":    { "score": 0, "justification": "string (avec indice)" },
    "score_composite": 0,
    "verdict": "fort | moyen | faible",
    "maillon_faible": "D | U | R | aucun"
  },
  "synthese": {
    "resume": "string",
    "angle_accroche": "reformulation du problème pour maximiser le Reconnu",
    "risques_analyse": ["ce qui manque ou reste à vérifier"],
    "confiance_globale": "élevée | moyenne | faible"
  }
}
```

## Extension optionnelle — Fit prospect (n'exécuter que si `MON_OFFRE` est renseigné)

Applique une **seconde analyse DUR**, cette fois sur **l'entreprise en tant qu'acheteur** : a-t-elle *elle-même* un problème D/U/R que **`MON_OFFRE`** résout ? Ajoute alors ce bloc au JSON :

```json
{
  "fit_prospect": {
    "offre_evaluee": "string",
    "probleme_du_prospect": "string",
    "douloureux": { "score": 0, "justification": "string" },
    "urgent":     { "score": 0, "justification": "string" },
    "reconnu":    { "score": 0, "justification": "string" },
    "score_composite": 0,
    "recommandation": "cible chaude | tiède | à écarter",
    "angle_outbound": "1re ligne d'accroche possible, ancrée sur un signal concret"
  }
}
```

## Exemples (few-shot)

### Exemple A — DUR **fort**
*Entreprise fictive : « Inbox Rescue » — SaaS de délivrabilité & warm-up d'emails, pricing public, CTA « Start free », cas clients d'équipes outbound.*

```json
{
  "entreprise": {
    "nom": "Inbox Rescue",
    "url": "https://inboxrescue.example",
    "categorie_revendiquee": "Plateforme de délivrabilité email pour équipes outbound",
    "resume_1_ligne": "vend un outil de warm-up et de monitoring de délivrabilité aux équipes sales/growth pour que leurs emails atterrissent en boîte de réception"
  },
  "profil": {
    "offres": ["Warm-up automatique de boîtes mail", "Monitoring de réputation et de placement (inbox vs spam)", "Rotation de domaines"],
    "icp": { "secteurs": ["SaaS B2B", "agences outbound", "services B2B"], "taille_entreprise": "PME à scale-up (10–200)", "roles_cibles": ["Head of Sales", "SDR Lead", "Growth"] },
    "motion_gtm": "hybride",
    "maturite": "croissance",
    "signaux_lus": ["Pricing public à 3 tiers → volume", "CTA principal 'Start free' → product-led", "Cas clients chiffrés sur le taux de placement", "Comparatif 'vs [concurrent]' en ligne"]
  },
  "problemes": [
    { "probleme": "Les emails de prospection finissent en spam et les domaines se crament", "categorie": "financier", "statut": "preuve", "confiance": "élevée" },
    { "probleme": "Aucune visibilité sur le placement réel des emails (inbox vs spam)", "categorie": "productivité", "statut": "preuve", "confiance": "élevée" }
  ],
  "analyse_dur": {
    "probleme_central": "Les campagnes outbound perdent en efficacité parce que les emails n'arrivent pas en boîte de réception",
    "douloureux": { "score": 5, "justification": "Impact direct sur le CA : un email en spam = 0 réponse ; réputation d'expéditeur difficile à réparer une fois cramée (cas clients qui chiffrent la chute de placement)" },
    "urgent":     { "score": 5, "justification": "Perte active et continue : chaque jour en spam = pipeline manqué ; déclencheur évident quand les taux d'ouverture s'effondrent" },
    "reconnu":    { "score": 4, "justification": "Les équipes voient leurs taux d'ouverture chuter (reconnu), mais l'attribuent parfois à leur copy plutôt qu'à la délivrabilité (mal attribué)" },
    "score_composite": 14,
    "verdict": "fort",
    "maillon_faible": "R"
  },
  "synthese": {
    "resume": "Problème DUR fort : douleur financière chiffrable, urgence mécanique, et large reconnaissance — le seul angle mort étant l'attribution (copy vs délivrabilité).",
    "angle_accroche": "Vos taux d'ouverture ont chuté et vous pensez que c'est votre copy ? 9 fois sur 10, c'est votre délivrabilité — et ça se mesure en 2 minutes.",
    "risques_analyse": ["Taille réelle de la base clients non déterminable depuis les sources"],
    "confiance_globale": "élevée"
  }
}
```

### Exemple B — DUR **faible**
*Entreprise fictive : « TeamVibe » — plateforme de sondages d'engagement / bien-être RH, pricing caché, CTA « Book a demo ».*

```json
{
  "entreprise": {
    "nom": "TeamVibe",
    "url": "https://teamvibe.example",
    "categorie_revendiquee": "Plateforme d'engagement et de bien-être des salariés",
    "resume_1_ligne": "vend une plateforme de sondages d'engagement aux équipes RH/People pour mesurer et améliorer le moral des salariés"
  },
  "profil": {
    "offres": ["Sondages d'engagement récurrents", "Dashboards eNPS", "Recommandations d'actions RH"],
    "icp": { "secteurs": ["tous secteurs"], "taille_entreprise": "Mid-market (100–1000)", "roles_cibles": ["DRH", "People Ops", "CHRO"] },
    "motion_gtm": "sales-led",
    "maturite": "croissance",
    "signaux_lus": ["Pricing caché derrière 'Contact sales' → qualification/enterprise", "CTA principal 'Book a demo'", "Témoignages centrés sur le 'feel-good', peu de chiffres business"]
  },
  "problemes": [
    { "probleme": "L'engagement des salariés est difficile à mesurer et à améliorer", "categorie": "humain", "statut": "preuve", "confiance": "moyenne" },
    { "probleme": "Manque de visibilité RH sur le moral des équipes", "categorie": "process", "statut": "hypothèse", "confiance": "moyenne" }
  ],
  "analyse_dur": {
    "probleme_central": "Améliorer l'engagement des salariés",
    "douloureux": { "score": 2, "justification": "Douleur réelle mais rarement chiffrable et rarement existentielle ; l'impact business (turnover, productivité) reste indirect et diffus" },
    "urgent":     { "score": 1, "justification": "Aucun déclencheur clair sur le site ; sujet 'important mais pas urgent', facilement repoussé quand les budgets se resserrent" },
    "reconnu":    { "score": 2, "justification": "Conscience partielle : les RH savent que l'engagement compte, mais ne le formulent pas comme un problème prioritaire à résoudre maintenant" },
    "score_composite": 5,
    "verdict": "faible",
    "maillon_faible": "U"
  },
  "synthese": {
    "resume": "Problème réel mais peu DUR en l'état : nice-to-have sans urgence ni impact chiffrable évident. Vendable seulement si on le relie à une douleur chiffrable et à un déclencheur.",
    "angle_accroche": "Reformuler vers un pain chiffrable + déclencheur : ex. 'Après un plan social / un eNPS en chute, vos meilleurs éléments partent — voici comment le voir venir 3 mois avant.' (remonte D et U)",
    "risques_analyse": ["Absence de pricing et de cas clients chiffrés limite l'évaluation de la douleur réelle"],
    "confiance_globale": "moyenne"
  }
}
```
