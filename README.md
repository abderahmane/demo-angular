# demo-angular

Application **Angular** de démonstration (composants standalone, signaux). Sert de projet d'essai pour le pipeline opencode.

## Prérequis
- Node.js 20 ou 22 LTS et npm
- Chrome ou Chromium pour les tests (Karma, ChromeHeadless)

## Commandes
| Action | Commande |
|---|---|
| Installer | `npm ci` |
| Lancer en développement | `npm start` (http://localhost:4200) |
| Tests unitaires | `npm test -- --watch=false --browsers=ChromeHeadless` |
| Build de production | `npm run build` |

## Structure
```
src/app/
  app.ts, app.config.ts, app.routes.ts   racine, configuration, routes
  <fonctionnalité>/                      un dossier par fonctionnalité
    <nom>.component.ts / .html / .css / .spec.ts
```

## Tests dans un conteneur
ChromeHeadless échoue en conteneur durci (« No usable sandbox »). Le dépôt définit donc un lanceur `ChromeHeadlessCI` (option `--no-sandbox`) dans `karma.conf.js` ; le pipeline l'utilise via `ANGULAR_TEST_BROWSER=ChromeHeadlessCI`.

## Contribuer
Les modifications passent par merge request ; les tests et le build doivent être verts. Conventions détaillées dans `AGENTS.md`.
