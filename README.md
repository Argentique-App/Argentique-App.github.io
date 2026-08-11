# Argentique : le site

Site public d'[Argentique](https://github.com/Argentique-App), servi par GitHub
Pages. Il fait deux choses : présenter l'application, et **héberger les quatre
documents légaux** dont Google Play exige l'URL publique.

Aucun script, aucune police distante, aucune ressource externe. Ce n'est pas une
préférence de style : une page qui vend l'absence de réseau et qui chargerait un
traceur au passage se contredirait à voix haute.

---

## L'adresse

```
https://argentique-app.github.io
```

Le dépôt s'appelle `Argentique-App.github.io`, ce qui fait de lui le **site
d'organisation** : GitHub Pages le sert à la racine du sous-domaine, sans segment
de chemin. C'était le but du renommage, et ce n'était pas cosmétique — la même
adresse est destinée au pied des affiches de Rétrospective partagées depuis
l'application, chaîne qui part avec chaque version publiée et que les images déjà
diffusées porteront pendant des années.

Elle est déjà renseignée dans `LEGAL_BASE_URL` du dépôt applicatif.

## Activer Pages

`Settings` → `Pages` → `Deploy from a branch` → `main` / `/ (root)`.

Le fichier `.nojekyll` à la racine est nécessaire : sans lui, Jekyll ignore les
dossiers commençant par un souligné et réécrit certaines pages.

---

## Ce qu'il reste à combler avant de publier

L'identité de l'éditeur est renseignée partout. **Un seul marqueur subsiste**, et
il est délibéré :

| Où | Quoi | Quand |
|---|---|---|
| `legal/cgv.html`, art. 10 | Le médiateur de la consommation | **Avant la première vente**, pas avant |

L'article L612-1 du code de la consommation impose au professionnel **qui vend à
des consommateurs** d'adhérer à un dispositif de médiation et d'en publier les
coordonnées. L'obligation naît donc de la vente, pas de la publication d'un site
ni d'un test fermé : tant que les produits ne sont pas ouverts à l'achat, aucun
contrat de consommation n'est conclu.

Plutôt que de laisser un trou, l'article 10 des CGV **dit cet état** : aucun
contenu payant n'est proposé à la vente, et le médiateur sera désigné avant la
mise en vente effective. C'est exact aujourd'hui et ça cesse de l'être le jour où
Play Billing encaisse le premier euro.

> **Le jour où tu ouvres les ventes, cette ligne devient bloquante.** L'adhésion
> est payante (de l'ordre de 50 € par activité) et prend quelques jours. À lancer
> en même temps que la création des produits en Console, pas après.

Les marqueurs restants sont **volontairement criards** — surlignés en jaune,
classe CSS `.todo`. Une page légale mise en ligne avec un trou invisible dedans
est pire que pas de page du tout.

---

## Brancher l'application dessus

Une fois l'adresse connue, renseigner `LEGAL_BASE_URL` dans `src/legal.ts` du
dépôt de l'application :

```ts
export const LEGAL_BASE_URL = 'https://argentique-app.github.io/legal';
```

`LEGAL_URLS_CONFIGURED` repasse alors à `true` de lui-même. Vérifier ensuite que
les quatre URL répondent :

```
…/legal/confidentialite.html
…/legal/cgu.html
…/legal/cgv.html
…/legal/mentions-legales.html
```

---

## `legal/` est une copie

Les quatre documents et leur feuille de style sont **écrits dans le dépôt de
l'application**, sous `legal/`. Ce qui est ici en est une copie : c'est le seul
moyen d'obtenir une URL publique qui ne contienne ni « gram » ni « insta », le
dépôt applicatif portant encore son ancien nom.

Deux copies divergent toujours. Après toute modification des documents côté
application, resynchroniser :

```bash
cp ~/dev/gramvault/legal/*.html ~/dev/gramvault/legal/style.css \
   ~/dev/argentique-site/legal/
```

La source fait foi. Ne corrige jamais un document ici sans le corriger là-bas.

---

## Structure

```
.nojekyll               nécessaire à GitHub Pages
index.html              page d'accueil (FR)
en/index.html           page d'accueil (EN)
accueil.css             styles de la page d'accueil
fonts/                  Instrument Serif, auto-hébergée (SIL OFL 1.1)
img/                    icône, captures, carte sociale
legal/                  copie des quatre documents + leur index
```

Les captures d'`img/` sont prises sur une **archive de démonstration** générée par
`scripts/make-demo-archive.js` : personnes, conversations et statistiques
inventées. Aucune donnée réelle, aucune personne réelle. Ne jamais les remplacer
par des captures d'un export véritable, le sien ou celui d'un testeur.

---

Argentique n'est ni affiliée à, ni sponsorisée par, ni approuvée par Meta
Platforms, Inc.
