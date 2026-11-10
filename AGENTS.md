# AGENTS.md — demo-angular

Application Angular (TypeScript strict, composants standalone, signaux). Tests : Karma + Jasmine.

## Commandes
- Dépendances : `npm ci` (ne modifie `package-lock.json` que si la tâche ajoute ou met à jour une dépendance).
- Tests : `npm test -- --watch=false --browsers=ChromeHeadless` (ou `ChromeHeadlessCI` si défini dans `karma.conf.js`). Ils doivent passer avant de conclure.
- Build : `npm run build`.
- Pas de serveur de développement pour vérifier : les tests suffisent.

## Architecture
- Composants **standalone** uniquement : pas de `NgModule`.
- Un dossier par fonctionnalité sous `src/app/<fonctionnalité>/` : `x.component.ts`, `x.component.html`, `x.component.spec.ts`.
- Routes dans `src/app/app.routes.ts` (chargement paresseux avec `loadComponent` pour les pages).
- Logique et état partagés dans des services `@Injectable({ providedIn: 'root' })`, récupérés avec `inject()`.

## Conventions
- État local avec les **signaux** (`signal`, `computed`) ; `ChangeDetectionStrategy.OnPush`.
- Syntaxe de template moderne : `@if`, `@for` (avec `track`), pas de `*ngIf` / `*ngFor`.
- Pas de `any` : types explicites ; `strict` reste activé.
- Pas de `console.log` ni de code mort.
- Accessibilité : libellés sur les champs, boutons réels (`<button>`), pas de `div` cliquable.
- Texte de l'interface en français.

## Tests
- Jasmine + `TestBed`. Un fichier `.spec.ts` à côté de chaque composant ou service.
- Teste le comportement visible (texte, boutons, états), pas les détails d'implémentation.
- Ajoute des tests NOUVEAUX ; ne modifie pas et ne désactive pas un test existant (`xit`, `fit`, `xdescribe`, `fdescribe` interdits).

## Dépendances
- N'ajoute une dépendance que si la tâche le demande, en version exacte (`--save-exact`) ; `package.json` et `package-lock.json` changent ensemble.
- Ne change pas la version d'Angular ni de TypeScript sans demande.

## Sécurité
- Aucun secret ni jeton dans le code, les tests ou `environment*.ts`.
- Laisse Angular assainir le HTML : évite `bypassSecurityTrust*`, `innerHTML` non assaini et `eval`, sauf si la tâche l'exige explicitement.
- Des contrôles automatiques (Semgrep, Trivy) tournent avant le commit : corrige la cause d'un constat ; n'ajoute ni commentaire `nosem` ni fichier d'exclusion.

## Périmètre
Fais seulement ce que demande la tâche, avec les changements les plus petits possibles. Ne touche pas à `AGENTS.md`, à `.gitignore`, à `angular.json` ni à la CI sauf demande.
