### Erste Schritte

In diesen Artikeln lernen Sie die **wichtigsten Grundlagen** von Nest kennen. Um sich mit den wesentlichen Bausteinen von Nest-Anwendungen vertraut zu machen, erstellen wir eine grundlegende CRUD-Anwendung mit Funktionen, die auf Einführungsebene viel abdecken.

#### Sprache

Wir lieben [TypeScript](https://www.typescriptlang.org/) , aber vor allem lieben wir [Node.js](https://nodejs.org/en/) . Aus diesem Grund ist Nest sowohl mit TypeScript als auch mit **reinem JavaScript** kompatibel. Nest nutzt die neuesten Sprachfunktionen. Um es mit Vanille-JavaScript zu verwenden, benötigen wir einen [Babel-](https://babeljs.io/) Compiler.

In den von uns bereitgestellten Beispielen verwenden wir hauptsächlich TypeScript, aber Sie können **die Code-Snippets** jederzeit auf Vanilla-JavaScript-Syntax umstellen (klicken Sie einfach auf die Sprachschaltfläche in der oberen rechten Ecke jedes Snippets, um sie umzuschalten).

#### Voraussetzungen

Bitte stellen Sie sicher, dass [Node.js](https://nodejs.org/) (&gt;= 10.13.0) auf Ihrem Betriebssystem installiert ist.

#### Einrichten

Das Einrichten eines neuen Projekts ist mit der [Nest-CLI](/cli/overview) ganz einfach. [Wenn npm](https://www.npmjs.com/) installiert ist, können Sie mit den folgenden Befehlen in Ihrem Betriebssystem-Terminal ein neues Nest-Projekt erstellen:

```bash
$ npm i -g @nestjs/cli
$ nest new project-name
```

Das `project` wird erstellt, Knotenmodule und einige andere Boilerplate-Dateien werden installiert und ein `src/` wird erstellt und mit mehreren Kerndateien gefüllt.

<div class="file-tree">
  <div class="item">src</div>
  <div class="children">
    <div class="item">app.controller.ts</div>
    <div class="item">app.controller.spec.ts</div>
    <div class="item">app.module.ts</div>
    <div class="item">app.service.ts</div>
    <div class="item">main.ts</div>
  </div>
</div>

Hier ist eine kurze Übersicht über diese Kerndateien:

|                          |                                                                                                                    |
|--------------------------|--------------------------------------------------------------------------------------------------------------------|
| `app.controller.ts`      | Ein einfacher Controller mit einer einzigen Route.                                                                 |
| `app.controller.spec.ts` | Die Unit-Tests für den Controller.                                                                                 |
| `app.module.ts`          | Das Stammmodul der Anwendung.                                                                                      |
| `app.service.ts`         | Ein Basisdienst mit einer einzigen Methode.                                                                        |
| `main.ts`                | Die Eintragsdatei der Anwendung, die die Kernfunktion `NestFactory` , um eine Nest-Anwendungsinstanz zu erstellen. |

Die `main.ts` enthält eine Asynchron - Funktion, die unsere Anwendung **Bootstrap** wird:

```typescript
@@filename(main)

import { NestFactory } from '@nestjs/core';
import { AppModule } from './app.module';

async function bootstrap() {
  const app = await NestFactory.create(AppModule);
  await app.listen(3000);
}
bootstrap();
@@switch
import { NestFactory } from '@nestjs/core';
import { AppModule } from './app.module';

async function bootstrap() {
  const app = await NestFactory.create(AppModule);
  await app.listen(3000);
}
bootstrap();
```

Um eine Nest-Anwendungsinstanz zu erstellen, verwenden wir die `NestFactory` . `NestFactory` stellt einige statische Methoden bereit, mit denen eine Anwendungsinstanz erstellt werden kann. Die `create()` liefert ein Anwendungsobjekt zurück, das die Schnittstelle `INestApplication` Dieses Objekt stellt eine Reihe von Methoden bereit, die in den kommenden Kapiteln beschrieben werden. Im `main.ts` Beispiel starten wir einfach unseren HTTP-Listener, der die Anwendung auf eingehende HTTP-Anfragen warten lässt.

Beachten Sie, dass ein mit der Nest-CLI erstelltes Projekt eine anfängliche Projektstruktur erstellt, die Entwickler dazu ermutigt, der Konvention zu folgen, jedes Modul in einem eigenen dedizierten Verzeichnis zu speichern.

<app-banner-courses></app-banner-courses>

#### Plattform

Nest zielt darauf ab, ein plattformunabhängiges Framework zu sein. Die Plattformunabhängigkeit macht es möglich, wiederverwendbare logische Teile zu erstellen, die Entwickler über verschiedene Anwendungstypen hinweg nutzen können. Technisch gesehen kann Nest mit jedem Node-HTTP-Framework arbeiten, sobald ein Adapter erstellt wurde. Es werden zwei HTTP-Plattformen [standardmäßig](https://www.fastify.io) [unterstützt: express](https://expressjs.com/) und fastify . Sie können diejenige auswählen, die Ihren Bedürfnissen am besten entspricht.

|                    |                                                                                                                                                                                                                                                                                                                                                                                       |
|--------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `platform-express` | [Express](https://expressjs.com/) ist ein bekanntes minimalistisches Web-Framework für Node. Es ist eine kampferprobte, produktionsbereite Bibliothek mit vielen Ressourcen, die von der Community implementiert wurden. Das `@nestjs/platform-express` wird standardmäßig verwendet. Viele Benutzer sind mit Express gut bedient und müssen nichts unternehmen, um es zu aktivieren. |
| `platform-fastify` | [Fastify](https://www.fastify.io/) ist ein leistungsstarkes Framework mit geringem Overhead, das sich stark auf maximale Effizienz und Geschwindigkeit konzentriert. [Lesen Sie hier,](/techniques/performance) wie Sie es verwenden.                                                                                                                                                 |

Welche Plattform auch immer verwendet wird, sie stellt ihre eigene Anwendungsschnittstelle bereit. Diese werden als `NestExpressApplication` bzw. `NestFastifyApplication` .

Wenn Sie wie im folgenden Beispiel einen Typ an die `NestFactory.create()` `app` Objekt über Methoden, die ausschließlich für diese spezielle Plattform verfügbar sind. Beachten Sie jedoch, dass Sie keinen Typ angeben **müssen** **, es sei denn,** Sie möchten tatsächlich auf die zugrunde liegende Plattform-API zugreifen.

```typescript
const app = await NestFactory.create<NestExpressApplication>(AppModule);
```

#### Ausführen der Anwendung

Sobald der Installationsvorgang abgeschlossen ist, können Sie den folgenden Befehl an der Eingabeaufforderung Ihres Betriebssystems ausführen, um die Anwendung zu starten, die auf eingehende HTTP-Anforderungen lauscht:

```bash
$ npm run start
```

Dieser Befehl startet die App mit dem HTTP-Server, der auf dem Port lauscht, der in der `src/main.ts` ist. Sobald die Anwendung ausgeführt wird, öffnen Sie Ihren Browser und navigieren Sie zu `http://localhost:3000/` . Sie sollten die `Hello World!` Botschaft.
