---
layout: default
title: "Configuration poste de travail - Angular"
permalink: /formation/angular/install/
lang: fr
my_menu: menu-angular.html
---

## Configuration du poste de travail

- Installer NodeJS (et donc NPM) pour vérifier l'installation `npm --version`.
- Installer Angular CLI via NPM : `npm install -g @angular/cli` pour vérifier l'installation `ng version`.

### Création d'un projet Angular

Pour créer un projet **nom-de-mon-application** taper la commande suivante : `ng new nom-de-mon-application --minimal --style=css`.

- `--minimal` : permet de générer un projet minimaliste, c'est-à-dire avec le strict minimum de fichiers et de fonctionnalités nécessaires pour démarrer une application.
- `--style=css` : indique que le style sera géré en CSS.

#### Arborescence du projet

- `nodes_modules` : dépendances NodeJS
- `src` : les sources du projet
- `src/app/app-routing.module.ts` : routes du projet
- `src/app/app.component.ts` : composant racine
- `src/app/app.module.ts` : module racine
- `src/assets` : images du projet, par exemple
- `environnements` : variabes d'environnements
- `angular.json` : configuration du projet
- `package.json` : dépendances du projet
- `tsconfig.app.json` : configuration du compilateur TypeScript pour le projet
- `tsconfig.json` : fichier de configuration du compilateur TypeScript principal
