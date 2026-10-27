# Présentation orale — 8 minutes, 7 diapositives

Mohammed El Amine BENBAKRETI et Mohamed Aziz BEN ROMDHANE. Diapositives : `presentation_APT.pptx`, soit une page de titre et les 7 diapos ci-dessous. Comme la page de garde du rapport, la page de titre ne compte pas. Les notes de l'orateur de chaque diapo reprennent la partie « À dire ».

**Fil conducteur.** Les modèles qualitatifs se passent de paramètres. L'article de Cosme *et al.* (2023) défend une exécution *asynchrone* des règles. Nous avons reproduit ses deux expériences avec `ecco`. Le calcul est confirmé ; la validation écologique est fragile.

| # | Diapo | Durée | Chrono | Visuel |
|---|---|---|---|---|
| 1 | Modéliser un écosystème sans ses paramètres | 0:50 | 0:50 | une équation à paramètres face à une règle `A+ >> P-` |
| 2 | L'article : une revue historique et une proposition | 0:50 | 1:40 | frise chronologique et les 4 objectifs |
| 3 | EDEN et `ecco` en pratique | 1:10 | 2:50 | le fichier `APT.rr` et un mini-schéma état → règle → état |
| 4 | Expérience 1 : figure 5 reproduite | 1:30 | 4:20 | `figures/figure5_APT.png` |
| 5 | Expérience 2 : figure 7 reproduite | 1:30 | 5:50 | `figures/figure7_sync_async.png` |
| 6 | Quelle confiance accorder aux résultats ? | 1:20 | 7:10 | deux colonnes « solide / fragile » |
| 7 | Perspectives et message à retenir | 0:50 | 8:00 | 4 puces et une phrase finale |

Les diapos 4 et 5 sont le cœur de l'oral (3 minutes). Si tu dépasses, raccourcis la diapo 2.

---

## 1. Modéliser un écosystème sans ses paramètres (0:50)

**Message.** Les modèles classiques demandent des paramètres qu'on ne sait pas mesurer ; les modèles qualitatifs s'en passent.

- À gauche, une équation de type proie-prédateur : 4 paramètres à mesurer (croissance, capacité, prédation…).
- À droite, une règle : « si A est présente, P peut disparaître ». Chaque espèce est seulement présente ou absente.
- Annonce : « Nous reproduisons deux expériences d'un article de 2023, avec l'outil `ecco` développé à l'IBISC (Évry). »

## 2. L'article : une revue historique et une proposition (0:50)

**Message.** C'est surtout une revue historique, qui débouche sur une proposition : le cadre EDEN.

- Frise : Camerano (1880) → modèles à compartiments (années 1950) → *loop analysis* (Levins, 1974) → raisonnement qualitatif (QSIM, Garp3) → modèles état-transition → EDEN.
- Chaque formalisme est un assemblage de propriétés (Fig. 4 de l'article), jugé sur 4 objectifs : saisir la dynamique qualitative, limiter les hypothèses, expliquer, prédire.
- EDEN combine 4 choix : qualitatif, événements discrets, mise à jour **asynchrone**, **possibiliste**.

## 3. EDEN et `ecco` en pratique (1:10)

**Message.** On écrit les règles, et `ecco` calcule tous les états accessibles.

- Montrer `APT.rr` : 3 espèces (A amibe, P paramécie, T tétrahymena), 4 règles R1–R4.
- Une règle est **applicable** si sa condition est vraie et si elle change l'état.
- **Asynchrone** : une seule règle à la fois, n'importe laquelle. **Synchrone** : toutes les règles applicables en même temps.
- Le résultat est le **graphe de transitions d'états** : nœuds = états, arcs = règles. Un **état stable** est un état d'où plus rien ne bouge.

## 4. Expérience 1 : figure 5 reproduite (1:30)

**Message.** On retrouve exactement la figure de l'article : 6 états, 2 fins possibles ({T} et ∅), 3 trajectoires.

- La figure (c) est le graphe affiché par `ecco` dans le notebook `APT_asynchrone`, avec le nom des états. Contour épais = état stable.
- Pour finir en {T}, il faut R1 (A mange P) puis R4 (A meurt faute de P), **avant** R2 (A mange T).
- Le graphe confirme l'affirmation de l'article : « l'extinction de P est nécessaire mais pas suffisante pour {T} ».
- Depuis AP (T déjà éteinte), seule la fin ∅ reste possible : c'est la notion de bassin.

## 5. Expérience 2 : figure 7 reproduite (1:30)

**Message.** En synchrone le modèle ne prédit que ∅ ; en asynchrone il prédit aussi {T}, observé expérimentalement.

- En synchrone, R1, R2 et R3 se déclenchent ensemble : A mange P et T au même instant, donc T ne survit jamais.
- `ecco` n'a pas de mode synchrone. Nous avons regroupé à la main les règles tirées ensemble (`APT_synchrone.rr`) : S1 = R1, R2, R3 depuis APT ; S2 = R4 depuis A.
- `ecco` affiche alors la chaîne APT → A → ∅, comme la Fig. 7a.
- Limite à dire : ce codage ne vaut que depuis {APT}, ce n'est pas un mode synchrone générique.

## 6. Quelle confiance accorder aux résultats ? (1:20)

**Message.** La reproduction valide le **calcul**, pas l'**écologie**.

| Solide | Fragile |
|---|---|
| graphes calculés directement par `ecco` | synchrone codé à la main, valable seulement depuis {APT} |
| graphe asynchrone identique, arc par arc, à la Fig. 5c | une seule étude expérimentale (Weatherby *et al.*, 1998), aucun chiffre dans l'article |
| calcul déterministe, vérifiable à la main sur 8 états | règles dérivées des mêmes expériences : la validation n'est pas indépendante |
| tous les points vérifiables de l'article se lisent sur les graphes | exemple jouet (3 espèces, 4 règles) ; « possible » ne veut pas dire « probable » |

## 7. Perspectives et message à retenir (0:50)

- Valider sur les autres combinaisons d'espèces du même pool expérimental.
- Attacher des probabilités au même graphe pour estimer la probabilité de {T}.
- Comparer d'autres modes de mise à jour, et tester la robustesse règle par règle.
- Apprendre les règles à partir des données au lieu de les écrire à la main.

**Phrase finale :** « L'ordre des événements compte : un modèle qualitatif asynchrone garde des issues qu'un modèle synchrone efface. Mais "possible" ne veut pas dire "probable". »

---

# 5 questions probables du jury

**1. Pourquoi l'asynchrone serait-il plus réaliste que le synchrone ?**
Le synchrone suppose que tous les événements possibles arrivent au même instant, donc que tous les processus vont à la même vitesse : ici, A mangerait P et T exactement en même temps. Or ces vitesses dépendent des effectifs et des interactions, qu'on ne connaît pas. L'asynchrone ne tranche pas : il garde tous les ordres possibles. Il n'est pas « plus réaliste » en soi, il est plus **prudent**. Il manque moins d'issues réelles, mais il peut proposer des trajectoires qui n'arrivent jamais. Ici, il retrouve {T}, observé expérimentalement.

**2. Votre reproduction prouve-t-elle que le modèle APT est juste ?**
Non. Elle prouve que les figures 5 et 7 découlent bien des 4 règles : le calcul est déterministe, vérifiable à la main sur 8 états, et il coïncide arc par arc avec les figures de l'article. La validité écologique repose sur une seule étude en microcosmes, dont les données ne sont pas dans l'article. De plus, les règles ont été construites à partir des mêmes expériences. Reproduire un calcul, ce n'est pas valider un modèle.

**3. `ecco` n'a pas de mode synchrone : comment avez-vous obtenu la figure 7a ?**
Une règle `ecco` peut modifier plusieurs variables à la fois. Nous avons donc regroupé en une seule règle celles qui doivent se déclencher ensemble : S1 (`A+, P+, T+ >> P-, T-`) pour R1, R2 et R3 depuis APT, et S2 (`A+, P-, T- >> A-`) pour R4 depuis A. `ecco` affiche alors la chaîne APT → A → ∅ de la figure 7a. C'est une limite que nous assumons : ce codage ne vaut que depuis {APT}. Depuis AT, par exemple, un vrai pas synchrone (R2 et R4 ensemble) mènerait à ∅, alors qu'aucune de nos règles ne s'y applique.

**4. Que se passe-t-il avec un modèle plus grand ?**
Avec n espèces, il y a 2ⁿ états possibles, et en asynchrone le nombre de trajectoires peut exploser. `ecco` calcule de façon symbolique, avec des diagrammes de décision (libDDD/libITS). Il regroupe ensuite les états en composantes (cycles, bassins, états stables) et permet le *model-checking*, par exemple « {T} est-il atteignable ? ». Mais l'interprétation devient difficile, ce que les auteurs reconnaissent. APT, avec ses 6 états, ne teste pas du tout cet aspect.

**5. Pourquoi ne pas utiliser un modèle probabiliste, comme une chaîne de Markov ?**
Il faudrait estimer une probabilité pour chaque transition, donc disposer de données, ce qui manque justement (objectif 2 de l'article). Le possibilisme liste toutes les évolutions possibles sans les pondérer. Son défaut : on ne sait pas si {T} est une issue rare ou fréquente. Une perspective naturelle serait d'attacher des taux au même graphe d'états et de comparer les probabilités obtenues aux fréquences observées.

**À préparer aussi :** si vous montrez les notebooks, « que signifient les numéros des nœuds ? » Dans le graphe asynchrone : 6 = APT, 5 = AT, 3 = AP, 2 = A, 4 = {T}, 1 = ∅ ; dans le synchrone : 3 = APT, 2 = A, 1 = ∅. Ce sont les numéros de composantes d'`ecco`. L'onglet *Nodes* sous le graphe donne la valeur de chaque variable, et donc l'état correspondant.
