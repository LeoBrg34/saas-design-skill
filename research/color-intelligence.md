---
title: "Color Intelligence for Modern SaaS UI"
version: "1.0"
research_date: "2026-10-06"
intended_use: "Source de skill pour agent IA de design/coding UI"
scope: "Web SaaS, applications produit, dashboards, landing pages, light/dark mode, accessibilité"
normative_accessibility_baseline: "WCAG 2.2"
---

# Color Intelligence for Modern SaaS UI

> **But du document** — fournir à un agent IA des règles de décision exécutables sur la couleur dans une interface SaaS. Ce document n'est pas un guide général de « psychologie des couleurs ». Il distingue explicitement les exigences normatives, les conventions industrielles fortes, les recommandations contextuelles et les tendances faiblement étayées.

## 0. Résumé exécutable

Si un agent IA ne retient que dix principes, utiliser ceux-ci :

1. **Choisir des rôles sémantiques avant de choisir des hex codes.** Le rôle (`text-primary`, `surface`, `danger`, `focus`, etc.) reste stable ; la valeur change selon le thème.
2. **Construire l'interface produit principalement avec des neutres.** Réserver les couleurs chromatiques à l'action, aux états, à la catégorisation et à la marque.
3. **Ne jamais faire porter une information essentielle à la couleur seule.** Ajouter texte, icône, forme, motif, position ou libellé.
4. **Respecter au minimum WCAG 2.2 AA :** texte normal 4.5:1 ; grand texte 3:1 ; information graphique et indicateurs UI requis 3:1 ; focus clavier visible.
5. **Ne pas inverser mécaniquement une palette light pour créer le dark mode.** Mapper les mêmes rôles vers des valeurs adaptées, avec des surfaces et des niveaux d'élévation propres au thème.
6. **Limiter la compétition chromatique.** Une zone fonctionnelle ne devrait normalement avoir qu'une action primaire visuellement dominante.
7. **Réserver success / warning / error / information à leur signification.** Ne pas les détourner pour de la décoration ou du branding si cela peut créer une ambiguïté.
8. **Traiter l'accent comme une couleur remplaçable.** Si remplacer un accent par une autre teinte change le sens, ce n'est probablement pas un accent mais une couleur sémantique.
9. **Pour les graphiques, utiliser une palette data-viz distincte et plusieurs canaux visuels.** Couleur + forme / style de ligne / label / séparation.
10. **Les associations de marque comme “bleu = confiance” ne sont que des priorités contextuelles.** Elles ne doivent jamais supplanter l'accessibilité, le contexte produit, la culture ou l'identité existante.

---

# 1. Méthode, niveaux de preuve et limites

## 1.1 Hiérarchie des preuves utilisée

**Evidence-backed rules**

- normes WCAG/W3C ;
- résultats expérimentaux ou revues académiques pertinents ;
- exigences mesurables de contraste et de perception.

**Strong industry conventions**

- convergence observée entre plusieurs design systems de production : Adobe Spectrum, IBM Carbon, Atlassian, GitHub Primer, Microsoft Fluent 2, GitLab Pajamas, Vercel Geist, Stripe ;
- règles de tokens, séparation des rôles, hiérarchie CTA et gestion light/dark.

**Context-dependent recommendations**

- budgets de couleur ;
- choix de saturation ;
- densité chromatique ;
- personnalité de marque ;
- adaptations par secteur.

**Trends / weak evidence**

- gradients “aurora” ;
- palettes néon / cyber ;
- “AI purple” ;
- noir comme raccourci de “luxe” ;
- règles de proportion de type 60/30/10.

## 1.2 État des standards d'accessibilité au 2026-10-06

WCAG 2.2 est le standard W3C actuel. Il a été publié comme W3C Recommendation le 5 octobre 2023 et a été approuvé comme ISO/IEC 40500:2025 en octobre 2025. WCAG 3 est toujours un **Working Draft incomplet** ; le W3C indique explicitement qu'il changera substantiellement et recommande de viser WCAG 2.2 aujourd'hui. [S01][S02][S08][S09]

**Conséquence pour un skill IA :** ne pas coder des seuils de conformité à partir de WCAG 3 tant qu'ils ne sont pas normatifs. Utiliser WCAG 2.2 comme baseline, et traiter WCAG 3 comme signal prospectif seulement.

## 1.3 Limite importante : “60/30/10”

Aucune base académique ou normative convaincante n'a été trouvée établissant 60/30/10 comme ratio optimal pour une interface SaaS. Les design systems matures étudiés structurent la couleur par rôles, niveaux de contraste, tokens et hiérarchie, pas par un partage fixe de surface. Les proportions proposées plus loin sont donc des **heuristiques opérationnelles**, pas des lois perceptives.

---

# 2. Evidence-backed rules

## EB-01 — Ne jamais encoder une information essentielle uniquement par la couleur

**RULE**  
Toute information qui déclenche une décision, indique un état, une erreur, une sélection, une variation ou une catégorie importante doit disposer d'au moins un second canal perceptible : texte, icône, forme, motif, soulignement, position, style de ligne ou libellé explicite.

**WHY**  
WCAG 2.2 SC 1.4.1 interdit l'utilisation de la couleur comme seul moyen visuel de transmettre une information, une action ou une réponse. Les déficiences de vision des couleurs et les contextes de mauvaise visibilité rendent les distinctions de teinte non fiables. [S05]

**WHEN TO USE**  
Toujours pour erreurs, succès, warnings, états sélectionnés, statuts de workflow, profit/perte, sévérité, disponibilité, séries de graphiques.

**WHEN NOT TO USE**  
La couleur seule peut rester décorative lorsqu'aucune information n'est perdue si elle disparaît.

**EXCEPTIONS**  
Aucune pour l'information essentielle ; un logo ou une illustration décorative n'est pas un canal informationnel.

**CONFIDENCE: High**

**SOURCES:** [S05], [S16], [S18], [S25]

---

## EB-02 — Contraste textuel : viser au minimum WCAG 2.2 AA

**RULE**  
- Texte normal : **>= 4.5:1** par rapport au fond.
- Grand texte : **>= 3:1**.
- Pour les petites tailles, les interfaces denses ou les contextes à risque, préférer une marge au-dessus du minimum plutôt que viser exactement le seuil.

**WHY**  
WCAG 2.2 SC 1.4.3 définit ces seuils. Le W3C rappelle que le contraste de luminance, plus que la teinte, est déterminant pour la lisibilité. [S03]

**WHEN TO USE**  
Tout texte fonctionnel, placeholder affiché, labels de formulaires, aides, légendes, texte coloré, texte sur CTA.

**WHEN NOT TO USE**  
Les logotypes et le texte purement décoratif sont exemptés par le critère, mais cela ne signifie pas qu'un contraste faible soit souhaitable.

**EXCEPTIONS**  
Les composants inactifs sont exemptés du critère ; ne pas interpréter cette exemption comme une invitation à rendre un état désactivé illisible.

**CONFIDENCE: High**

**SOURCES:** [S03], [S27]

---

## EB-03 — Contraste non textuel : les informations visuelles nécessaires doivent atteindre 3:1

**RULE**  
Les contours, icônes, indicateurs d'état, contrôles et objets graphiques nécessaires à la compréhension doivent avoir **>= 3:1** contre les couleurs adjacentes pertinentes.

**WHY**  
WCAG 2.2 SC 1.4.11 impose 3:1 pour l'information visuelle nécessaire à l'identification des composants et états, ainsi que pour les objets graphiques nécessaires. [S04]

**WHEN TO USE**  
Bordure requise d'un input, checkbox, radio, focus, icône de statut, ligne d'un graphique, barre, point, séparateur qui est le seul signal de structure.

**WHEN NOT TO USE**  
Une bordure purement décorative n'a pas à satisfaire 3:1. Ne pas forcer tous les dividers subtils à être très visibles s'ils ne sont pas nécessaires à l'identification de la structure.

**EXCEPTIONS**  
Les composants inactifs et certaines présentations graphiques essentielles sont exemptés selon WCAG ; tester le cas réel.

**CONFIDENCE: High**

**SOURCES:** [S04], [S18], [S25]

---

## EB-04 — Le focus clavier doit être visible, distinct et robuste

**RULE**  
Chaque élément opérable au clavier doit afficher un focus visible. Pour un système robuste, concevoir un indicateur d'environ 2 px et assurer un contraste perceptible d'au moins 3:1 par rapport aux pixels adjacents lorsqu'il constitue l'information de focus.

**WHY**  
WCAG 2.2 SC 2.4.7 (AA) exige un focus visible. SC 1.4.11 s'applique à l'information non textuelle du focus. SC 2.4.13 donne au niveau AAA un critère plus précis de taille et contraste ; il constitue une bonne cible de conception même quand AA suffit juridiquement. [S06][S07]

**WHEN TO USE**  
Tous les boutons, liens, inputs, tabs, menus, chips interactifs, cartes cliquables et contrôles custom.

**WHEN NOT TO USE**  
Ne pas remplacer un focus visible par un changement de couleur trop subtil, une animation seule ou une ombre presque imperceptible.

**EXCEPTIONS**  
Les contrôles natifs peuvent s'appuyer sur le focus du navigateur si celui-ci reste visible et n'est pas supprimé.

**CONFIDENCE: High**

**SOURCES:** [S06], [S07], [S10]

---

## EB-05 — Ne pas supposer qu'une teinte particulière attire toujours l'attention

**RULE**  
Pour créer une hiérarchie, combiner couleur avec taille, contraste, position, espace, typographie et forme. Ne jamais écrire une règle du type “rouge attire toujours le plus l'œil” ou “une couleur vive garantit le clic”.

**WHY**  
La couleur est une dimension perceptive capable de faciliter la discrimination visuelle, mais une étude de salience UI à grande échelle (1 980 interfaces, 62 participants) a conclu que la couleur n'affectait pas significativement la salience globale dans son analyse, malgré de petits biais de luminosité. Les effets sont donc fortement contextuels. [S31][S32]

**WHEN TO USE**  
Hiérarchie de CTA, badges, alertes, sélection, découverte de contenu.

**WHEN NOT TO USE**  
Ne pas compenser une mauvaise hiérarchie structurelle par une saturation croissante partout.

**EXCEPTIONS**  
Dans des tâches de recherche visuelle contrôlées, une différence de couleur peut être très efficace ; cela ne se transpose pas en classement universel des teintes dans une interface complexe.

**CONFIDENCE: High** sur le rejet des règles universelles ; **Medium** sur les choix précis de salience UI.

**SOURCES:** [S31], [S32]

---

## EB-06 — Dark mode : préserver les rôles, pas les valeurs

**RULE**  
Ne jamais générer le dark mode par inversion RGB/HSL globale. Garder la même sémantique des tokens et remapper chaque rôle vers une valeur spécifique au thème.

**WHY**  
Apple, Carbon, Primer, Atlassian, Fluent et Spectrum utilisent des valeurs différentes par thème. Apple indique explicitement que les couleurs dark ne sont pas nécessairement l'inverse des couleurs light. Carbon fait varier les valeurs des tokens tout en conservant leur rôle. [S10][S11][S14][S17][S19][S23]

**WHEN TO USE**  
Toute interface qui offre light/dark mode ou plusieurs thèmes.

**WHEN NOT TO USE**  
Ne pas créer `darkColor = 255 - lightColor` ou une transformation automatique qui ignore contraste, saturation et élévation.

**EXCEPTIONS**  
Des assets ou éléments très simples peuvent parfois avoir une inversion acceptable ; valider visuellement et par contraste.

**CONFIDENCE: High**

**SOURCES:** [S10], [S11], [S14], [S17], [S19], [S23]

---

## EB-07 — Le dark mode n'est pas intrinsèquement “meilleur pour les yeux”

**RULE**  
Ne pas présenter le dark mode comme une amélioration universelle de lisibilité ou de fatigue visuelle. Pour des contenus textuels denses et de petite taille, conserver un light mode de haute qualité et laisser le choix à l'utilisateur.

**WHY**  
Des travaux expérimentaux sur la polarité d'affichage ont trouvé un avantage de la polarité positive (texte sombre sur fond clair) sur l'acuité et la relecture, y compris chez des adultes plus âgés. Cela ne rend pas le dark mode mauvais, mais invalide l'affirmation générale “dark = plus lisible”. [S33]

**WHEN TO USE**  
Interfaces text-heavy, tableaux denses, documentation, formulaires, lecture longue.

**WHEN NOT TO USE**  
Ne pas interdire le dark mode aux developer tools, analytics, médias ou environnements à faible lumière ; l'avantage dépend de la tâche et du contexte.

**EXCEPTIONS**  
Les préférences individuelles, l'éclairage ambiant, le contenu et la taille du texte modifient l'expérience.

**CONFIDENCE: Medium-High**

**SOURCES:** [S23], [S33]

---

## EB-08 — Graphiques : la couleur doit être redondante avec un autre encodage

**RULE**  
Pour chaque série ou état important d'un graphique, ajouter au moins un signal supplémentaire : label direct, symbole, style de ligne, motif adapté, séparation ou annotation.

**WHY**  
Primer explique qu'il est impossible de définir une grande palette qui soit simultanément sûre pour l'ensemble des déficiences chromatiques et qui maintienne 3:1 entre toutes les couleurs. GitLab et Apple recommandent eux aussi de ne pas dériver le sens du graphique de la couleur seule. [S18][S25][S26]

**WHEN TO USE**  
Line charts, bar charts, pie/donut, heatmaps, dashboards financiers, métriques de sécurité.

**WHEN NOT TO USE**  
Un gradient continu représentant une mesure peut utiliser la couleur comme dimension, mais doit fournir échelle, valeurs, labels et alternatives lorsque nécessaire.

**EXCEPTIONS**  
Les visualisations scientifiques où la couleur est intrinsèque à la donnée peuvent relever de l'exception “essential”, mais la lecture doit rester explicite.

**CONFIDENCE: High**

**SOURCES:** [S04], [S18], [S25], [S26]

---

# 3. Strong industry conventions

## SC-01 — Utiliser des design tokens sémantiques, jamais des couleurs brutes dans les composants

**RULE**  
L'agent doit générer une architecture à deux ou trois niveaux :

```text
palette primitive -> tokens sémantiques -> tokens composant (seulement si nécessaire)
```

Exemples :

```text
blue-600              -> color.action.primary.bg
neutral-950           -> color.text.primary
red-600               -> color.feedback.danger.fg
color.action.primary.bg -> button.primary.bg
```

**WHY**  
Primer interdit l'utilisation directe de ses base colors dans le code produit ; Carbon, Fluent, Atlassian et Spectrum séparent eux aussi valeur et rôle afin de supporter les thèmes et changements à l'échelle. [S10][S11][S14][S17][S19]

**WHEN TO USE**  
Toujours dans un produit maintenable, en particulier si dark mode, rebranding, multi-tenant theming ou white-label sont possibles.

**WHEN NOT TO USE**  
Les hex directs peuvent être tolérés dans des prototypes jetables ou illustrations statiques, pas comme architecture de couleur produit.

**EXCEPTIONS**  
Une valeur de marque contractuelle peut rester primitive, mais les composants doivent la consommer via un token de rôle.

**CONFIDENCE: High**

**SOURCES:** [S10], [S11], [S14], [S17], [S19]

---

## SC-02 — Les neutres doivent porter l'essentiel de l'interface produit

**RULE**  
Utiliser les neutres pour le canvas, les surfaces, la majorité des textes, bordures, dividers, zones de formulaire et contrôles secondaires. Utiliser les couleurs chromatiques avec parcimonie pour hiérarchiser l'action, le feedback, les états et la catégorisation.

**WHY**  
Carbon décrit le gris comme famille dominante et les autres couleurs comme rares et intentionnelles. Spectrum dit que trop de couleur devient visuellement accablant. Fluent réserve les neutres aux surfaces/texte et conseille d'utiliser couleurs partagées et de marque avec parcimonie. [S10][S16][S19]

**WHEN TO USE**  
Dashboards, B2B, enterprise, fintech, developer tools, analytics, productivité.

**WHEN NOT TO USE**  
Ne pas appliquer cette règle telle quelle à une landing page de campagne ou à un contenu éditorial où une surface de marque dominante peut être intentionnelle.

**EXCEPTIONS**  
Un produit très identitaire peut avoir des surfaces de marque étendues ; les zones fonctionnelles doivent néanmoins préserver la lisibilité et la hiérarchie.

**CONFIDENCE: High** comme convention ; **Medium** sur toute proportion exacte.

**SOURCES:** [S10], [S16], [S19], [S20]

---

## SC-03 — Une action primaire dominante par zone fonctionnelle

**RULE**  
Dans une page ou une zone d'action cohérente, n'afficher normalement qu'un CTA de plus haute emphase. Les autres actions doivent être secondary/default/tertiary/ghost.

**WHY**  
Atlassian recommande que le bouton primary n'apparaisse qu'une fois par zone et précise que toutes les vues n'en ont pas besoin. Carbon suit la même hiérarchie de boutons dans sa documentation produit. [S13]

**WHEN TO USE**  
Formulaires, modales, onboarding, settings, tables avec actions globales, wizards, checkout.

**WHEN NOT TO USE**  
Ne pas forcer un primary si aucune action n'est clairement prioritaire.

**EXCEPTIONS**  
Une page très longue peut avoir le même CTA répété pour l'accessibilité/navigation ; ce n'est pas deux priorités concurrentes mais la même action à plusieurs emplacements.

**CONFIDENCE: High**

**SOURCES:** [S13]

---

## SC-04 — Un accent doit être sémantiquement remplaçable

**RULE**  
Utiliser `accent.*` uniquement lorsque la teinte différencie ou catégorise sans porter un sens universel. Test : remplacer l'accent violet par teal ; si le sens produit change, il ne s'agit pas d'un accent.

**WHY**  
Atlassian définit exactement les accents comme des couleurs sans signification spécifique et recommande de les réserver aux catégories, contenus choisis par l'utilisateur et différenciation visuelle. [S12][S11]

**WHEN TO USE**  
Tags, project icons, catégories, avatars, color pickers, séries sans signification fixe.

**WHEN NOT TO USE**  
Erreur, succès, danger, warning, information, focus, action destructive.

**EXCEPTIONS**  
Une couleur de catégorie peut acquérir un sens local dans un produit ; documenter alors ce sens comme token de domaine, pas comme accent générique.

**CONFIDENCE: High**

**SOURCES:** [S12], [S11]

---

## SC-05 — Séparer marque, interaction et statut lorsque leur collision serait ambiguë

**RULE**  
Ne pas réutiliser aveuglément la même couleur pour :

- branding ;
- action primaire ;
- lien ;
- sélection ;
- succès / warning / danger / info.

Si une même teinte doit remplir plusieurs fonctions, les distinguer par structure, tokens, forme et intensité.

**WHY**  
Apple déconseille d'utiliser la même couleur pour éléments interactifs et texte non interactif. Fluent sépare neutral / brand / status ; Atlassian sépare brand et rôles sémantiques. [S11][S19][S24]

**WHEN TO USE**  
Particulièrement si la couleur de marque est rouge, verte, jaune ou proche d'un rôle de feedback.

**WHEN NOT TO USE**  
Ne pas créer artificiellement cinq couleurs très différentes si les affordances et tokens rendent déjà les rôles non ambigus.

**EXCEPTIONS**  
GitHub, par exemple, utilise le vert dans certains primary buttons et dans des contextes de succès. Une convention produit cohérente peut le permettre si les composants ne deviennent pas ambigus.

**CONFIDENCE: High** sur la séparation sémantique ; **Medium** sur la nécessité d'un hue différent.

**SOURCES:** [S11], [S14], [S19], [S24]

---

# 4. Color roles — contrat sémantique complet

Le tableau ci-dessous est conçu pour être directement transformé en règles de skill.

| Rôle | Utiliser pour | Ne PAS utiliser pour | Notes / exceptions | Confiance |
|---|---|---|---|---|
| `primary` / `brand-action` | CTA principal, action importante, sélection forte si la convention du produit l'autorise | toute action, tout texte décoratif, success/error | Le primary est un rôle de priorité, pas “la couleur préférée de la marque partout” | High |
| `secondary` | action de moindre emphase, alternative au primary | deuxième CTA concurrent de même poids ; nouveau hue juste “pour faire joli” | Peut être neutre plutôt qu'une seconde couleur de marque | High |
| `accent` | catégorisation, user-generated color, éléments décoratifs localisés | statuts, danger, succès, warning, info | Doit pouvoir être remplacé sans changer le sens | High |
| `background` | canvas global / base page | cartes, modales et zones qui nécessitent une séparation de couche si le même ton supprime la structure | En dark, le fond de base est souvent le plus sombre | High |
| `surface` | cards, panels, fields, sections, containers | hiérarchie par “rainbow cards” | Utiliser valeur/ton neutre pour la structure | High |
| `surface-elevated` | popovers, modales, menus, éléments au-dessus d'une base | simple décoration | En dark, l'elevated est souvent plus clair que la base | High |
| `border` | limites, séparations, contour de contrôles | créer toute la hiérarchie à lui seul | Bordure essentielle : 3:1 ; divider décoratif peut être plus subtil | High |
| `muted` | sous-surfaces, aides, metadata, éléments de faible priorité | body text si contraste insuffisant ; info importante | “Muted” = moins emphatique, pas illisible | High |
| `text-primary` | corps, titres, valeurs essentielles | disabled / placeholder | Doit être le contraste textuel le plus fort du système normal | High |
| `text-secondary` | labels secondaires, metadata, descriptions | contenu critique si la hiérarchie devient trop faible | Doit encore satisfaire WCAG si c'est du texte fonctionnel | High |
| `text-disabled` | contrôle réellement indisponible | contenu simplement “moins important” | WCAG contraste inactive exempt, mais préserver compréhension | High |
| `success` | issue favorable, confirmation, opération réussie | CTA primaire générique, “on”, croissance financière seule | Ajouter icône/texte si sens important | High |
| `warning` | prudence, risque évitable, état demandant attention avant erreur | erreur déjà survenue ; décoration jaune | Les fonds jaunes exigent souvent texte sombre, pas blanc | High |
| `error/destructive` | erreur, échec, suppression irréversible ou risque grave | notification info, CTA marketing | Réserver le rouge renforce sa valeur signalétique | High |
| `information` | message informatif, processus en cours selon convention | tous les liens/éléments bleus par défaut si cela crée confusion | Si primary est bleu, différencier info par fond subtil + icône + label | High |

**Sources transversales :** [S10][S11][S12][S14][S16][S17][S19][S20]

## 4.1 Tokens minimaux recommandés

Un skill IA devrait générer au minimum :

```text
color.bg.canvas
color.bg.surface
color.bg.surface.subtle
color.bg.surface.elevated
color.bg.inverse

color.text.primary
color.text.secondary
color.text.muted
color.text.disabled
color.text.inverse

color.border.subtle
color.border.default
color.border.strong
color.border.interactive
color.focus

color.action.primary.bg
color.action.primary.fg
color.action.primary.hover
color.action.primary.active
color.action.secondary.bg
color.action.secondary.fg

color.feedback.info.bg / fg / border / icon
color.feedback.success.bg / fg / border / icon
color.feedback.warning.bg / fg / border / icon
color.feedback.danger.bg / fg / border / icon

color.accent.{family}.{subtle|default|strong}
```

### Règle d'implémentation

Un composant ne doit jamais choisir `#2563eb` parce qu'il “veut du bleu”. Il doit demander `color.action.primary.bg`, `color.feedback.info.fg`, etc. La palette primitive décide ensuite quelle valeur satisfait le rôle dans chaque thème.


# 5. Color distribution — quantité, saturation et hiérarchie

## CD-01 — Remplacer 60/30/10 par un “color budget” contextuel

**RULE**  
L'agent ne doit pas appliquer de ratio universel. Il doit estimer la densité fonctionnelle et attribuer un budget de surface chromatique.

**Heuristique opérationnelle — non normative :**

| Contexte | Surfaces neutres | Brand / accent | Couleurs sémantiques | Interprétation |
|---|---:|---:|---:|---|
| Dashboard B2B / enterprise dense | ~85–95% | ~5–15% | localisées, souvent <5% à un instant donné | La couleur doit aider à trouver l'important, pas teinter tout le workspace |
| Fintech / cybersecurity / healthcare opérationnel | ~85–95% | ~3–10% | uniquement là où un état/risk existe | Plus le coût d'erreur est élevé, moins la décoration doit concurrencer les signaux |
| Developer tool / analytics | ~80–95% hors data-viz | ~5–15% | localisées | Les données peuvent être chromatiques ; le chrome de l'app reste calme |
| Productivity / B2C utility | ~70–90% | ~10–30% | localisées | Plus de personnalité possible sans perdre la hiérarchie |
| Landing / marketing | **pas de ratio fixe** | peut dominer de grandes surfaces | états UI toujours réservés | Le contenu de marque peut occuper le hero ; les contrôles restent hiérarchisés |

**IMPORTANT** — Ces plages sont une **synthèse heuristique** issue de la convergence des systèmes étudiés (“neutral dominant”, “colors sparingly”, “avoid overusing brand colors”), pas un résultat expérimental. Elles ne doivent jamais être utilisées comme critère de conformité. [S10][S16][S19]

**WHY**  
Le vrai objectif n'est pas une proportion décorative mais le maintien de la hiérarchie : si chaque région est colorée, la couleur cesse d'être un signal distinctif.

**WHEN TO USE**  
Génération initiale d'un thème ou audit d'un écran trop coloré.

**WHEN NOT TO USE**  
Ne pas mesurer au pixel près et refuser un écran parce qu'il est à 82% plutôt qu'à 85% de neutres.

**EXCEPTIONS**  
Data visualizations, médias, illustrations et brand campaigns peuvent dépasser largement ces budgets.

**CONFIDENCE: Medium** pour la direction ; **Low-Medium** pour les chiffres précis.

**SOURCES:** [S10], [S16], [S19]

---

## CD-02 — Une palette peut être grande ; un écran ne doit pas montrer toutes ses couleurs

**RULE**  
Distinguer **taille du système** et **diversité simultanée** :

- le système peut contenir une grande rampe de neutres ;
- 1 famille brand primaire suffit généralement ;
- 1 famille secondaire/accent est optionnelle ;
- conserver les familles sémantiques `info`, `success`, `warning`, `danger` ;
- une palette data-viz séparée peut contenir plusieurs hues ;
- un écran produit ne doit instancier que les rôles réellement nécessaires.

**WHY**  
Spectrum possède de nombreuses familles de couleurs mais demande de les utiliser avec parcimonie. Geist dispose de 10 scales et répartit leurs niveaux selon les rôles UI. Un grand vocabulaire de tokens ne justifie donc pas une grande variété visible simultanément. [S16][S20]

**WHEN TO USE**  
Création d'un design system scalable.

**WHEN NOT TO USE**  
Ne pas réduire la palette primitive à 3 couleurs si le produit nécessite data-viz, états, accessibilité et dark mode.

**EXCEPTIONS**  
Un produit mono-marque extrêmement minimal peut fonctionner avec neutral + brand + feedback.

**CONFIDENCE: High** comme architecture ; **Medium** pour le nombre de familles.

**SOURCES:** [S16], [S20], [S17]

---

## CD-03 — Saturation élevée = ressource rare

**RULE**  
Dans un workspace dense, limiter les couleurs à forte chroma aux éléments de forte priorité ou de petite surface : CTA principal, état critique, sélection, badge important, série de données focalisée.

**Heuristique IA :** si plus de 2 familles fortement saturées sont visibles hors data-viz et qu'elles n'ont pas chacune une fonction claire, réduire la saturation ou neutraliser l'une d'elles.

**WHY**  
Spectrum et Fluent recommandent une application parcimonieuse de la couleur. Atlassian relie explicitement les niveaux d'emphase au contraste avec la surface. La saturation seule n'est cependant pas une mesure universelle d'attention, d'où une règle de parcimonie plutôt qu'un seuil numérique. [S11][S16][S19][S32]

**WHEN TO USE**  
Dashboards, tables, settings, applications productives, dark mode.

**WHEN NOT TO USE**  
Ne pas désaturer les signaux au point de supprimer leur distinction ou leur contraste.

**EXCEPTIONS**  
Landing pages, illustrations, visualisations catégorielles, campagnes ou jeux peuvent employer davantage de chroma.

**CONFIDENCE: Medium-High**

**SOURCES:** [S11], [S16], [S19], [S32]

---

## CD-04 — Les grandes surfaces de couleur doivent être moins agressives que les petits accents

**RULE**  
Plus une couleur couvre de surface, plus sa chroma et/ou son contraste local doit généralement être contrôlé. Préférer :

- tint / subtle background pour banners, cards, sections ;
- version bold/emphasis pour bouton, badge, icon ou petite zone ;
- texte adapté au fond (`on-*` / inverse token), jamais un blanc supposé universel.

**WHY**  
Atlassian, Spectrum, Fluent et Primer proposent explicitement plusieurs niveaux `subtle`/`bold` ou des rôles distincts pour backgrounds, borders et text. Spectrum réserve certaines intensités à des backgrounds précis et change même entre texte noir/blanc selon la luminance. [S11][S12][S14][S16][S17]

**WHEN TO USE**  
Callouts, alerts, hero cards, sélection, KPI cards.

**WHEN NOT TO USE**  
Ne pas mettre un rouge/bleu/vert saturé plein écran pour signaler un statut standard.

**EXCEPTIONS**  
Écrans d'alarme très critique ou brand campaign ; valider fatigue visuelle et contraste.

**CONFIDENCE: High**

**SOURCES:** [S11], [S12], [S14], [S16], [S17]

---

## CD-05 — Un gradient doit avoir une fonction, pas seulement combler le vide

**RULE**  
Autoriser un gradient si au moins une condition est vraie :

1. il encode une dimension continue de données ;
2. il matérialise une identité de marque déjà établie ;
3. il crée une transition spatiale/élévation intentionnelle ;
4. il appartient à une zone marketing non opérationnelle.

Sinon, préférer une surface unie.

**WHY**  
WCAG note que les gradients compliquent l'évaluation du contraste : le point de contraste minimum doit être testé. Les design systems étudiés privilégient généralement des surfaces/tokens prédictibles pour le produit. GitLab recommande les couleurs solides pour la prédictibilité. [S04][S27]

**WHEN TO USE**  
Hero marketing, visualisation de magnitude, aura de marque, background non critique.

**WHEN NOT TO USE**  
Inputs, boutons primaires, cards fonctionnelles, tableaux, alertes, backgrounds de texte si le gradient fait varier le contraste sous le contenu.

**EXCEPTIONS**  
Un composant peut avoir un gradient brand si le contraste est garanti sur **toute** la zone sous le texte/contrôle.

**CONFIDENCE: High** pour la contrainte de contraste ; **Medium** pour la préférence stylistique.

**SOURCES:** [S04], [S27]

---

# 6. Light mode / Dark mode

## DM-01 — Construire deux palettes sémantiquement équivalentes, pas deux palettes mathématiquement symétriques

**RULE**  
Pour chaque token sémantique, définir une valeur light et une valeur dark indépendamment :

```text
color.text.primary.light  -> neutral-950
color.text.primary.dark   -> neutral-50

color.bg.canvas.light     -> neutral-0
color.bg.canvas.dark      -> neutral-950

color.action.primary.light -> brand-600
color.action.primary.dark  -> brand-400/500  # selon contraste réel
```

Puis vérifier chaque paire sur son fond réel.

**WHY**  
Carbon conserve les mêmes rôles mais change les valeurs selon les thèmes ; Primer fait varier les scales par color mode ; Fluent fournit des alias distincts light/dark ; Apple demande des variantes bright/dim. [S10][S14][S17][S23]

**WHEN TO USE**  
Tout produit multi-thème.

**WHEN NOT TO USE**  
Ne pas calculer le dark depuis le light par inversion ou `lightness = 100 - lightness`.

**EXCEPTIONS**  
Aucune au niveau du système ; quelques couleurs primitives peuvent accidentellement coïncider.

**CONFIDENCE: High**

**SOURCES:** [S10], [S14], [S17], [S23]

---

## DM-02 — En dark mode, créer la profondeur principalement par niveaux de surface

**RULE**  
Utiliser une rampe de surfaces sombre cohérente. Typiquement :

```text
canvas/base       = le plus sombre
surface           = légèrement plus clair
surface-elevated  = encore légèrement plus clair
popover/modal     = niveau élevé + bordure/ombre si nécessaire
```

Ne pas dépendre exclusivement de l'ombre, moins lisible sur fond sombre.

**WHY**  
Apple utilise des backgrounds `base` plus sombres et `elevated` plus lumineux. Carbon indique qu'en dark theme les layers deviennent un pas plus clairs à mesure qu'ils s'empilent. [S10][S23]

**WHEN TO USE**  
Cards, menus, modales, side panels, command palettes.

**WHEN NOT TO USE**  
Ne pas multiplier les niveaux de gris pour chaque carte : 3–5 niveaux fonctionnels suffisent généralement à une hiérarchie produit.

**EXCEPTIONS**  
Un écran media/terminal très plat peut volontairement utiliser moins de niveaux.

**CONFIDENCE: High** sur la direction ; **Medium** sur le nombre de niveaux.

**SOURCES:** [S10], [S23]

---

## DM-03 — Éviter le noir pur comme obligation, pas comme interdit

**RULE**  
Par défaut, utiliser un near-black neutre pour le canvas si plusieurs niveaux de surface sont nécessaires. Autoriser `#000` lorsque le produit a une raison claire : média immersif, OLED, terminal, identité, contraste souhaité.

**WHY**  
Carbon propose des thèmes dark basés sur `#262626` et `#161616`, GitLab utilise `#18171d` comme surface dark de référence, et Apple recommande des backgrounds système avec niveaux base/elevated. Cela montre qu'un dark mode mature n'exige pas le noir absolu. [S10][S25][S23]

**WHEN TO USE**  
Interfaces multi-layer, SaaS généralistes.

**WHEN NOT TO USE**  
Ne pas transformer “avoid pure black” en dogme d'accessibilité : WCAG n'interdit pas `#000`.

**EXCEPTIONS**  
Media, code/terminal, contexte de faible lumière, économie OLED.

**CONFIDENCE: Medium**

**SOURCES:** [S10], [S23], [S25]

---

## DM-04 — Réajuster chroma et brightness des couleurs sémantiques en dark

**RULE**  
Ne pas réutiliser les mêmes valeurs RGB pour status/accent dans les deux modes. En dark :

- tester si la couleur devient visuellement trop vibrante ;
- souvent réduire la chroma ou déplacer la luminosité ;
- préserver le rôle sémantique et le contraste ;
- vérifier le texte `on-color` séparément.

**WHY**  
Fluent indique que les shared colors changent saturation et brightness en dark mode. Apple demande des variantes adaptées ; Atlassian et Carbon mappent leurs tokens à des valeurs différentes par thème. [S11][S17][S19][S23]

**WHEN TO USE**  
Brand, info, success, warning, danger, selected, focus.

**WHEN NOT TO USE**  
Ne pas “désaturer par principe” si cela fait perdre la reconnaissance ou le contraste.

**EXCEPTIONS**  
Certains signaux critiques peuvent conserver une forte chroma si elle reste confortable et accessible.

**CONFIDENCE: High** sur le remapping ; **Medium** sur la direction précise de saturation.

**SOURCES:** [S11], [S17], [S19], [S23]

---

## DM-05 — Tester le dark mode comme un produit séparé

**RULE**  
Exécuter les mêmes vérifications sur light **et** dark :

- contrastes textuels ;
- non-text contrast ;
- focus ;
- hover/pressed/selected ;
- semantic backgrounds ;
- charts ;
- images/logo ;
- disabled ;
- bordures ;
- overlays / alpha blending.

**WHY**  
La conformité d'une paire de couleurs en light ne prédit pas celle d'une autre paire en dark ; les design systems utilisent des mappings spécifiques par thème. [S10][S14][S17][S23]

**WHEN TO USE**  
À chaque release de theme ou ajout de component.

**WHEN NOT TO USE**  
Ne pas valider une palette en regardant uniquement des swatches isolés.

**EXCEPTIONS**  
Aucune.

**CONFIDENCE: High**

**SOURCES:** [S10], [S14], [S17], [S23]

---

# 7. Accessibility — règles détaillées pour agent IA

## 7.1 Texte

- [ ] `text-primary`, `text-secondary`, helper text, labels et placeholders fonctionnels atteignent 4.5:1 s'ils sont de taille normale. [S03]
- [ ] Le “muted” reste lisible ; ne pas choisir un gris simplement parce qu'il semble subtil.
- [ ] Le texte coloré conserve 4.5:1 ; une teinte “sémantique” n'est pas exemptée.
- [ ] Ne pas arrondir un ratio sous le seuil vers le haut : 4.49 n'est pas 4.5.
- [ ] AAA 7:1 peut être une cible pour petits textes critiques, mais n'est pas la baseline générale AA. [S03]

## 7.2 Composants

- [ ] Les informations nécessaires pour identifier un contrôle ou un état ont 3:1 contre les couleurs adjacentes. [S04]
- [ ] Les bordures décoratives peuvent être plus subtiles si le composant reste identifiable sans elles.
- [ ] Les composants désactivés sont exemptés de plusieurs exigences de contraste, mais doivent rester reconnaissables comme indisponibles. [S03][S04][S10]
- [ ] Ne pas confondre `disabled`, `read-only` et `secondary` : un contenu secondaire reste actif et doit être lisible.

## 7.3 Focus

- [ ] Le focus clavier n'est jamais supprimé. [S06]
- [ ] Utiliser un ring/outline clair ; la cible AAA de SC 2.4.13 constitue un bon standard interne. [S07]
- [ ] Sur surfaces variables, préférer un focus à deux tons ou un inset de contraste — Carbon et le W3C documentent ce pattern. [S06][S10]

## 7.4 Erreurs et formulaires

- [ ] Une erreur possède au minimum : texte explicite + relation avec le champ ; icône si utile ; couleur en renfort.
- [ ] Une bordure rouge seule n'est pas suffisante. [S05]
- [ ] Le warning n'est pas une error : warning = prévenir avant faute / risque ; error = faute ou échec déjà présent. [S11]
- [ ] Sur fond jaune, choisir texte sombre si nécessaire au contraste ; ne pas imposer `white-on-warning`. [S11][S16]

## 7.5 Daltonisme et statuts

- [ ] Profit/perte : `+/-`, flèches, labels et valeur, pas vert/rouge seul.
- [ ] Sévérité : labels `Critical / High / Medium / Low` + icon/shape, pas une heatmap de couleurs seule.
- [ ] Online/offline : texte ou symbole distinct, pas point vert/rouge seul.
- [ ] Selected/unselected : check, border, fill, icon ou position, pas hue seul.
- [ ] Graph series : hue + line style / marker / direct label. [S18][S26]

## 7.6 Graphiques

- [ ] Texte des axes et labels : 4.5:1. [S18]
- [ ] Marks significatifs : viser 3:1 contre le background. [S18][S25]
- [ ] Utiliser des séparateurs si deux zones adjacentes ne sont pas distinguables ; Primer recommande notamment espaces/dividers. [S18]
- [ ] Limiter pie/donut à peu de slices lorsque possible ; Primer recommande au plus cinq slices pour préserver la comparaison. [S18]
- [ ] Pour lignes multiples : styles de trait et/ou markers différents. [S18]

---

# 8. Product context — adapter la couleur à la tâche

## PC-01 — Dashboard dense

**RULE**  
Neutral-first. Réserver la couleur aux séries, anomalies, filtres sélectionnés, états et CTA réellement prioritaires.

**WHY**  
Une interface dense contient déjà beaucoup de signaux ; ajouter de la chroma à chaque card réduit la capacité de la couleur à différencier les événements importants. Les systèmes Carbon/Spectrum/Fluent convergent vers des neutres dominants. [S10][S16][S19]

**USE**  
85–95% de surfaces neutres comme point de départ heuristique, hors data-viz.

**AVOID**  
“Rainbow dashboard” où chaque KPI a sa couleur permanente sans signification.

**EXCEPTIONS**  
Dashboard éditorial ou consumer très brandé.

**CONFIDENCE: High** direction / **Medium** proportion.

---

## PC-02 — Landing page

**RULE**  
Autoriser davantage de brand color, gradients, illustration et surfaces chromatiques, tout en conservant une hiérarchie CTA unique et des zones de texte accessibles.

**WHY**  
Une landing optimise persuasion et identité plutôt que scanning répétitif d'une application métier. Les contraintes de contraste restent identiques.

**USE**  
Hero, social proof accent, visual storytelling, sections de marque.

**AVOID**  
Plusieurs CTA saturés de couleurs différentes ; texte fin sur gradient ; semantic red/green utilisés comme décoration.

**EXCEPTIONS**  
Landing intégrée dans une console produit : rapprocher du système produit.

**CONFIDENCE: Medium-High**

---

## PC-03 — B2B / Enterprise

**RULE**  
Favoriser la prévisibilité : neutres, une action brand claire, sémantiques stables, focus robuste, data-viz accessible.

**WHY**  
Les workflows enterprise sont répétitifs, denses et à coût d'erreur élevé ; la cohérence des rôles a plus de valeur que la nouveauté stylistique.

**USE**  
Tables, forms, settings, admin, CRM/ERP, management consoles.

**AVOID**  
Décoration chromatique dans chaque section, statut par hue seul, primary CTA multiples.

**EXCEPTIONS**  
Portails customer-facing avec composante de marque forte.

**CONFIDENCE: High**

---

## PC-04 — B2C

**RULE**  
Autoriser davantage d'expression de marque dans les surfaces, illustrations et accents, mais ne jamais affaiblir les conventions sémantiques ou l'accessibilité.

**WHY**  
La différenciation et l'émotion peuvent jouer un rôle plus important dans l'expérience B2C, mais les contraintes perceptives ne changent pas.

**USE**  
Personalization, onboarding, empty states, achievement, discovery.

**AVOID**  
Gamification chromatique qui masque la structure ou fait ressembler toute interaction à une récompense.

**CONFIDENCE: Medium**

---

## PC-05 — Developer tool

**RULE**  
Dark mode first-class mais pas forcément dark-only. Utiliser une base neutre forte, accent d'interaction clair, syntax highlighting comme système séparé, statuts explicites.

**WHY**  
Geist, GitHub Primer et GitLab montrent des palettes fonctionnelles très structurées, avec light/dark themes et tokens séparés. Les petites tailles de texte imposent une attention particulière au contraste. [S14][S20][S27]

**USE**  
IDEs web, observability, API tools, deployment consoles.

**AVOID**  
Syntax colors trop nombreuses ou saturées au même niveau ; terminal-like noir pur imposé si la lisibilité longue souffre.

**CONFIDENCE: High** convention.

---

## PC-06 — Fintech

**RULE**  
Prioriser exactitude et redondance : montants, variation, risque et statut ne doivent jamais dépendre uniquement de vert/rouge.

**WHY**  
Les conséquences financières augmentent le coût d'une mauvaise interprétation ; WCAG exige déjà une alternative à la couleur seule. [S05]

**USE**  
`+$42.10 ↑ 3.2%` vs `-$42.10 ↓ 3.2%`, accompagnés éventuellement de vert/rouge.

**AVOID**  
Solde positif = vert sans signe ; transaction échouée = point rouge seul.

**EXCEPTIONS**  
Aucune pour l'information critique.

**CONFIDENCE: High**

---

## PC-07 — Cybersecurity

**RULE**  
Traiter la couleur de sévérité comme renfort : `Critical`, `High`, `Medium`, `Low` doivent être textuels et/ou iconographiques.

**WHY**  
Une palette red/orange/yellow peut être difficile à distinguer, et l'importance de l'alerte ne doit pas disparaître avec une déficience chromatique. [S05]

**USE**  
Incident queues, vulnerabilities, SIEM, IAM alerts.

**AVOID**  
Toutes les alerts en néon ; red = “security aesthetic” même sans danger.

**CONFIDENCE: High**

---

## PC-08 — AI SaaS

**RULE**  
Ne pas choisir violet/purple-gradient par défaut. Choisir la palette à partir de la marque, du produit, de la hiérarchie et de l'accessibilité. Si le contenu généré par IA doit être distingué, utiliser un token dédié + label/icon/provenance, pas une couleur seule.

**WHY**  
Il n'existe aucune preuve que le violet soit intrinsèquement “AI”. Les systèmes actuels divergent : Carbon possède des tokens AI avec une aura bleue, ce qui illustre l'absence de convention chromatique universelle. [S15]

**USE**  
Accent AI seulement si la marque ou le système le justifie.

**AVOID**  
Violet + cyan gradient comme raccourci automatique de “futuristic AI”.

**EXCEPTIONS**  
Si l'identité de marque possède déjà le violet, il reste parfaitement valable.

**CONFIDENCE: Medium** sur l'anti-pattern / **Low** sur toute généralisation de tendance.

---

## PC-09 — Productivity

**RULE**  
Préférer des surfaces calmes, une sélection claire, un accent brand limité et des semantic colors localisées.

**WHY**  
La couleur doit aider à revenir rapidement à la tâche plutôt que devenir une couche de bruit permanent.

**USE**  
Editors, notes, tasks, calendars, docs.

**AVOID**  
Colorer tous les projets, boutons et cards à forte saturation simultanément.

**CONFIDENCE: Medium-High**

---

## PC-10 — Analytics

**RULE**  
Séparer strictement **UI palette** et **data-viz palette**. Les couleurs de séries représentent des données, pas des états de composant.

**WHY**  
GitLab documente explicitement une palette data-viz séparée du reste de l'UI ; Primer impose des redondances non chromatiques. [S18][S25]

**USE**  
Charts, heatmaps, cohort tables, funnels.

**AVOID**  
Réutiliser `danger-red` comme couleur arbitraire d'une série si elle n'est pas négative.

**CONFIDENCE: High**

---

## PC-11 — Healthcare / clinical

**RULE**  
Appliquer le niveau de prudence d'un produit à haut risque : labels explicites, redondance iconographique, contrastes avec marge, aucune information clinique critique codée par couleur seule.

**WHY**  
WCAG couvre la perception générale, mais les interfaces de santé peuvent ajouter des exigences réglementaires ou institutionnelles spécifiques ; ces exigences doivent supplanter ce guide lorsqu'elles existent. [S05]

**USE**  
Patient portals, clinical dashboards, lab results, alerts.

**AVOID**  
Utiliser green = “safe” ou red = “danger” sans texte clinique explicite.

**EXCEPTIONS**  
Standards du domaine, conventions hospitalières ou dispositifs réglementés peuvent imposer des mappings spécifiques.

**CONFIDENCE: High** pour l'accessibilité ; **Medium** pour le styling général.


# 9. Brand personality — traduire des attributs en décisions sans pseudo-science

## Principe général

La littérature montre que des associations couleur–émotion et couleur–personnalité existent, mais elles ne sont ni universelles ni suffisamment stables pour devenir des règles absolues d'interface. Elliot & Maier décrivent une littérature encore fortement dépendante du contexte ; Jonauskaite et al. trouvent des patterns transnationaux mais aussi des différences prédites par pays, langue et géographie ; Palmer & Schloss montrent que les préférences peuvent être apprises via les associations avec des objets ; Labrecque & Milne trouvent des associations de brand personality dans un contexte marketing. [S28][S29][S30][S34]

**Règle IA :** utiliser les associations de personnalité comme **priors faibles à modérés**, puis les filtrer par contexte, marque existante, accessibilité et conventions produit.

## Matrice de décision

| Attribut recherché | Décision palette recommandée | Ne pas déduire automatiquement | Confiance |
|---|---|---|---|
| `premium` | neutres raffinés, nombre réduit de chromas, accents précis, contraste maîtrisé | “premium = noir + or” | Medium |
| `serious` | chroma modérée, hiérarchie claire, faible bruit décoratif, états stables | “serious = bleu obligatoire” | Medium |
| `trustworthy` | cohérence sémantique, contraste fort, faible ambiguïté ; cool hues possibles comme point de départ | “le bleu crée la confiance chez tout le monde” | Medium |
| `technical` | neutres, accent froid possible, surfaces structurées, data/syntax colors disciplinées | “tech = cyan néon” | Medium |
| `futuristic` | dark + accent électrique ou gradient possible, mais limité et fonctionnel | “futuristic = violet” | Low-Medium |
| `friendly` | tints plus doux, accents plus chaleureux ou variés, contrastes accessibles | “friendly = pastel faible contraste” | Medium |
| `playful` | plus de diversité chromatique, accents/catégories expressifs, petites surfaces saturées | “playful = rainbow partout” | Medium |
| `minimal` | neutral scale + 1 accent principal + semantics | “minimal = monochrome total” | High comme convention |
| `enterprise` | neutral-first, brand stable, semantic states explicites, saturation limitée | “enterprise = boring gray” | High comme convention |
| `luxury` | saturation souvent plus faible si l'objectif est héritage/timelessness ; palette retenue | “luxe = noir” | Medium |
| `energetic` | chroma plus élevée sur accents/CTA/illustrations, forte séparation hiérarchique | “énergique = rouge partout” | Medium |

## BP-01 — Serious / trustworthy / enterprise

**RULE**  
Commencer par un système neutre à forte lisibilité, puis ajouter une famille de marque stable. Une gamme froide/bleutée peut être testée comme hypothèse de compétence/trust, mais ne doit pas être imposée.

**WHY**  
Labrecque & Milne ont trouvé dans des études de branding des liens entre hues et dimensions de personnalité, notamment autour de la compétence, mais les revues générales insistent sur les effets contextuels. [S28][S30]

**WHEN TO USE**  
B2B, enterprise, finance, infrastructure, sécurité.

**WHEN NOT TO USE**  
Ne pas remplacer une identité existante forte par “corporate blue” uniquement pour suivre une convention.

**EXCEPTIONS**  
Des marques rouges, oranges, violettes ou vertes peuvent être extrêmement crédibles si le système est cohérent.

**CONFIDENCE: Medium**

**SOURCES:** [S28], [S30]

---

## BP-02 — Premium / luxury

**RULE**  
Pour une personnalité luxury classique ou patrimoniale, tester une saturation plus faible et une palette restreinte. Pour une marque premium explicitement innovante, une saturation élevée peut au contraire mieux servir la perception recherchée.

**WHY**  
Une recherche publiée dans le *Journal of Consumer Research* (2026 issue, mise en ligne en 2025) rapporte, sur sept études, que les couleurs moins saturées augmentaient le statut perçu des marques de luxe via la perception d'héritage/continuité ; l'effet était atténué pour les marques récentes et inversé lorsque la marque était positionnée comme innovante. Ce résultat porte sur le branding/luxury products, pas directement sur les contrôles UI. [S35]

**WHEN TO USE**  
Marketing, hero, brand surfaces, illustrations, premium positioning.

**WHEN NOT TO USE**  
Ne pas désaturer les semantic colors jusqu'à perdre contraste et identification.

**EXCEPTIONS**  
Luxury innovant / fashion-forward : la saturation peut servir la visual prominence.

**CONFIDENCE: Medium** pour branding ; **Low-Medium** pour transposition UI.

**SOURCES:** [S35]

---

## BP-03 — Friendly / playful / energetic

**RULE**  
Augmenter d'abord la variété ou la chroma sur les accents, illustrations, avatars, badges et empty states ; ne pas augmenter simultanément le nombre de CTA primaires ou la saturation des surfaces opérationnelles.

**WHY**  
Les associations hue/saturation peuvent influencer la personnalité perçue, mais l'expérience produit exige une hiérarchie stable. [S28][S30]

**WHEN TO USE**  
Consumer SaaS, collaboration, creator tools, education.

**WHEN NOT TO USE**  
Formulaires à risque, alertes, tables très denses où l'expression chromatique nuit au scanning.

**EXCEPTIONS**  
Une marque très expressive peut conserver des surfaces colorées si le contenu et les contrôles restent accessibles.

**CONFIDENCE: Medium**

**SOURCES:** [S28], [S30]

---

## BP-04 — Futuristic / AI / cybersecurity aesthetic

**RULE**  
Traiter dark + neon + gradients comme une direction artistique, pas comme une propriété intrinsèque de la technologie. Utiliser au maximum une ou deux familles électriques fortes dans la couche fonctionnelle ; le reste doit être neutre ou discret.

**WHY**  
Aucune preuve académique solide ne relie une teinte “AI” ou “cyber” universelle à la compréhension d'un produit. Les effets de couleur dépendent des associations apprises et du contexte. [S30][S34]

**WHEN TO USE**  
Marketing, hero, visual identity, decorative data moments.

**WHEN NOT TO USE**  
Body text néon, warnings confondus avec brand accents, plusieurs glows concurrents dans un dashboard.

**EXCEPTIONS**  
Brand identity déjà établie.

**CONFIDENCE: Low-Medium**

**SOURCES:** [S30], [S34]

---

# 10. Real-world analysis — systèmes et produits reconnus

> Cette section compare les règles documentées des design systems utilisés par de grandes familles de produits. Il s'agit d'une analyse de conventions réelles, pas d'un classement esthétique.

| Produit / système | Pattern couleur observé | Ce qui semble généralisable | Ce qui reste propre à la marque |
|---|---|---|---|
| **IBM Carbon** | Gray family dominante, blue comme action primaire IBM, couleurs additionnelles rares ; layering light/dark ; tokens role-based | neutral-first, tokens sémantiques, surface hierarchy | blue comme primary global IBM |
| **Adobe Spectrum** | 11 grays par thème, couleurs utilisées avec parcimonie ; semantic accent/negative/notice/positive/informative ; ramps construites par contraste | système perceptuel + contrast targets, sparse chroma | sélection exacte des hues Adobe |
| **Atlassian** | rôles neutral/brand/info/success/warning/danger/discovery/accent ; accent remplaçable ; light/dark mappings | séparation brand/semantic/accent ; niveaux d'emphase | discovery role et palette Atlassian |
| **GitHub Primer** | base tokens jamais utilisés directement ; functional/component tokens ; accent/success/attention/danger ; multiples thèmes | token abstraction, thème, data-viz multi-encoding | green primary dans certains flows GitHub, rôles open/closed/done |
| **Microsoft Fluent 2** | neutral/brand/status aliases ; surfaces et text neutral ; brand non dominant sur grandes surfaces ; dark adjusts saturation/brightness | séparation neutral/brand/status, alias tokens | couleurs produits M365 |
| **Vercel Geist** | deux backgrounds principaux ; scale structurée : 1–3 backgrounds, 4–6 borders, 7–8 strong BG, 9–10 text/icons | ramp par rôle et contraste, simplicité developer-tool | esthétique quasi monochrome Vercel |
| **Stripe** | palette brand traduite dans l'UI via espace perceptuel et contrast targets ; recherche de “visual weight” uniforme | palette perceptuellement structurée, accessibilité intégrée à la génération | signature chromatique Stripe |
| **GitLab Pajamas** | UI color et data-viz séparées ; semantic tokens ; dark mode ; préférence pour solid colors prédictibles | séparation UI/data, contrôle de contraste, token semantics | combinaison purple/orange brand GitLab |
| **Apple HIG** *(hors SaaS web mais utile pour dark mode)* | semantic dynamic colors, base/elevated dark backgrounds, pas d'inversion mécanique | dark-mode role mapping, elevation by surface | APIs et materials spécifiques Apple |

## Patterns communs forts dans l'échantillon

1. **La valeur brute n'est pas l'API de design.** Les tokens sémantiques sont l'interface stable. [S10][S11][S14][S17]
2. **Les neutres portent la majorité de la structure produit.** [S10][S16][S19][S20]
3. **La couleur sémantique est intentionnelle et rare.** [S11][S16][S19]
4. **Light et dark utilisent des valeurs différentes pour les mêmes rôles.** [S10][S11][S14][S17][S23]
5. **Les data visualizations nécessitent une palette et des règles spécifiques.** [S18][S25]
6. **La hiérarchie CTA se fait par niveaux d'emphase, pas par multiplication de couleurs concurrentes.** [S13]
7. **Le contraste est conçu dans le système, pas vérifié uniquement à la fin.** Spectrum et Stripe utilisent explicitement le contraste/perceptual lightness pour construire leurs scales. [S16][S21]

## Ce qui relève plutôt du style ou de la marque

- GitHub peut associer le vert à certaines actions primaires ; ce n'est pas une règle SaaS universelle. [S14]
- Vercel pousse beaucoup plus loin la neutralité/monochromie que certains autres produits. [S20]
- Stripe conserve une identité plus chromatique mais la structure dans un système perceptuel. [S21]
- Atlassian possède un rôle `discovery` spécifique aux nouveautés/onboarding. [S11]
- Les systèmes n'utilisent pas tous les mêmes hues pour chaque rôle ; la **sémantique et le contraste** convergent davantage que les hex codes.

---

# 11. Failure modes / anti-patterns

## FM-01 — Trop de couleurs sans rôle

**SYMPTOM**  
Chaque card, section, bouton ou metric possède une teinte différente.

**WHY IT FAILS**  
La couleur perd sa capacité de signal ; la hiérarchie dépend alors d'une mémorisation arbitraire.

**FIX**  
Neutraliser les surfaces et conserver la couleur uniquement pour action, état, sélection, catégorisation ou marque.

**CONFIDENCE: High** — convention convergente. [S10][S16][S19]

---

## FM-02 — Accent partout

**SYMPTOM**  
Brand/accent color sur titres, icônes, liens, borders, cards, boutons et selected states en même temps.

**WHY IT FAILS**  
Plus rien ne paraît prioritaire. Fluent avertit que l'abus de brand color dilue la hiérarchie. [S19]

**FIX**  
Choisir 1–3 rôles d'accent principaux : CTA primaire, sélection/focus selon système, moments de marque ciblés.

**CONFIDENCE: High**

---

## FM-03 — CTA concurrents

**SYMPTOM**  
Deux ou trois boutons pleins, saturés et de poids identique dans la même zone.

**WHY IT FAILS**  
L'utilisateur doit reconstruire la priorité à partir du texte au lieu de la voir dans la hiérarchie.

**FIX**  
Un primary ; autres actions default/secondary/tertiary. [S13]

**CONFIDENCE: High**

---

## FM-04 — Gradient gratuit

**SYMPTOM**  
Gradient multicolore derrière chaque card, border ou CTA sans rôle de données ou de marque.

**WHY IT FAILS**  
Ajoute du bruit et crée des zones de contraste variables difficiles à tester. [S04]

**FIX**  
Surface unie ou gradient limité aux zones non opérationnelles ; tester le point de contraste le plus faible.

**CONFIDENCE: High** pour accessibilité / **Medium** pour style.

---

## FM-05 — Saturation excessive

**SYMPTOM**  
Multiples couleurs bold de grande surface dans un dashboard.

**WHY IT FAILS**  
La compétition visuelle augmente ; les status et CTA perdent leur rareté.

**FIX**  
Réduire chroma des surfaces, conserver bold pour petits éléments prioritaires.

**CONFIDENCE: Medium-High**

---

## FM-06 — Dark mode = palette light inversée

**SYMPTOM**  
Même hues avec lightness retournée automatiquement ; warnings fluorescents ; surfaces sans profondeur.

**WHY IT FAILS**  
La perception et les contrastes ne sont pas symétriques ; les design systems utilisent des mappings spécifiques. [S10][S17][S23]

**FIX**  
Remapper token par token, reconstruire surfaces/elevation, retester chaque pair.

**CONFIDENCE: High**

---

## FM-07 — Dark mode plat noir + cartes presque noires

**SYMPTOM**  
Canvas, cards, modals et menus ont des valeurs quasi identiques ; seules les ombres tentent d'indiquer la profondeur.

**WHY IT FAILS**  
Les couches deviennent difficiles à distinguer.

**FIX**  
Créer une rampe base/surface/elevated ; en dark, l'élévation peut correspondre à une surface plus claire. [S10][S23]

**CONFIDENCE: High**

---

## FM-08 — Muted = faible contraste

**SYMPTOM**  
Secondary text gris très clair sur blanc ou gris sombre sur noir.

**WHY IT FAILS**  
La hiérarchie stylistique ne dispense pas de 4.5:1 pour le texte normal. [S03]

**FIX**  
Créer la hiérarchie avec poids, taille, espace et un contraste **toujours conforme**.

**CONFIDENCE: High**

---

## FM-09 — Couleurs sémantiques ambiguës

**SYMPTOM**  
Vert = success + primary + “online” + catégorie ; rouge = error + destructive + brand + série de chart.

**WHY IT FAILS**  
Un même signal visuel acquiert plusieurs interprétations.

**FIX**  
Séparer les tokens et ajouter signaux non chromatiques ; changer de hue lorsque la collision est réellement ambiguë.

**CONFIDENCE: High**

---

## FM-10 — Red/green-only analytics

**SYMPTOM**  
P&L, KPI, heatmap ou incident state lisible uniquement via rouge/vert.

**WHY IT FAILS**  
Violation du principe WCAG color-only ; défaut pour de nombreux utilisateurs. [S05]

**FIX**  
Signes +/−, flèches, labels, valeurs, icônes, formes.

**CONFIDENCE: High**

---

## FM-11 — “AI purple” générique

**SYMPTOM**  
Violet-indigo-cyan gradient ajouté uniquement parce que le produit contient de l'IA.

**WHY IT FAILS**  
Aucun fondement perceptif universel ; risque de convergence visuelle avec la catégorie et de perte de différenciation.

**FIX**  
Déduire la couleur de la personnalité, du contexte, de la marque et des besoins sémantiques. L'IA peut posséder un rôle visuel dédié sans être violet.

**CONFIDENCE: Low-Medium** — observation de tendance, pas règle scientifique.

---

## FM-12 — Psychologie des couleurs transformée en vérité

**SYMPTOM**  
“Blue = trustworthy”, “red = urgency”, “black = luxury” utilisés comme règles absolues.

**WHY IT FAILS**  
Les associations varient avec culture, langue, apprentissage, contexte et positionnement. [S29][S30][S34]

**FIX**  
Traiter ces associations comme hypothèses à tester, jamais comme exigences.

**CONFIDENCE: High** sur le rejet de l'universalité.

---

# 12. Trends / weak evidence

## 12.1 “AI purple”, aurora gradients, neon dark

**STATUT : Trend / weak evidence**

Ces directions peuvent être esthétiquement efficaces mais ne disposent pas d'un fondement qui les rende supérieures pour les produits AI. Un agent ne doit les choisir que si elles correspondent à la marque ou à une direction artistique explicite.

## 12.2 Glassmorphism / tinted glass

**STATUT : Context-dependent / weak evidence**

Le matériau translucide peut créer de la profondeur, mais la couleur sous-jacente varie ; la lisibilité doit être testée avec les backgrounds réels. Apple recommande de choisir les materials selon leur fonction sémantique et non selon la couleur apparente qu'ils produisent. [S24]

## 12.3 Black = luxury

**STATUT : Weak simplification**

Le noir peut participer à une esthétique premium mais aucune règle universelle ne l'impose. La recherche récente sur le luxury branding supporte davantage une interaction saturation × heritage/innovation qu'un hue unique. [S35]

## 12.4 60/30/10

**STATUT : Stylistic heuristic, not evidence-backed UI rule**

Ne pas coder cette règle comme contrainte de skill. Utiliser plutôt les budgets contextuels de ce document.

---

# 13. Decision Framework

Exécuter ces étapes dans l'ordre.

## Step 1 — Identifier le type de surface

```text
marketing ? -> plus de liberté brand/decorative
product UI ? -> neutral-first
high-risk workflow ? -> réduire décoration, renforcer redondance
analytics ? -> séparer UI palette et data-viz palette
```

## Step 2 — Inventorier les rôles avant les couleurs

Créer la liste :

```text
canvas
surface
surface-elevated
text-primary
text-secondary
text-disabled
border-subtle/default/interactive
focus
primary action
secondary action
accent
info
success
warning
danger
```

Si un rôle n'est pas nécessaire, ne pas inventer une couleur pour lui.

## Step 3 — Choisir la neutral scale

Déterminer :

- neutral pur ou légèrement teinté ;
- combien de niveaux light ;
- combien de niveaux dark ;
- séparation canvas/surface/elevated ;
- contraste des textes.

## Step 4 — Choisir la famille brand/action

Questions :

1. La marque possède-t-elle déjà une couleur ?
2. Peut-elle atteindre les contrastes requis dans ses rôles interactifs ?
3. Entre-t-elle en collision avec success/warning/danger ?
4. Une variante plus sombre/claire/chroma différente suffit-elle ?
5. Le CTA doit-il être brand-colored ou neutral high-emphasis ?

## Step 5 — Construire les semantic ramps

Pour chaque `info/success/warning/danger` créer :

```text
subtle background
foreground text/icon
border
bold background
on-bold foreground
```

Puis vérifier les contrastes.

## Step 6 — Créer light et dark séparément

Garder les mêmes token names ; changer les values.

## Step 7 — Réserver l'accent

N'ajouter une famille accent que s'il existe un besoin réel : catégorie, user color, discovery, visual differentiation.

## Step 8 — Vérifier la hiérarchie

- un primary par zone ;
- aucun statut ne concurrence le CTA sans raison ;
- aucun decorative accent n'est plus fort qu'une information critique ;
- muted reste lisible.

## Step 9 — Vérifier accessibilité

Exécuter la checklist §16.

## Step 10 — Vérifier la personnalité de marque

Appliquer les associations de couleur uniquement après les étapes fonctionnelles et accessibilité.

---

# 14. Color Selection Decision Tree

```text
START
 |
 |-- La couleur transmet-elle un sens ?
 |      |
 |      |-- OUI --> Le sens est-il info/success/warning/danger ?
 |      |             |
 |      |             |-- OUI --> utiliser token semantic dédié
 |      |             |            + texte/icône/forme redondante
 |      |             |
 |      |             |-- NON --> sens de domaine stable ?
 |      |                          |
 |      |                          |-- OUI --> créer token de domaine documenté
 |      |                          |-- NON --> probablement accent/catégorie
 |      |
 |      |-- NON --> Est-ce une action ?
 |                    |
 |                    |-- OUI --> action principale de la zone ?
 |                    |             |
 |                    |             |-- OUI --> primary/high emphasis
 |                    |             |-- NON --> neutral/secondary/tertiary
 |                    |
 |                    |-- NON --> Est-ce structure/surface/texte ?
 |                                  |
 |                                  |-- OUI --> neutral role
 |                                  |-- NON --> accent/decorative possible
 |
 |-- Le rôle passe-t-il WCAG sur le fond réel ?
 |      |-- NON --> ajuster lightness/chroma/hue ou ajouter border/outline
 |
 |-- La même couleur signifie-t-elle autre chose ailleurs ?
 |      |-- OUI --> séparer tokens / modifier rendu / ajouter second signal
 |
 |-- Dark mode ?
 |      |-- remapper la valeur ; ne pas inverser
 |
 |-- Trop de couleurs fortes visibles ?
 |      |-- réduire accents / neutraliser surfaces / baisser chroma
 |
 END
```

---

# 15. Light/Dark Mode Checklist

- [ ] Même sémantique des tokens dans les deux modes.
- [ ] Aucune inversion RGB/HSL automatique utilisée comme solution finale.
- [ ] Canvas, surface et elevated ont des valeurs distinctes et cohérentes.
- [ ] En dark, les overlays/popovers sont perceptibles sans dépendre uniquement d'une ombre.
- [ ] `text-primary`, `secondary`, `muted`, placeholder et disabled ont été testés séparément.
- [ ] Brand/action hue a été retuné pour dark si nécessaire.
- [ ] Success/warning/danger/info ont des valeurs dark dédiées.
- [ ] Warning background a un foreground réellement lisible, souvent sombre si le jaune est lumineux.
- [ ] Focus est visible sur **toutes** les surfaces.
- [ ] Borders essentielles passent 3:1 ; dividers décoratifs ne sont pas inutilement forts.
- [ ] Charts ont des palettes compatibles avec les deux thèmes.
- [ ] Logos, illustrations et images ont été vérifiés dans les deux modes.
- [ ] Les alpha colors ont été testées après composition sur chaque fond possible.
- [ ] Le dark mode n'est pas présenté comme “meilleur pour les yeux” par défaut.
- [ ] Le choix système/utilisateur est respecté lorsque pertinent.

---

# 16. Accessibility Checklist

- [ ] WCAG 2.2 utilisée comme baseline normative actuelle. [S01][S08]
- [ ] Texte normal >= 4.5:1. [S03]
- [ ] Grand texte >= 3:1. [S03]
- [ ] Information UI/graphique nécessaire >= 3:1 contre couleurs adjacentes. [S04]
- [ ] La couleur n'est jamais le seul canal d'information. [S05]
- [ ] Focus clavier visible. [S06]
- [ ] Focus renforcé proche du standard SC 2.4.13 lorsque possible. [S07]
- [ ] Error = texte explicite + signal visuel, pas border rouge seule.
- [ ] Warning, success, info possèdent texte/icon lorsque leur sens est important.
- [ ] Disabled est identifiable et n'est pas utilisé pour du contenu simplement secondaire.
- [ ] Red/green states ont signe, texte, forme ou icon.
- [ ] Selected/unselected ne dépend pas uniquement de hue.
- [ ] Chart series utilisent shape/line style/direct labels en plus de la couleur. [S18][S26]
- [ ] Mark de chart significatif atteint 3:1 contre le background lorsque requis. [S18][S25]
- [ ] Texte de chart atteint 4.5:1. [S18]
- [ ] Toute zone de texte sur gradient est testée au point de contraste le plus faible. [S04]
- [ ] Light et dark sont testés séparément.

---

# 17. Anti-pattern Checklist

Si une réponse est “oui”, l'agent doit revoir sa palette :

- [ ] Ai-je appliqué 60/30/10 comme une loi sans contexte ?
- [ ] Ai-je plus d'un CTA de plus haute emphase dans la même zone ?
- [ ] Ai-je utilisé une semantic color comme décoration ?
- [ ] Ai-je utilisé un accent pour transmettre danger/success/warning ?
- [ ] Ai-je utilisé la même couleur pour interaction et contenu non interactif de manière ambiguë ?
- [ ] Ai-je plus de deux familles fortement saturées concurrentes hors data-viz sans justification ?
- [ ] Ai-je coloré chaque card/KPI simplement pour “faire moderne” ?
- [ ] Ai-je rendu `muted` sous les seuils de contraste ?
- [ ] Ai-je construit le dark mode par inversion ?
- [ ] Ai-je utilisé un dark mode quasi noir sans vraie hiérarchie de surfaces ?
- [ ] Ai-je utilisé rouge/vert comme unique signal ?
- [ ] Ai-je placé du texte sur un gradient non testé ?
- [ ] Ai-je choisi purple/cyan uniquement parce que le produit est “AI” ?
- [ ] Ai-je choisi noir uniquement parce que la marque doit sembler “luxury” ?
- [ ] Ai-je utilisé une couleur de chart sémantique pour une catégorie qui n'a pas ce sens ?
- [ ] Ai-je hardcodé des hex dans les composants au lieu de tokens ?

---

# 18. Rules suitable for direct conversion into AI instructions

Le bloc suivant est volontairement impératif et peut être transformé presque tel quel en `SKILL.md`.

```text
COLOR SYSTEM RULES

1. Define semantic color roles before selecting raw color values.
2. Never hardcode raw palette colors inside product components when semantic tokens exist.
3. Keep product workspaces neutral-dominant unless the user explicitly requests a brand-heavy or marketing treatment.
4. Do not apply the 60/30/10 rule as a scientific or universal UI law.
5. Use one primary brand/action color family by default. Add a secondary brand hue only when it has a documented role.
6. Treat accent colors as semantically swappable. If changing the hue changes meaning, create a semantic/domain token instead.
7. Reserve danger/error, warning, success, and information colors for their intended states. Do not use them decoratively when that could create ambiguity.
8. Never communicate essential information with color alone. Add text, icon, shape, line style, position, or another redundant cue.
9. Ensure normal text contrast is at least 4.5:1 and large text at least 3:1 under WCAG 2.2 AA.
10. Ensure non-text visual information required to identify controls, states, or meaningful graphics reaches at least 3:1 against relevant adjacent colors.
11. Always provide a visible keyboard focus indicator. Prefer a robust ring/outline that remains visible across all surfaces.
12. Muted and secondary text must remain accessible; muted does not mean low-contrast.
13. Disabled controls may be de-emphasized, but do not use disabled styling for merely secondary content.
14. Use only one highest-emphasis primary CTA per coherent action area unless repeated instances perform the same action.
15. Use neutral surfaces for most dense SaaS dashboards. As a heuristic, start around 85–95% neutral large-area surfaces, then adjust by context. Do not treat this percentage as normative.
16. Keep high-chroma colors scarce in dense product UIs. If more than two strong chromatic families compete outside data visualization and lack clear roles, reduce or remove one.
17. Use subtle/tinted semantic backgrounds for large areas and bold semantic colors for smaller, higher-priority elements.
18. Do not assume white text works on every saturated background. Compute contrast and choose an appropriate on-color token.
19. Do not generate dark mode by inverting light mode values. Preserve token roles and independently map dark values.
20. In dark mode, create depth with distinct base/surface/elevated tones; elevated dark surfaces often become lighter than the base.
21. Retune saturation and lightness of brand and semantic colors in dark mode when needed; validate contrast after composition.
22. Pure black is allowed but not required. Prefer near-black when multiple dark surface levels are needed.
23. Do not claim dark mode is universally more readable or better for eye strain. Preserve a strong light mode for text-heavy workflows.
24. Separate application UI colors from data-visualization colors.
25. In charts, never rely on hue alone. Pair series colors with direct labels, markers, line styles, shapes, or separators.
26. For financial gain/loss, security severity, healthcare status, or other high-stakes states, always show explicit text/symbols in addition to color.
27. Treat brand-personality color associations as contextual priors, not universal truths.
28. Do not automatically choose blue for trust, black for luxury, red for urgency, or purple gradients for AI.
29. For premium/heritage positioning, lower saturation may be tested as a branding hypothesis; for innovation-led luxury, higher saturation may be appropriate. Do not transfer this research blindly to functional UI controls.
30. A gradient must have a function: data, brand, spatial transition, or marketing. Otherwise prefer a solid surface.
31. When text or controls sit on a gradient, test the least-contrasting point, not the average color.
32. Avoid using transparency when it makes contrast unpredictable across possible backgrounds; prefer solid tokens for critical UI.
33. Every color token must be validated in light and dark themes, including rest, hover, active, selected, focus, disabled, error, and inverse states.
34. Prefer semantic role consistency over hue consistency across themes.
35. When an existing design system is present, inherit its semantic color contracts instead of inventing a new palette.
```

## Optional machine-readable decision hints

```yaml
color_strategy:
  normative_baseline: WCAG_2_2
  architecture: semantic_tokens
  product_default: neutral_first
  primary_cta_per_area: 1
  color_only_information: forbidden
  normal_text_contrast_min: 4.5
  large_text_contrast_min: 3.0
  required_non_text_contrast_min: 3.0
  dark_mode:
    invert_palette: false
    remap_semantic_tokens: true
    layered_surfaces: true
  accent:
    carries_semantic_meaning: false
  data_visualization:
    separate_palette: true
    hue_only_differentiation: false
  heuristics:
    dense_product_neutral_surface_share: "85-95% (non-normative starting range)"
    competing_high_chroma_families_outside_dataviz: "<=2 unless justified"
  prohibited_assumptions:
    - "60/30/10 is a universal UI law"
    - "blue universally means trust"
    - "black universally means luxury"
    - "purple universally means AI"
    - "dark mode is universally easier to read"
```

---

# 19. Confidence map

## High confidence

- WCAG contrast thresholds and use-of-color requirements.
- Visible focus requirement.
- Semantic token architecture.
- Light/dark theme remapping rather than raw inversion.
- Color + non-color redundancy for status/data.
- Neutral-dominant structure as a widespread SaaS/product convention.
- Separation of semantic roles from accent/decorative roles.
- One highest-emphasis CTA per coherent area as a strong design-system convention.

## Medium confidence

- Exact amount of saturation appropriate to a category.
- Near-black preferred over pure black for generic multi-layer SaaS.
- Color budgets expressed as percentages.
- Brand personality mappings such as cool colors for technical/serious contexts.
- Lower saturation for premium/luxury positioning when transferred from branding research to SaaS marketing.

## Low confidence / trend

- Purple as an AI color.
- Neon as inherently futuristic/technical.
- Black as inherently luxury.
- Any universal percentage formula such as 60/30/10.
- Claims that a specific hue universally maximizes attention or conversion.

---

# 20. Source registry

Toutes les URLs ci-dessous ont été consultées ou vérifiées pour cette recherche. Lorsque la page ne fournit pas de date de publication stable, la date d'accès est indiquée.

### Normes et accessibilité

**[S01] W3C — WCAG 2 Overview.** Current standard overview; indique que WCAG 2.2 est la version recommandée actuelle.  
URL: https://www.w3.org/WAI/standards-guidelines/wcag/  
Accessed: 2026-10-06.

**[S02] W3C — What's New in WCAG 2.2.** WCAG 2.2 publié comme W3C Recommendation le 2023-10-05.  
URL: https://www.w3.org/WAI/standards-guidelines/wcag/new-in-22/  
Published: 2023-10-05.

**[S03] W3C — Understanding SC 1.4.3: Contrast (Minimum).** 4.5:1 normal text, 3:1 large text, exceptions.  
URL: https://www.w3.org/WAI/WCAG22/Understanding/contrast-minimum  
Accessed: 2026-10-06.

**[S04] W3C — Understanding SC 1.4.11: Non-text Contrast.** 3:1 pour information graphique/UI nécessaire ; guidance sur gradients.  
URL: https://www.w3.org/WAI/WCAG22/Understanding/non-text-contrast.html  
Accessed: 2026-10-06.

**[S05] W3C — Understanding SC 1.4.1: Use of Color.** Couleur non utilisée comme seul moyen visuel de transmettre l'information.  
URL: https://www.w3.org/WAI/WCAG22/Understanding/use-of-color.html  
Accessed: 2026-10-06.

**[S06] W3C — Understanding SC 2.4.7: Focus Visible.**  
URL: https://www.w3.org/WAI/WCAG22/Understanding/focus-visible  
Updated: 2026-09-06 (page W3C consultée en 2026-10).

**[S07] W3C — Understanding SC 2.4.13: Focus Appearance.** Level AAA ; détails sur surface et contraste du focus.  
URL: https://www.w3.org/WAI/WCAG22/Understanding/focus-appearance  
Accessed: 2026-10-06.

**[S08] W3C — WCAG 3 Introduction.** Indique que WCAG 3 est un draft incomplet et que WCAG 2 reste le standard actuel.  
URL: https://www.w3.org/WAI/standards-guidelines/wcag/wcag3-intro/  
Updated: 2026-09-25.

**[S09] W3C — WCAG 2.2 Approved as an ISO Standard.** ISO/IEC 40500:2025.  
URL: https://www.w3.org/WAI/news/2025-10-21/wcag22-iso/  
Published: 2025-10-21.

### Design systems et produits

**[S10] IBM Carbon Design System — Color overview.** Neutral gray dominant, blue primary action IBM, couleurs additionnelles utilisées avec parcimonie, layering light/dark, role-based tokens.  
URL: https://www.carbondesignsystem.com/building-blocks/foundations/color/overview  
Updated: 2026-09-25.

**[S11] Atlassian Design System — Color.** Roles neutral/brand/information/success/warning/danger/discovery/accent/inverse, emphasis, light/dark.  
URL: https://atlassian.design/foundations/color  
Accessed: 2026-10-06.

**[S12] Atlassian Design System — Accents.** Accent sans signification spécifique ; test de swappability ; guidance contraste.  
URL: https://atlassian.design/foundations/color/accents  
Accessed: 2026-10-06.

**[S13] Atlassian Design System — Button.** Primary button réservé à l'action la plus importante et une fois par zone.  
URL: https://atlassian.design/server/components/buttons/  
Accessed: 2026-10-06.

**[S14] GitHub Primer — Color usage.** Base colors non utilisées directement ; functional/component tokens ; themes ; roles ; high-contrast targets.  
URL: https://primer.style/product/getting-started/foundations/color-usage/  
Accessed: 2026-10-06.

**[S15] IBM Carbon Design System — Color tokens.** Background/layer/text/border/focus/support tokens et tokens AI actuels.  
URL: https://www.carbondesignsystem.com/building-blocks/foundations/color/tokens  
Updated: 2026-09-25.

**[S16] Adobe Spectrum — Color system.** Grays par thème, colors sparingly/intentionally, semantic colors, target contrast, perceptual progression.  
URL: https://spectrum.adobe.com/page/color-system/  
Accessed: 2026-10-06.

**[S17] Microsoft Fluent 2 — Color tokens.** Alias neutral/brand/status, valeurs light/dark distinctes.  
URL: https://fluent2.microsoft.design/color-tokens/  
Accessed: 2026-10-06.

**[S18] GitHub Primer — Data visualization.** Mark/background contrast, stroke styles, markers, chart color accessibility, pie/donut guidance.  
URL: https://primer.style/product/ui-patterns/data-visualization/  
Accessed: 2026-10-06.

**[S19] Microsoft Fluent 2 — Color.** Neutral surfaces/text, brand color non surutilisée, semantic colors, dark-mode saturation/brightness changes.  
URL: https://fluent2.microsoft.design/color/  
Accessed: 2026-10-06.

**[S20] Vercel Geist — Colors.** 10 scales ; backgrounds 1/2 ; scale roles 1–3 background, 4–6 border, 7–8 strong backgrounds, 9–10 text/icons.  
URL: https://vercel.com/geist/colors  
Accessed: 2026-10-06.

**[S21] Stripe — Designing accessible color systems.** Usage d'un espace perceptuellement uniforme, contrast targets, uniform visual weight.  
URL: https://stripe.com/blog/accessible-color-systems  
Published: 2019-10-15.

**[S22] GitLab Pajamas — CSS / semantic tokens and dark-mode overrides.**  
URL: https://design.gitlab.com/product-foundations/css/  
Accessed: 2026-10-06.

**[S23] Apple Human Interface Guidelines — Dark Mode.** Dark colors not necessarily inversions, semantic adaptive colors, base/elevated backgrounds, contrast guidance.  
URL: https://developer.apple.com/design/human-interface-guidelines/dark-mode  
Page change log includes: 2024-08-06 update; accessed 2026-10-06.

**[S24] Apple Human Interface Guidelines — Color.** Avoid same color for interactive/noninteractive meaning, inclusive color, light/dark variants, Liquid Glass guidance.  
URL: https://developer.apple.com/design/human-interface-guidelines/color  
Change log: updated 2025-12-16 for Liquid Glass; accessed 2026-10-06.

**[S25] GitLab Pajamas — Data visualization color.** Separate data palette, 3:1 surface contrast, sequences, separators, light/dark.  
URL: https://design.gitlab.com/data-visualization/color/  
Accessed: 2026-10-06.

**[S26] Apple Human Interface Guidelines — Charts.** Do not rely solely on color; use shapes/patterns/other signals.  
URL: https://developer.apple.com/design/human-interface-guidelines/charts  
Accessed: 2026-10-06.

**[S27] GitLab Pajamas — Product color.** WCAG contrast guidance, semantic color usage, préférence pour solid colors dans les cas critiques/prédictibles.  
URL: https://design.gitlab.com/product-foundations/color/  
Accessed: 2026-10-06.

### Recherche académique / perception / branding

**[S28] Labrecque, L. I., & Milne, G. R. — “Exciting red and competent blue: the importance of color in marketing.”** *Journal of the Academy of Marketing Science*, 40, 711–727. Empirical studies on hue, saturation/value and brand personality.  
URL: https://doi.org/10.1007/s11747-010-0245-y  
Published online: 2011-01-28; issue: 2012.

**[S29] Jonauskaite, D. et al. — “Universal Patterns in Color-Emotion Associations Are Further Shaped by Linguistic and Geographic Proximity.”** *Psychological Science*, 31(10), 1245–1260. 4,598 participants, 30 nations, 22 languages ; universal patterns with cultural modulation.  
URL: https://doi.org/10.1177/0956797620948810  
Published: 2020.

**[S30] Elliot, A. J., & Maier, M. A. — “Color Psychology: Effects of Perceiving Color on Psychological Functioning in Humans.”** *Annual Review of Psychology*, 65, 95–120. Review emphasizing contextual/boundary conditions and maturity limits of the literature.  
URL: https://doi.org/10.1146/annurev-psych-010213-115035  
Published: 2014.

**[S31] Treisman, A. M., & Gelade, G. — “A feature-integration theory of attention.”** *Cognitive Psychology*, 12(1), 97–136. Color as separable perceptual feature in visual search/integration theory.  
URL: https://doi.org/10.1016/0010-0285(80)90005-5  
Published: 1980.

**[S32] Jiang, Y. et al. — “UEyes: Understanding Visual Saliency across User Interface Types.”** CHI 2023. Eye-tracking dataset: 62 participants, 1,980 UIs ; analysis concludes color did not significantly affect overall visual saliency in the studied UI set.  
URL: https://doi.org/10.1145/3544548.3581096  
Published: 2023-04-19.

**[S33] Piepenbrock, C., Mayr, S., Mund, I., & Buchner, A. — “Positive display polarity is advantageous for both younger and older adults.”** *Ergonomics*, 56(7), 1116–1124.  
URL: https://pubmed.ncbi.nlm.nih.gov/23654206/  
DOI: https://doi.org/10.1080/00140139.2013.790485  
Published: 2013.

**[S34] Palmer, S. E., & Schloss, K. B. — “An ecological valence theory of human color preference.”** *PNAS*, 107(19), 8877–8882. Preferences linked to affective associations with colored objects.  
URL: https://doi.org/10.1073/pnas.0906172107  
Published online: 2010-04-26.

**[S35] Zhou, X., Xiao, C., Yoon, S., & Zhu, H. — “Color of Status: Color Saturation, Brand Heritage, and Perceived Status of Luxury Brands.”** *Journal of Consumer Research*, 52(6), 1232–1252. Seven studies ; low saturation increased perceived status for heritage-oriented luxury, with boundary/reversal for innovation positioning.  
URL: https://academic.oup.com/jcr/article/52/6/1232/8120421  
DOI: https://doi.org/10.1093/jcr/ucaf029  
Published online: 2025-04-26; issue: 2026-04.

---

# 21. Final synthesis for skill authors

Le skill ne devrait pas commencer par :

> “Choisis une couleur primaire, une secondaire et une accent puis applique 60/30/10.”

Il devrait commencer par :

> “Identifie le contexte produit, les rôles sémantiques, la hiérarchie d'action et les contraintes de contraste. Construis un système de tokens dont les valeurs sont spécifiques à chaque thème. Utilise les neutres pour la structure, réserve la chroma à des fonctions explicites, et ne laisse jamais la couleur porter seule une information essentielle.”

La conclusion la plus robuste de la recherche est donc que la **color intelligence d'un agent IA n'est pas sa capacité à choisir de beaux hex codes**. C'est sa capacité à :

1. attribuer correctement des rôles ;
2. contrôler la quantité de signal chromatique ;
3. préserver des contrastes mesurables ;
4. distinguer branding, interaction, statut et data-viz ;
5. adapter ces rôles au light/dark mode ;
6. traiter la personnalité de marque comme un contexte, pas comme une superstition ;
7. expliquer et auditer ses choix.

