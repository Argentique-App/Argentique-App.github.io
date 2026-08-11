# Argentique : le site

Site public d'[Argentique](https://github.com/Argentique-App), servi par GitHub
Pages. Il fait deux choses : présenter l'application, et **héberger les quatre
documents légaux** dont Google Play exige l'URL publique.

Aucun script, aucune police distante, aucune ressource externe. Ce n'est pas une
préférence de style : une page qui vend l'absence de réseau et qui chargerait un
traceur au passage se contredirait à voix haute.

---

## L'adresse, et pourquoi elle compte

Selon le nom du dépôt, GitHub Pages sert le site à deux endroits différents :

| Dépôt | Adresse |
|---|---|
| `Argentique` | `https://argentique-app.github.io/Argentique/` |
| **`Argentique-App.github.io`** ✅ | `https://argentique-app.github.io/` |

**Renommer le dépôt en `Argentique-App.github.io` est recommandé**, et le moment
de le faire est maintenant. Deux raisons :

1. **L'URL de la politique de confidentialité s'affiche publiquement sur la fiche
   Play.** Plus elle est courte, mieux c'est.
2. **Surtout** : l'adresse est destinée à figurer en pied des affiches de
   Rétrospective partagées depuis l'application. Cette chaîne part avec chaque
   version publiée, et les images déjà partagées la porteront pendant des années.
   Elle doit être choisie une fois.

Le renommage ne casse rien : GitHub redirige l'ancienne adresse.

## Activer Pages

`Settings` → `Pages` → `Deploy from a branch` → `main` / `/ (root)`.

Le fichier `.nojekyll` à la racine est nécessaire : sans lui, Jekyll ignore les
dossiers commençant par un souligné et réécrit certaines pages.

---

## Ce qu'il reste à combler avant de publier

Les trous sont **volontairement criards** — surlignés en jaune à l'écran, classe
CSS `.todo`. Une page légale mise en ligne avec un trou dedans est pire que pas de
page du tout.

| Où | Quoi |
|---|---|
| `index.html`, `en/index.html` | L'adresse e-mail de contact, dans le lien « Rejoindre le test fermé » (`CONTACT@EXEMPLE.TEST`) et dans la mention sous le bouton |
| `legal/*.html` | Dénomination, statut juridique, SIRET, adresse, e-mail, TVA, hébergeur, **médiateur de la consommation** |

> **Le médiateur de la consommation est obligatoire**, pas optionnel : tout
> professionnel vendant à des consommateurs en France doit adhérer à un dispositif
> de médiation et en publier les coordonnées (art. L612-1 c. conso). L'adhésion
> est payante et prend quelques jours : à lancer tôt.

Rien n'empêche de **pousser et d'activer Pages tout de suite** — la page d'accueil
est complète et son travail actuel est de recruter les douze testeurs du test
fermé. Ce sont les pages légales qui doivent être finies avant le **dépôt sur
Play**, pas avant la mise en ligne du site.

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
