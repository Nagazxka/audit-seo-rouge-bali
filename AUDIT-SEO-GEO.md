# Rouge Bali — audit SEO, entités locales et découvrabilité GEO

**Mesure : 22 octobre 2026 UTC.** Site cible : https://www.rougebali.com/en/. Audit indépendant, public, sans accès GSC, GA4, GBP propriétaire, logs serveur ni réservation testée. Destinataire : Evan (lecture technique). Référence de forme : [audit Mon Notaire Conseil](https://audit-seo-mon-notaire-conseil.vercel.app/) ; aucun chiffre ni constat de cet autre site n'est transféré ici.

## 0. Décision / lecture en une minute

**Verdict : GO sous réserve.** Le site publie des pages de villas/lofts et un parcours de réservation non testé, mais son acquisition hors marque est sous-développée dans l'échantillon : **Rouge absent de la page 1 dans 10 des 11 SERP non-marque testées** ; seule exception : #3 sur `ubud loft villa accommodation` en AU/EN. **Cinq prompts ChatGPT Search non-marque** ne le mentionnent ni ne le citent ; un prompt explicitement brandé l'identifie et cite son site. Il ne faut donc ni dire « invisible partout », ni attribuer causalement ces écarts à un seul facteur. Sources : exports Serper locaux et identifiants DataForSEO §6-7.

**Signal local majeur vérifié :** l'ancienne fiche **« Rouge - Villas Ubud », Jl. Bisma**, renvoie `isPermanentlyClosed=true`, **424 avis / 4,3**, CID `10164099552258927653` dans Serper Maps (requête ID/EN, 22/10). Elle pointe encore vers le domaine, alors que le site indique pour son *management* **Jalan Raya Sayan No. 12** et un autre téléphone. Cette fiche peut décrire un ancien établissement réellement fermé ; **ne pas la rouvrir, déplacer, fusionner ou revendiquer sans preuves opérationnelles**. Le lien partagé par Evan résout vers le nom historique « Rouge Bali - Lounge Bar, Villas & Spa » et KGID `/g/12vrw103g`, mais Google a bloqué l'affichage de son statut dans le navigateur : correspondance exacte KGID↔CID non prouvée. [Fiche transmise](https://share.google/lXsZ6snHfGzwNgm2r) ; [site/contact](https://www.rougebali.com/en/contact/).

**Trois décisions de cette itération** : (1) verrouiller la matrice des entités et lieux avant toute opération GBP/schema ; (2) restaurer une architecture d'exploration simple et le hub hébergement aujourd'hui non lié depuis la home ; (3) choisir un pilote contenu « villa privée / couple à Ubud » à partir d'une propriété réellement adaptée, puis mesurer à nouveau SERP/GEO. Pas de production massive FR/ID avant validation.

## 1. Protocole, périmètre et limites

- **Collecte publique :** BFS des liens HTML internes depuis `/en/` ; 13 réponses relevées dont alias sans/avec slash et `/` redirigé, **8 pages EN uniques trouvées par ce parcours**. Une page supplémentaire `/en/rouge-villas` a été trouvée en SERP puis vérifiée HTTP 200 hors BFS : le chiffre 8 n'est donc **pas** un total exhaustif de pages publiées.
- **Extraction contenu :** script local Pingouin `website2md.py`, via `/root/le-pingouin/.venv/bin/python` (l'interpréteur système manque `bs4`) ; pages Rouge/concurrents clés extraites en cache de travail, pas un crawl intégral. Comptes de mots du script = indicatifs et susceptibles d'inclure navigation.
- **SERP :** script Serper partagé, `num=10`, 12 requêtes intent-clusterisées : 5 FR/FR (dont 1 marque), 2 GB/EN, 2 AU/EN, 1 US/EN, 1 ID/EN, 1 ID/ID. **12 `cache=miss`, 12 crédits Serper**, résultats instantanés non historiques. Pas de volumes de recherche ni d'estimations de trafic.
- **Maps :** 4 requêtes supplémentaires Serper Maps ID/EN ; les réponses JSON portent chacune `credits: 3`, **12 crédits Maps** au total. Captures JSON en cache local (voir §10).
- **GEO réel :** 6 appels DataForSEO `ai_optimization/chat_gpt/llm_scraper/live/advanced`, 5 prompts sans marque et 1 prompt marque. Prix public affiché : **0,004 USD/résultat Live**, coût théorique des 6 : **0,024 USD** ; le mode de retour MCP `.ai` ne donne pas le coût facturé, à confirmer dans le compte. Un seul moteur, un seul passage par prompt ; réponse variable, non représentative de l'ensemble des assistants.
- **Core Web Vitals :** PageSpeed Insights mobile a renvoyé **HTTP 429 quota journalier** ; **aucun score, LCP, INP, CLS mesuré**. Les observations HTML/images ne sont pas des mesures CWV.
- **GSC/GBP admin/backlinks :** pas d'accès propriété démontré ; aucune conclusion sur indexation réelle, clics, couverture GSC, contrôle des fiches ou profil de domaines référents. L'absence d'un lien/une page dans l'échantillon n'est pas une preuve d'absence globale.

## 2. Identité : groupe ≠ établissement ≠ propriété

| Source ou objet | Ce qui est constaté | Lecture / décision |
|---|---|---|
| [Home](https://www.rougebali.com/en/) / [About](https://www.rougebali.com/en/about_us/) | Nom « rouge », « Rouge Villas & Cafe Gabriel », collection de lofts et villas, anciens lounge-bar/villas explicitement évoqués | Garder « Rouge Bali » comme marque chapeau éditoriale, sans inventer une seule adresse pour toutes les propriétés. |
| [Contact](https://www.rougebali.com/en/contact/) | « Rouge Management and Consulting », Jalan Raya Sayan No. 12, téléphone `(0361) 958 5822` ; « Cafe Gabriel », Jl. Raya Sayan, téléphone `+62 812-1593-7020` | Deux numéros/rôles explicitement distincts : ne pas propager le numéro management à la fiche restaurant. |
| Serper Maps, ancienne fiche Jl. Bisma | « Rouge - Villas Ubud », CID `10164099552258927653`, 4,3/5, 424 avis, `isPermanentlyClosed=true`, tél. `+62 361 9080795`, site `http://www.rougebali.com/` | Contradiction apparente pour un internaute cherchant la marque. Vérifier historique de lieu et gestion avant décision : fermeture possiblement légitime du site Bisma ; avis attachés à CETTE fiche, pas transférables à Sayan. |
| Serper Maps, Café Gabriel | CID `6802711984626744705`, Jl. Raya Sayan, 4,9/5, 90 avis, pas de drapeau fermé dans la réponse ; la [page contact](https://www.rougebali.com/en/contact/) intègre cette carte | Entité restauration séparée ; « pas de drapeau fermé » ne garantit pas des horaires en temps réel. |
| Serper Maps, nouveaux lofts | « Rouge - Loft Noon » 7 avis, « Loft Minado » 9 avis (Jl. Baung), « Loft Mango » 9 avis (Jl. Rurung Dauh) ; plusieurs CIDs et numéros | Probables propriétés/adresses distinctes. Inventaire exhaustif + justificatifs avant arbitrer doublons potentiels vs fiches légitimes par propriété. |
| Liens sociaux de la [home](https://www.rougebali.com/en/) | Instagram `https://www.instagram.com/rouge.restaurant.ubud/`, Facebook `https://www.facebook.com/RougeBali` | Instagram pointe textuellement vers une identité restaurant historique, non vers la collection d'hébergement ; confirmer le handle officiel actuel avant remplacement. |
| Citations tierces | [Hotels.com « EDEN Ubud »](https://fr.hotels.com/ho442243/rouge-villas-spa-ubud-indonesie/) affiche les anciens noms « Rouge Villas Spa » ; [Reserving](https://fr.reserving.com/hotels/asie/indonesie/bali/ubud/rouge-villas-spa) conserve « Rouge Bali - Lounge Bar, Villas & Spa » ; [Booking Villa Condensé](https://www.booking.com/hotel/id/rouge-bali-villa-condense-ubud.fr.html) individualise une villa | Cartographier chaque citation par adresse, hôtel/propriété et ancienneté ; ne pas réclamer une mise à jour uniforme si EDEN/ancien hôtel est une entité désormais différente. |

**Point contre-intuitif :** la fiche fermée à 424 avis ne doit pas être « réparée » par un clic automatique. Une fermeture historique correcte protège l'usager ; la correction est une **cartographie d'entité** (ancienne adresse, actuelle, propriétaire, établissement, propriétés) puis, seulement si erreurs prouvées, procédure Google adaptée avec le propriétaire. Ajouter au site une clarification datée et factuelle « ancien lounge bar / ancien site Bisma » si confirmée par le client, sans prétendre que les 424 avis évaluent les villas actuelles. Une redirection site web ne migre pas les avis Maps.

**Gate client obligatoire :** pour chaque entité, fournir raison/nom commercial validé, adresse physique réelle, téléphone, statut actuel, date de déménagement/fermeture éventuelle, CID/place ID et accès GBP, URL officielle, handle Instagram, rapport juridique/ opérationnel avec Rouge Bali. Distinguer management non éligible éventuellement comme point client, Café, chaque site d'hébergement et anciennes implantations. Ne pas publier de `LocalBusiness` détaillé avant validation.

## 3. Technique et on-page — observations 22/10

| Constat mesuré | Preuve URL / mesure | Impact et correction |
|---|---|---|
| `robots.txt` 404 ; `/sitemap.xml`, `/sitemap_index.xml`, `/en/sitemap.xml` 404 | https://www.rougebali.com/robots.txt ; https://www.rougebali.com/sitemap.xml | Mettre `robots.txt` minimal et un XML des URLs canoniques 200, lier `Sitemap:` ; soumettre en GSC **si propriété obtenue**. 404 robots n'est pas un blocage de crawl en soi. |
| 0 canonical, 0 hreflang, 0 JSON-LD dans les **8 pages EN uniques parcourues** | [home](https://www.rougebali.com/en/), [villas](https://www.rougebali.com/en/rouge-private-villas/), [lofts](https://www.rougebali.com/en/rouge-lofts/), [contact](https://www.rougebali.com/en/contact/) et autres pages du crawl | Définir URL préférée et canonical auto-référent ; seulement `hreflang` si vraies versions traduites réciproques. JSON-LD `Organization` de marque puis `LodgingBusiness`/propriétés spécifiques sur données validées, `Restaurant` séparé. Schema aide la compréhension, ne garantit ni rang ni citation. |
| Alias sans slash ET avec slash rendent 200, pas de canonical | `/en/rouge-lofts` et `/en/rouge-lofts/` ; idem `/en/rouge-private-villas` | Fixer un format, 301 de l'autre ou canonical cohérent ; corriger les liens menu/cartes. Ne pas rediriger à l'aveugle sans vérifier dépendances réservation. |
| Home sans H1 ; contact/availability/about sans H1 ; lofts 2 H1, villas 4 H1, café 3 H1 | [home](https://www.rougebali.com/en/), [lofts](https://www.rougebali.com/en/rouge-lofts/), [villas](https://www.rougebali.com/en/rouge-private-villas/) | H1 unique et précis par page d'intention ; catégories/produits en H2/H3. Plusieurs H1 n'est pas une pénalité automatique : priorité à la clarté de la hiérarchie. |
| Titre home « Rouge Villas & Cafe Gabriel » ; méta description présente ; `html lang=en` | https://www.rougebali.com/en/ | Réécrire pour situer « Ubud » et les séjours villas/lofts sans masquer Café Gabriel ; les pages catégorie ont déjà des titres descriptifs : ne pas appliquer « pas de métas partout ». |
| Hub `/en/rouge-villas` = 200, titre « Accommodation in Ubud \| Private Villas & Lofts » et **#3** sur SERP AU/EN loft ; non lié depuis home selon les liens HTML crawlés | https://www.rougebali.com/en/rouge-villas ; https://www.rougebali.com/en/ | Opportunité de maillage immédiate : accueil/menu → hub hébergements → pages lofts/villas → sous-types ; pas de suppression/redirection d'un hub qui apparaît déjà en SERP. Vérifier accès via autres sources avant de le qualifier « orphelin absolu ». |
| `/en/rouge-lofts/` : 629 balises `<img>`, 153 627 octets HTML ; 616 images avec alt vide ; 627 images `loading=lazy` ; 49 scripts HTML | https://www.rougebali.com/en/rouge-lofts/ | Auditer galerie / doublons / DOM et ressources réseau, réduire thumbnails et carrousels cachés, garder galerie consultable ; alt descriptifs uniquement pour images informatives, alt vide légitime si décoratif. **Aucun LCP/INP démontré**. |
| `/fr/` et `/id/` renvoient 404 ; `/en/` est la seule langue découverte en navigation | https://www.rougebali.com/fr/ ; https://www.rougebali.com/id/ | Ce n'est pas un incident si la marque n'annonce pas ces langues ; mais l'absence de pages FR empêche de proposer une vraie réponse locale FR avec page d'atterrissage correspondante. Tester pilote FR plutôt que traduction mécanique du site. |
| Dans le HTML home, carte Villa Passion / Condensé / Jae renvoie vers la **catégorie**, pas une fiche détaillée par propriété | https://www.rougebali.com/en/ | Créer/relier des URL produit uniquement si inventaire stable : capacité, piscine exclusive ou partagée, emplacement réel, équipements, photos, prix/conditions/CTA. Profondeur de clic vérifiable ensuite. |

**Hors mesure :** HTTPS répond ; ni vitesse mobile, ni profondeur exhaustives, ni statut indexé GSC, ni validation Rich Results ne sont établis ici. L'accueil est SSR lisible dans le HTML brut, donc « tout le site inaccessible sans JS » serait faux.

## 4. SERP : qui prend la place et sur quelle intention

Échantillon (toutes 22/10/2026, `num=10`, 1 requête par cluster) :

| Marché / requête | Rouge dans top 10 | Sites observés haut placés et type |
|---|---|---|
| FR/FR `villa privée piscine ubud couple` | non | #1 Booking (OTA), #2 Villa-Bali (marketplace), #3 Airbnb (OTA) |
| FR/FR `villa lune de miel ubud` | non | #1 Villa-Bali (collection filtrée lune de miel), #2 Villa-Finder, #3 Airbnb |
| FR/FR `où dormir ubud en couple villa` | non | #1 Lilifoodiestravel (guide), #2 Booking, #3 Au goût d'Emma (guide) |
| FR/FR `villa ubud piscine privée` | non | #1 Booking, #2 Airbnb, #3 Agoda |
| GB/EN `ubud private pool villa couples` | non | #1 Airbnb, #2 Anantara (propriété), #3 Reddit (discussion) |
| GB/EN `honeymoon villas ubud` | non | #1 Booking, #2 Elite Havens, #3 Honeymoon Guesthouse |
| AU/EN `romantic villas ubud private pool` | non | #1 Luxury Escapes, #2 Facebook, #3 Pramana Experience |
| US/EN `boutique villa ubud private pool` | non | #1 Agoda, #2 Banyan Tree, #3 Tripadvisor ; Viceroy #4 |
| AU/EN `ubud loft villa accommodation` | **oui, #3** `/en/rouge-villas` | #1 Booking, #2 Expedia, #3 Rouge Bali |
| ID/EN `villa private pool ubud honeymoon` | non | #1 Villa-Finder, #2 Traveloka, #3 Booking ; Asvara #4 |
| ID/ID `villa romantis ubud private pool` | non | #1-2 Traveloka, #3 Booking, #4 Inivie |
| FR/FR `rouge bali villas ubud` **marque** | **oui, #2** `/en/rouge-villas` | #1 Booking Villa Condensé, #2 site officiel, #3 Agoda |

**Lecture :** les plateformes agrègent inventaire/avis et ciblent la comparaison transactionnelle ; les guides captent l'amont « où dormir » ; les établissements directs visibles font coïncider intitulé de page et besoin précis. Ils ne sont pas tous des concurrents business comparables. Rouge apparaît #3 sur l'unique requête loft testée en AU/EN, et #2 sur la requête de marque FR/FR ; pas de conclusion sur toutes les recherches ni causalité attribuable sans backlinks/GSC. Géographies sélectionnées car requêtes FR et EN alignées avec communication du site, plus test local ID ; **aucun volume pays prouvé**, donc ne pas appeler FR/GB/AU « marchés principaux en CA ».

## 5. Concurrents directs et comparaison d'arbo réelle

Les fichiers XML peuvent contenir médias et URL hors business ; chiffres ci-dessous = URLs `loc` uniques **récupérées** puis candidats HTML après exclusion conservatrice de répertoires de médias. Ce sont des **inventaires de sitemap**, ni pages indexées ni pages performantes.

| Domaine / catégorie | Inventaire sitemap observé | Couverture d'intention vérifiée | Écart exploitable pour Rouge |
|---|---|---|---|
| **Rouge Bali** / site direct | Aucun XML valide trouvé sur chemins standards. 8 pages EN uniques liées depuis home + hub hébergement 200 trouvé via SERP | Catégories génériques lofts/villas, offre, réservation ; pas de page couple/lune de miel trouvée dans ce périmètre | Relier hub existant et créer un seul parcours couple adapté, avant extension. |
| [Viceroy Bali](https://www.viceroybali.com/sitemap_index.xml) / resort direct premium | 1 260 `loc` récupérées ; ≈247 candidats HTML, dont ≈1 013 médias WP écartés ; 36 URLs candidat HTML contenant `honeymoon` (comptage de chaîne, non validation indexation) | [activités lune de miel](https://www.viceroybali.com/en/blog/ubud-honeymoon-activities/), [villas](https://www.viceroybali.com/en/bali-villa/), [package lune de miel](https://www.viceroybali.com/en/packages/ubud-honeymoon/) citée dans ChatGPT | Relie besoins → chambre/villa → package/preuves. Ne pas copier promesses luxe ou avantages absents chez Rouge. |
| [Ini Vie / Asvara](https://inivie.com/sitemap-0.xml) / portefeuille de villas | 632 `loc` uniques récupérées, ≈632 candidats HTML ; dossiers `discover-bali` 107 et `blog` 100, multiples sous-sites propriétés | [Asvara](https://inivie.com/asvaravilla) title « Luxury Honeymoon Vibe in Ubud », H1 romance, sections honeymoon, types de chambres avec piscine/jacuzzi, spa/offres | Entité produit et intention de couple explicites ; Rouge doit rendre extractibles les faits authentiques par propriété. |
| [Pramana Experience](https://pramanaexperience.com/sitemap_index.xml) / groupe | 1 619 `loc` uniques récupérées ; ≈122 candidats HTML après exclusion de 1 496 chemins médias ; `villa/` 51, `hotel-resort/` 18 | [collection villas Bali](https://pramanaexperience.com/villas-in-bali/) et pages de villas individuelles | Inventaire modulaire ; comparer produits pertinents plutôt que volume total. |
| [Bisma Eight](https://bisma-eight.com/sitemap.xml) / hôtel-villas | 1 703 `loc` uniques récupérées avant limite de 20 000, ≈304 candidats HTML après exclusion de 1 399 chemins `content/v1/` ; `whats-on/` 167, `news/` 110 | [offre honeymoon](https://bisma-eight.com/news/the-honeymoon-by-bisma-eight-hotel-villas), [villas](https://bisma-eight.com/villas) | Relie offres expérientielles et hébergement ; garder fraîcheur des offres datées. |
| [Villa-Bali.com](https://www.villa-bali.com/fr/search/honeymoon-villas-ubud) / marketplace | robots.txt annonce 9 familles linguistiques × villas/locations/main ; **sitemap XML renvoie 403 Cloudflare** dans cette collecte, total non vérifiable | Page filtre FR « honeymoon villas Ubud » #1 ; y figurent aussi des produits « The Loft Indigo / Emylia », relation à Rouge à confirmer | Plateforme = canal de distribution et adversaire SERP, pas site homologue ; investiguer fiches qui distribuent déjà Rouge et liens de retour. |

**Interprétation GEO :** Viceroy/Asvara/Sanctuary/Kayumanis ont été sélectionnés dans cet échantillon ; leurs pages officielles associent explicitement type de villa, piscine privative, contexte romantique, prestation et URL stable. Les citations observées proviennent effectivement de pages officielles ET de tiers (Tripadvisor, OTA) ; cela ne prouve pas que cette structure cause la citation. [Asvara](https://inivie.com/asvaravilla), [Viceroy](https://www.viceroybali.com/en/packages/ubud-honeymoon/), [Sanctuary](https://www.sanctuaryvillas.co/honeymoon-villa-ubud), [Kayumanis](https://www.kayumanisubud.com/offer/honeymoon-hideaway-package).

### Maillage cible minimal (sans cannibaliser)

```text
/en/ — home (accommodation Ubud, identité claire)
  → /en/rouge-villas/ — hub hébergements déjà en SERP
      → /en/rouge-lofts/ — catégorie, données par loft / liens fiches si créées
      → /en/rouge-private-villas/ — catégorie, données par villa / liens fiches si créées
  → /en/cafe-gabriel/ — entité restaurant distincte
  → /en/availability/ — réservation
Pilotage : /en/romantic-stays-ubud/ OU section forte du hub, seulement après validation produit
  → villa 1 chambre réellement adaptée → réservation → réponses pratiques.
```

URL cible proposée = **hypothèse d'arbo**, non page existante. Chaque guide d'amont (« choisir Ubud pour 5 nuits », « hôtel vs loft vs villa », « piscine privée ») doit renvoyer contextuellement au hub/propriété pertinente, pas seulement à la home. Ne pas produire 30 pages localisées interchangeables.

## 6. Panel GEO — 6 tests effectifs, pas une prédiction

**Moteur :** DataForSEO ChatGPT LLM Scraper Live, réponse ChatGPT Search. Codes locaux employés FR `2250`, GB `2826`, AU `2036`, ID `2360`. Les réponses sont des observations de ce moteur à ce moment, pas une note universelle de « GEO » ; aucune vérification de la véracité de toutes les affirmations de l'IA n'est impliquée.

| Prompt exact / marché | ID de tâche | Rouge mentionné / URL Rouge citée | Marques et URLs observées dans la réponse |
|---|---|---|---|
| EN/GB « Suggest a romantic private pool villa for a honeymoon in Ubud Bali and cite your sources. » | `10222230-2227-0629-0000-1093544f3a1e` | non / non | Kayumanis `kayumanisubud.com/villas`, Viceroy `viceroybali.com/en/packages/ubud-honeymoon/`, Sanctuary `sanctuaryvillas.co/honeymoon-villa-ubud` |
| FR/FR « Quelles villas avec piscine privée recommandes-tu pour une lune de miel à Ubud à Bali ? Cite tes sources. » | `10222230-2227-0629-0000-1a357cdcc857` | non / non | Kayumanis, Casa Pohon, Viceroy, Asvara, Sanctuary, Aria ; sources officielles + Tripadvisor |
| EN/AU « Where should a couple stay in Ubud Bali for a romantic trip in a villa with a private pool? Cite sources. » | `10222230-2227-0629-0000-3bdf08505e14` | non / non | Sanctuary, Kayumanis, Villa Semana, Bidadari, Asvara ; sources directes + Tripadvisor |
| EN/GB « Recommend a stylish loft or villa for a couple near Ubud Bali, ideally with a pool. Cite sources. » | `10222231-2227-0629-0000-4ec03e0379b7` | non / non | Four Elements Villas `fourelementsvillas.com/`, Casa Veranda, Origin Ubud, Clan Living, Aria |
| FR/FR « Pour un couple français qui prépare 5 nuits à Ubud, quelles villas privées recommandes-tu et pourquoi ? Cite les sources. » | `10222231-2227-0629-0000-0232e7ea6241` | non / non | Sanctuary, Aria, Kayumanis, Villa Lateng, K-Club ; sources directes |
| EN/ID **marque** « What is Rouge Bali in Ubud, are the Rouge private villas and lofts open, and where can I book them? Cite sources. » | `10222231-2227-0629-0000-d631890fe461` | **oui / oui** | Rouge décrit comme marque villas/lofts/Café, cite [About](https://www.rougebali.com/en/about_us/), [villas](https://www.rougebali.com/en/rouge-private-villas/), [disponibilité](https://www.rougebali.com/en/availability/) |

**Le point commercial :** l'IA peut retrouver Rouge quand elle reçoit son nom, mais ne l'a pas proposé spontanément dans ces cinq parcours testés. L'explication **plausible, non démontrée** : faible correspondance explicite des pages pour les scénarios couple/honeymoon, peu de pages d'entité-propriété, signaux tiers fragmentés et ancienne fiche locale fermée. On ne peut pas isoler la contribution de chaque facteur avec ces tests. Attention : le prompt de marque a aussi généré un récit/horaire/coordonnées ; toute affirmation de l'IA doit être vérifiée contre le site et le client avant usage public.

### Panel de suivi à geler avant expansion (prompts proposés, **non testés**)

- **Prépa vacances en couple (FR/EN)** : « Quel quartier d'Ubud choisir pour 5 nuits à deux si nous voulons visiter à pied et profiter d'une piscine ? » ; « Compare a Ubud loft and a private pool villa for a couple staying five nights. »
- **Lune de miel (FR/EN)** : « Quelles villas intimistes près d'Ubud conviennent à une lune de miel avec piscine réellement privative, et quels services sont inclus ? » ; « Which honeymoon villas near Ubud offer private pool, dinner and flexible booking? Cite official pages. »
- **Preuve / décision (FR/EN)** : « Quelles adresses vérifiées ont une villa 1 chambre à Ubud, quelles sont les adresses exactes et les conditions d'annulation ? » ; « Is Rouge Bali still open, and is the closed Rouge Villas Ubud listing the same property as its current villas? Cite evidence. » La dernière est un **test de désambiguïsation**, pas un prompt promotionnel.
- **Indonésie / proximité (ID/EN)** : « Villa privat untuk pasangan di Ubud dengan kolam renang pribadi dan dekat restoran » ; « Ubud couple stay with private pool near Sayan ». Avant suivi mensuel, fixer moteur, pays/langue, libellé, date et preuve de sortie. Distinguer `mention`, `recommandation`, `citation URL`, `lien direct officiel`.

## 7. Off-site et sources de citation : ce qui est prouvé / non prouvé

**Prouvé dans la collecte :** anciennes dénominations rémanentes chez certains distributeurs ; nouveaux lofts avec fiches Maps séparées ; résultats de marque dominés en FR par une propriété Booking (#1) puis le site (#2) ; pages éditoriales/OTA dominent les requêtes non-marque ; le site lie le compte social restaurant. L'ancienne fiche à 424 avis n'est pas une preuve que « Rouge Bali actuel possède 424 avis ».

**Non mesuré :** nombre/qualité de backlinks et domaines référents, profil de citations exhaustif, partage OTA de chiffre d'affaires, contrôle des comptes sociaux, granularité des avis, visibilité Google Business réelle par géogrid. Aucune conclusion de type « manque de backlinks » ou « reviews perdues » sans accès/données.

**Actions off-site licites :** inventorier Booking/Agoda/Tripadvisor/Hotels.com/Reserving/Facebook/Instagram avec identifiant et adresse de chaque propriété ; corriger uniquement les informations factuellement fausses auprès de l'administrateur du compte ; préserver les anciens lieux fermés lorsqu'ils l'ont réellement été ; sourcer les preuves clients/photographies autorisées ; obtenir des mentions éditoriales pertinentes via partenariats réels, sans faux avis ni promesses de citation IA. Ne pas mélanger fiche café, ancien bar et villas récentes dans un seul `sameAs`.

## 8. Roadmap priorisée — trois chantiers par vague

### Vague A — P0/P1, 0–14 jours (accès client requis pour les entités/GBP ; validation technique distincte pour le site)

1. **Entités / GBP (P0, owner client + Ruel)** : tableau d'autorité et captures des fiches ; confronter vieille Jl. Bisma vs Sayan vs propriétés ; décider « historique légitimement fermé » ou « erreur », puis uniquement procédure officielle adéquate. KPI : identité, adresse et téléphone cohérents par lieu ; aucune promesse de récupération des 424 avis.
2. **Découverte et canonical (P1, owner développeur)** : `/robots.txt` 200, XML des URL choisies, canonical et 301 slash cohérents, home → `/en/rouge-villas/` → deux catégories. QA HTTP + HTML avant/après, GSC si accès. Ne pas supprimer le hub classé #3 sur AU loft.
3. **Template / clarté (P1, owner développeur + contenu)** : H1 unique et descriptif home/hub/villas/lofts ; corriger titres génériques et orthographe EN des blocs pertinents ; profiler le rendu galerie lofts 629 img avant réduction, confirmer préservation des images et booking. KPI : DOM/images réellement chargées et test Lighthouse mobile lab + CrUX si disponible, **pas** une promesse de score.

### Vague B — P1/P2, 2–6 semaines

1. **Pilote intention commerciale** : une page/section couples EN fondée sur une villa 1 chambre appropriée **confirmée par le client** : piscine exclusive ou non, emplacement, équipements, photos originales, inclusions/conditions/réservation, comparaison juste avec loft. Lien depuis hub et catégorie ; pas de forfait honeymoon inventé.
2. **Version FR conditionnelle** : seulement la page money EN validée et son parcours de réservation si clientèle FR et maintenance confirmées ; traduction native avec URL FR, canonical propre et `hreflang` réciproque EN/FR ; pas de `/id/` sur simple hypothèse de marché.
3. **Distribution/citations** : prioriser pages tierces qui mélangent ancien et nouveau Rouge et fiches des propriétés actives ; obtenir cohérence nom/adresse/téléphone/URL, puis `Organization` + schémas adaptés selon vérité validée. Pas de balisage FAQ destiné à forcer des rich results commerciaux.

### Vague C — mesure et arbitrage, 6–12 semaines

1. GSC : impressions/clics par URL et requêtes `villa`, `loft`, `couple`, pays/langues ; distinguer indexation réelle du XML.
2. Refaire **les mêmes 11 SERP non-marque + 5 prompts GEO** à paramètres figés ; consigner mentions, citations et domaines tiers ; comparer tendance, pas « position GEO » fictive.
3. Selon données de réservation et demandes réelles, étendre au maximum trois angles parmi couple, long séjour, architecture/design, gastronomie + séjour ; abandonner ceux sans preuve d'adéquation ou de demande.

## 9. QA/CoVe Salomon — portes de sortie

- **Plan : GO sous réserve**, exiger preuves de marché et distinguer sitemap/indexation ; ne jamais traiter 424 avis comme avis du site actuel.
- **SERP/GEO : GO avec réserves**, photographie de 11 requêtes non-marque et 5 prompts non-marque ; exception loft AU ; comparaison d'URLs HTML, pas des totaux médias. No-go pour « invisible sur Google/ChatGPT » ou causalité directe.
- **Technique/entité : GO partiel**, état public publiable ; no-go pour toute modification GBP, fusion d'entités, attribution/transfert d'avis ou score CWV. Statut exact KGID↔CID à valider.
- **Mon arbitrage final Ruel :** traiter l'identité opérationnelle avant `sameAs`/GBP, mais ne pas bloquer le quick win maillage + canonical si l'équipe peut intervenir indépendamment. Aucun changement sur le site ou les fiches n'a été opéré par cet audit.

## 10. Sources, traçabilité, reprise

- **Site source :** [home](https://www.rougebali.com/en/), [about](https://www.rougebali.com/en/about_us/), [contact](https://www.rougebali.com/en/contact/), [hub](https://www.rougebali.com/en/rouge-villas), [villas](https://www.rougebali.com/en/rouge-private-villas/), [lofts](https://www.rougebali.com/en/rouge-lofts/), [café](https://www.rougebali.com/en/cafe-gabriel/), [réservation](https://www.rougebali.com/en/availability/), [fiche partagée](https://share.google/lXsZ6snHfGzwNgm2r).
- **Concurrents :** [Viceroy XML](https://www.viceroybali.com/sitemap_index.xml), [Inivie XML](https://inivie.com/sitemap-0.xml), [Pramana XML](https://pramanaexperience.com/sitemap_index.xml), [Bisma XML](https://bisma-eight.com/sitemap.xml), [Villa-Bali robots](https://www.villa-bali.com/robots.txt) et [listing honeymoon FR](https://www.villa-bali.com/fr/search/honeymoon-villas-ubud). Les pages précises figurent §5-6.
- **Données de travail locales temporaires** (non versionnées, susceptibles d'expirer) : `/root/.hermes/profiles/seo/cache/scratch/rougebali-serper/outputs/*.json` (12 SERP avec `checked_at`, `cache_status`, positions), `rougebali-serper/runlog.json`, `rougebali-tech.json`, `rougebali-sitemaps.json`, `rougebali-map-serper.json`, `rougebali-map-entities.json`, `rougebali-pages/*.md`. **Les réponses GEO brutes ont été retournées par MCP mais non archivées en fichier ; IDs et extrait de leurs citations sont documentés §6.** Pour une présentation client réplicable, exporter les réponses complètes lors du prochain run, sans inventer aujourd'hui une archive absente.
- **API/coût :** Serper 12 SERP × 1 crédit observé + 4 Maps × 3 crédits indiqués par les réponses JSON = **24 crédits Serper** ; DataForSEO 6 réponses `status_code=20000`, coût théorique catalogue 0,024 USD, facturation exacte non lue ; PSI 1 appel HTTP 429 et aucun résultat.

**Blocage principal :** confirmation par propriétaire de la carte des entités et accès GBP/GSC. **Prochain livrable utile :** matrice entités validée par le client + tickets techniques ciblés, pas un volume de nouvelles pages spéculatives.
