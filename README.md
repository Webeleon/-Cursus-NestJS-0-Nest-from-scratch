# 0 - Nest JS from scratch

// TODO video embed

## Installation des dépendances

Pour l'occasion, créons un dossier vide:
```bash
mkdir 0-nest-from-scratch
cd 0-nest-from-scratch
```

Dans un premier temps, il faut initialiser npm.
```bash
npm init
```
Installation des dépendances de développement:
```bash
npm i -D @typescript@4.3.5 @types/node
```

Installation des dépendances:
```bash
npm i @nestjs/core @nestjs/common @nestjs/platform-express reflect-metadata
```

## Configuration de Typescript

La première chose à faire dans un projet typescript est de configurer typescript via le fichier `tsconfig.json`

```json
{
  "include": ["src/**/*"], 
  "compilerOptions": {
    "module": "CommonJS",
    "target": "ES2017",
    "outDir": "dist",
    "experimentalDecorators": true
  }
}
```

## Création d'un module

Une application NestJS, ça commence par un module.
Donc on va créer le fichier `src/app.module.ts`.

Un module c'est une classe exportée sur laquelle on applique le décorateur `@Module` qui nous vient de `@nestjs/common`.

```ts
import { Module } from '@nestjs/common';

@Module({})
export class AppModule {}
```

## Création d'un controlleur

C'est bien beau d'avoir un module mais faut-il encore en faire quelque chose.
Et pour cela nous allons créer un controlleur.
Un controlleur c'est une classe exportée sur laquelle on applique le décorateur `@Controller` importé de `@nestjs/common`.

```ts
import { Controller } from '@nestjs/common';

@Controller()
export class AppController {}
```

Pour le moment, notre controlleur n'est pas très utile...
Nous allons donc lui ajouter une méthode `sayHello` qui retournera la string `Hello Nest`.

```ts
import { Controller } from '@nestjs/common';

@Controller()
export class AppController {
  sayHello(): string {
    return 'Hello Nest';
  }
}
```

Une méthode, c'est bien. Une route, c'est mieux!
Pour transformer la méthode `sayHello` en routeur http, il suffit de lui appliquer le décorateur `@Get()`

```ts
import { Controller, Get } from '@nestjs/common';

@Controller()
export class AppController {
  @Get()
  sayHello(): string {
    return 'Hello Nest';
  }
}
```

Pour en finir avec notre super controlleur, ajoutons-le tout simplement dans le module que nous avons créé précédemment.
Ajoutons la classe `AppController` dans la section `controllers` des options de notre module.

```ts
import { Module } from '@nestjs/common';
import { AppController } from './app.controller';

@Module({
  controllers: [AppController]
})
export class AppModule {}
```

## Un fichier de démarrage: `main.ts`

Top!
Maintenant que nous avons un module et un controlleur, il va nous falloir démarrer notre application.

Pour réaliser ce miracle, nous allons créer un fichier `main.ts` qui va se charger de compiler le module et lancer le serveur.
On commence par créer une fonction asynchrone que l'on appellera bootstrap.
Et ensuite on l'execute.
```ts
async function bootstrap() {}
bootstrap();
```

À l'intérieur de la fonction bootstrap, créons une variable app qui va recevoir le résultat awaiter de NestFactory.create() avec notre AppModule en paramètre.
```ts
import { NestFactory } from '@nestjs/core';
import { AppModule } from './app.module';

async function bootstrap() {
  const app = await NestFactory.create(AppModule);
}
bootstrap();
```

Finalement, on await la fonction app.listen() sur le port 3000.
```ts
import { NestFactory } from '@nestjs/core';
import { AppModule } from './app.module';

async function bootstrap() {
  const app = await NestFactory.create(AppModule);
  await app.listen(3000)
}
bootstrap()
```

Il ne reste plus qu'à retourner dans le terminal pour transpiler et tester notre superbe API.

## Compiler, lancer et tester

De retour dans le terminal, on peut utiliser la commande `tsc` installée par typescript pour transpiler dans le dossier dist.
```bash
node_modules/.bin/tsc
```

Une fois la transpilation terminée, on peut lancer notre API via commande:
```bash
node dist/main.js
```

Et pour tester, un petit curl des familles sera du meilleur des goûts.
```bash
curl http://localhost:3000
```


![questions?](https://media.giphy.com/media/DUrdT2xEmJWbS/giphy.gif)

Je serai heureux de répondre à toutes vos questions en commentaires


:phone:[Discord Webeleon](https://discord.gg/h7HzYzD82p)

:gift:[Code sur github](https://github.com/Webeleon/-Cursus-NestJS-0-Nest-from-scratch)

<script type="text/javascript" src="https://cdnjs.buymeacoffee.com/1.0.0/button.prod.min.js" data-name="bmc-button" data-slug="webeleon" data-color="#FFDD00" data-emoji="" data-font="Cookie" data-text="Buy me a coffee" data-outline-color="#000000" data-font-color="#000000" data-coffee-color="#ffffff" ></script>
