# Developpement Back End Node.js

## Revue des fondamentaux du javascript

### Variables 

#### Différents types de variables

***var*** :
- Portée : La portée des variables déclarées avec var est fonctionnelle. Cela signifie qu'elles sont visibles dans toute la fonction où elles sont déclarées, mais pas à l'extérieur de cette fonction.
- Hoisting : Les déclarations de variables avec var sont soumises à l'hoisting, ce qui signifie que la déclaration est déplacée vers le haut de la fonction ou du script lors de l'exécution.
- Mutabilité : On peut réassigner une valeur à une variable déclarée avec var.

***let*** :
- Portée : La portée des variables déclarées avec let est de bloc. Cela signifie qu'elles sont visibles uniquement à l'intérieur du bloc (par exemple, une paire de {}) où elles sont déclarées.
- Hoisting : Les déclarations de variables avec let sont également soumises à l'hoisting, mais la variable ne sera pas initialisée avant la déclaration.
- Mutabilité : On peut réassigner une valeur à une variable déclarée avec let.

**const** :

- Portée : La portée des variables déclarées avec const est également de bloc.
- Hoisting : Comme let, les déclarations de variables avec const sont soumises à l'hoisting, mais la variable ne sera pas initialisée avant la déclaration.
- Mutabilité : Les variables déclarées avec const ne peuvent pas être réassignées après leur initialisation. Cependant, cela ne signifie pas que la valeur est immuable, seulement que la référence à la valeur ne peut pas changer.
En résumé, let est souvent préféré à var en raison de sa portée de bloc plus prévisible, et const est utilisé lorsque vous avez l'intention de ne pas réassigner la variable après son initialisation. Il est recommandé d'utiliser const autant que possible pour rendre le code plus prévisible et sûr, en ne réassignant une variable que si c'est vraiment nécessaire.


### Types de fonctions 

#### Déclaration de fonction :

```
function nomDeLaFonction(parametre1, parametre2) {
  // Corps de la fonction
  // Code à exécuter
}
```

#### Expression de fonction anonyme :

```
var nomDeLaFonction = function(parametre1, parametre2) {
  // Corps de la fonction
  // Code à exécuter
};
```


#### Expression de fonction nommée :


```
var nomDeLaFonction = function nomDeLaFonction(parametre1, parametre2) {
  // Corps de la fonction
  // Code à exécuter
};
```

####  Fonction fléchée (arrow function) :


```
var nomDeLaFonction = (parametre1, parametre2) => {
  // Corps de la fonction
  // Code à exécuter
};
```

Les fonctions fléchées (arrow functions) en JavaScript présentent plusieurs différences par rapport aux autres types de fonctions, notamment en ce qui concerne la syntaxe, la gestion de la portée (this), et le comportement avec l'objet arguments. Voici les principales distinctions :

**this** :
Fonctions déclaratives et expressions de fonction anonyme : La valeur de this dépend de la manière dont la fonction est appelée. Elle est définie par le contexte d'appel et peut varier.
Fonctions fléchées : La valeur de this est héritée du contexte dans lequel la fonction fléchée est définie. Cela signifie que les fonctions fléchées n'ont pas leur propre this ; elles capturent le this de l'environnement parent lors de leur déclaration.


```
function FonctionNormale() {
  this.valeur = 1;

  // Fonction normale
  setTimeout(function() {
    this.valeur++;
    console.log(this.valeur); // "NaN" car "this" ne fait pas référence à l'objet externe
  }, 1000);
}

function FonctionFlechee() {
  this.valeur = 1;

  // Fonction fléchée
  setTimeout(() => {
    this.valeur++;
    console.log(this.valeur); // "2" car "this" fait référence à l'objet externe
  }, 1000);
}

var objetNormal = new FonctionNormale();
var objetFleche = new FonctionFlechee();

```

arguments :
Fonctions déclaratives et expressions de fonction anonyme : Ont leur propre objet arguments qui contient les arguments passés à la fonction.
Fonctions fléchées : N'ont pas leur propre objet arguments. Vous devez utiliser le reste des paramètres (...) pour récupérer les arguments.


```

function fonctionNormale() {
  console.log(arguments);
}

var fonctionFlechee = (...args) => {
  console.log(args);
};

fonctionNormale(1, 2, 3);      // { '0': 1, '1': 2, '2': 3 }
fonctionFlechee(1, 2, 3);     // [ 1, 2, 3 ]

```

En résumé, les fonctions fléchées sont souvent préférées pour des fonctions simples en raison de leur syntaxe concise et de leur comportement prévisible avec this. Cependant, elles ne conviennent pas à toutes les situations, en particulier lorsqu'une gestion complexe de this est nécessaire ou lorsqu'un objet arguments distinct est requis. Dans ces cas, les fonctions déclaratives ou les expressions de fonction anonyme peuvent être plus appropriées.


## Introduction à Node.js

###  Qu'est-ce que Node.js ?

Node.js est un environnement d'exécution côté serveur basé sur le moteur JavaScript V8 de Google.
Node.js permet l'exécution de JavaScript côté serveur, contrairement à son utilisation traditionnelle côté client dans les navigateurs web.

**Apache/PHP**: Dans un environnement Apache avec PHP, chaque demande crée un nouveau processus ou thread, ce qui peut entraîner un coût en termes de performances.

**Node.js** : Node.js utilise un modèle non bloquant, qui permet à une seule instance de gérer plusieurs connexions simultanées sans créer de nouveaux processus, améliorant ainsi l'efficacité.

### Le modèle événementiel de Node.js

### Principes fondamentaux

Asynchrone : Les opérations dans Node.js sont généralement effectuées de manière asynchrone, permettant à l'application de continuer à traiter d'autres tâches pendant l'attente de résultats.

### Callbacks

Les callbacks sont un concept essentiel en développement d'application backend, surtout dans des environnements asynchrones comme Node.js. Voici un résumé rapide des conseils techniques concernant les callbacks :

**Compréhension du concept** : Comprendre que les callbacks sont des fonctions passées en tant qu'arguments à d'autres fonctions, et qui seront exécutées ultérieurement, généralement après une opération asynchrone.

**Gestion des erreurs** : Toujours gérer les erreurs dans les callbacks en utilisant le premier argument de la fonction de rappel conventionnellement dédié aux erreurs (err).

**Éviter le callback hell** : Éviter la pyramide des callbacks (aussi appelée "callback hell") en utilisant des techniques telles que les fonctions nommées, les promesses ou les fonctions de rappel asynchrones (async/await) pour rendre le code plus lisible et maintenable.

**Modularité** : Utiliser des fonctions de rappel modulaires et réutilisables pour améliorer la lisibilité et la maintenabilité du code.

**Gestion des dépendances** : Faire attention à la gestion des dépendances et à la portée des variables dans les callbacks, en particulier lorsqu'ils sont imbriqués.

**Documentation** : Commenter clairement le code pour expliquer le rôle de chaque callback, son format d'entrée et de sortie, ainsi que les éventuelles erreurs qu'il peut générer.

**Tests unitaires** : Écrire des tests unitaires pour les fonctions de rappel afin de s'assurer de leur bon fonctionnement et de leur robustesse.

### L'Event Loop

Boucle d'événements : Détailler le rôle de l'Event Loop dans le traitement des événements.

Non-blocant : Expliquer comment l'Event Loop permet à Node.js de rester non bloquant en gérant les tâches de manière efficace.

### Introduction à l'EventEmitter

L'EventEmitter est un élément fondamental du fonctionnement de Node.js, car de nombreuses fonctionnalités de Node.js reposent sur ce module pour gérer les interactions asynchrones. Voici quelques-unes des principales façons dont l'EventEmitter est utilisé de base dans le fonctionnement de Node.js :

**Gestion des requêtes HTTP** : Lorsqu'un serveur Node.js reçoit une requête HTTP, il émet un événement 'request'. Les développeurs attachent ensuite des écouteurs à cet événement pour traiter la requête et renvoyer une réponse appropriée. Cela permet une gestion efficace des requêtes HTTP asynchrones sans bloquer l'exécution du programme.

**Traitement des opérations asynchrones** : De nombreuses opérations dans Node.js sont asynchrones, telles que les opérations de lecture/écriture de fichiers, les appels réseau, etc. Les modules intégrés de Node.js utilisent souvent l'EventEmitter pour signaler la fin de ces opérations en émettant des événements tels que 'data' pour les flux de données ou 'close' pour les connexions de fichiers.

**Gestion des événements système** : Node.js peut également écouter et réagir à des événements système tels que la fin du processus, la réception de signaux (comme SIGINT pour un arrêt propre), etc. Encore une fois, l'EventEmitter est utilisé pour écouter ces événements et prendre des mesures appropriées.

**Construction de modules** : Les développeurs peuvent également utiliser l'EventEmitter pour construire des modules réutilisables qui émettent des événements pour indiquer des changements d'état ou des événements significatifs. Cela permet une communication efficace entre les différents composants d'une application Node.js.

**Gestion des erreurs** : L'EventEmitter est également utilisé pour la gestion des erreurs dans Node.js. Les erreurs peuvent être émises à l'aide de l'événement 'error', ce qui permet aux développeurs de capturer et de gérer les erreurs de manière centralisée.

###  Manipulation des événements

Vous pouvez créer, émettre et écouter des événements dans votre application Node.js.

Émetteur d'événements : L'EventEmitter est une classe qui expose plusieurs méthodes, telles que on, emit, et removeListener. Cette classe est utilisée pour créer un émetteur d'événements personnalisé dans votre application.

Événements : Un événement est une action qui se produit au sein de votre application, telle qu'une requête HTTP arrivant sur votre serveur, une connexion à une base de données, etc. Ces événements peuvent être associés à des chaînes de caractères, généralement appelées "noms d'événements".

Écouteurs d'événements : Vous pouvez attacher des fonctions (ou des callbacks) à des événements spécifiques. Ces fonctions sont appelées des écouteurs d'événements. Chaque fois que l'événement associé est émis, les écouteurs correspondants sont invoqués.

Émission d'événements : Lorsque quelque chose d'intéressant se produit dans votre application, vous pouvez émettre un événement en appelant la méthode emit sur votre EventEmitter. Tous les écouteurs attachés à cet événement seront alors invoqués avec les données éventuellement passées lors de l'émission.

Gestion des erreurs : L'EventEmitter prend également en charge la gestion des erreurs. Vous pouvez émettre des événements d'erreur ('error') pour signaler des conditions d'erreur dans votre application.

Utilisations courantes : L'EventEmitter est largement utilisé dans Node.js pour la création de serveurs, le traitement des requêtes HTTP, la gestion des flux de données, etc.

```
const EventEmitter = require('events');

// Créer un nouvel EventEmitter
const monEventEmitter = new EventEmitter();

// Attacher un écouteur d'événements pour l'événement 'message'
monEventEmitter.on('message', (msg) => {
  console.log(`Message reçu : ${msg}`);
});

// Émettre l'événement 'message'
monEventEmitter.emit('message', 'Bonjour le monde !');

```

## Ordre de traitement d'une requête Node.js

1. Réception de la Requête HTTP

Client envoie une requête HTTP : Un client (par exemple, un navigateur) envoie une requête HTTP à un serveur Node.js.
Event Loop : L'Event Loop de Node.js est constamment en attente d'événements. Lorsqu'une requête HTTP arrive, elle déclenche un événement.

2. Traitement de la Requête par le Serveur HTTP

Serveur HTTP (ex: Express) : Le serveur HTTP, souvent Express.js dans le contexte de Node.js, reçoit l'événement de la requête HTTP.
Middleware : Si des middleware sont définis, ils sont exécutés. Les middleware sont des fonctions qui ont accès à l'objet de requête (req), à l'objet de réponse (res), et à la fonction next.

Route Matching : Le serveur cherche la route correspondante en fonction de l'URL de la requête. Si une route correspond, la fonction associée à cette route est exécutée.

Event Emitter : Pendant ces étapes, des objets Event Emitter peuvent être utilisés pour déclencher des événements personnalisés. Par exemple, Express utilise un Event Emitter pour gérer les événements liés aux routes et aux middleware.

3. Exécution de la Logique de l'Application

Logique de l'Application : La fonction associée à la route est exécutée, effectuant la logique spécifique à l'application en fonction de la requête reçue.
Appels Asynchrones : Si des opérations asynchrones sont nécessaires (comme l'accès à une base de données, la lecture de fichiers, etc.), ces opérations sont déléguées à des mécanismes non bloquants (callbacks, Promesses, ou async/await).

4. Réponse HTTP

Création de la Réponse : Le serveur crée la réponse HTTP en utilisant l'objet de réponse (res) et y ajoute le corps de la réponse, les en-têtes, etc.
Event Loop : Le serveur déclenche un nouvel événement dans l'Event Loop pour indiquer que la réponse est prête.

5. Envoi de la Réponse au Client

Transmission de la Réponse au Client : La réponse HTTP est envoyée au client via le réseau.

Fin de la Requête : Le cycle de la requête est terminé.

# HTTP

Les messages HTTP (Hypertext Transfer Protocol) sont utilisés pour la communication entre clients (comme les navigateurs web) et serveurs sur Internet. Ils sont divisés en plusieurs types, chacun ayant une fonction spécifique. 

Voici un résumé des principaux types de messages HTTP et de leurs utilisations :

- GET : Ce type de requête est utilisé pour demander des données à partir d'une ressource spécifiée. Les paramètres sont généralement inclus dans l'URL. Les requêtes GET ne doivent normalement pas avoir d'effet de côté sur le serveur.
- POST : Les requêtes POST sont utilisées pour envoyer des données au serveur dans le corps de la requête. Elles sont souvent utilisées pour soumettre des formulaires en ligne ou pour effectuer des opérations qui peuvent avoir un effet de côté sur le serveur, comme la création d'une ressource.
- PUT : Ce type de requête est utilisé pour mettre à jour une ressource existante ou créer une ressource si elle n'existe pas. Le corps de la requête contient les données mises à jour.
- DELETE : Les requêtes DELETE sont utilisées pour demander la suppression d'une ressource spécifiée sur le serveur.
- HEAD : Ce type de requête est similaire à GET, mais le serveur ne renvoie que les en-têtes de la réponse, sans le corps. Il est souvent utilisé pour vérifier la validité d'une ressource sans télécharger l'intégralité de son contenu.
- PATCH : Les requêtes PATCH sont utilisées pour appliquer des modifications partielles à une ressource. Elles sont utiles lorsque vous ne souhaitez pas renvoyer l'ensemble des données, mais seulement les changements.
- OPTIONS : Les requêtes OPTIONS sont utilisées pour demander les méthodes de communication (par exemple, quels types de requêtes sont autorisés) disponibles pour une ressource spécifique.
- TRACE : Ce type de requête est rarement utilisé et est principalement destiné au débogage. Il permet de suivre la route qu'une requête prend lorsqu'elle traverse un réseau.


Les messages HTTP peuvent transporter des données dans différents formats, et le choix du format dépend souvent du type d'application et des besoins spécifiques. 

Voici un résumé des types de formats de message HTTP couramment utilisés :
- HTML (Hypertext Markup Language) : Utilisé pour représenter et formater le contenu des pages web. Les réponses HTTP renvoyant du contenu destiné à être affiché dans un navigateur sont généralement au format HTML.
- XML (eXtensible Markup Language) : Un format de données structuré, souvent utilisé pour l'échange de données entre applications. Il est extensible et peut être utilisé pour représenter une variété de structures de données complexes.
- JSON (JavaScript Object Notation) : Un format de données léger, lisible par les humains et facile à traiter côté serveur et côté client. Très populaire dans le développement web pour l'échange de données entre le client et le serveur.
- Texte brut (Plain Text) : Les réponses HTTP peuvent être simplement du texte brut, sans formatage particulier. Cela est parfois utilisé pour les réponses simples ou pour des données non structurées.
- Formulaires (application/x-www-form-urlencoded) : Les données de formulaire, généralement soumises via la méthode POST, sont encodées dans le corps de la requête au format x-www-form-urlencoded. C'est le format standard pour l'envoi de données de formulaire via HTTP.
Multipart (multipart/form-data) : Utilisé pour envoyer des fichiers binaires ou des données complexes via les formulaires HTML. Souvent utilisé avec la méthode POST pour la transmission de fichiers.
- Binaire (application/octet-stream) : Utilisé pour transmettre des données binaires non textuelles. Les fichiers tels que des images, des vidéos ou d'autres types de données binaire peuvent être transférés de cette manière.
- Protocole WebSocket (WebSocket Protocol) : Bien que cela ne soit pas un format de message HTTP à proprement parler, le protocole WebSocket est utilisé pour établir une connexion bidirectionnelle persistante entre un client et un serveur, permettant un échange de données en temps réel.

### TYPES DE CODE HTTP

#### 1xx (Informations) :
- 100 Continue : Indique que le serveur est prêt à recevoir la requête du client, mais celle-ci n'a pas encore été complètement envoyée.
#### 2xx (Succès) :
- 200 OK : Indique que la requête a réussi. C'est le code de statut standard pour une réponse réussie.
- 201 Created : Indique que la requête a été traitée avec succès, et qu'une nouvelle ressource a été créée.
- 204 No Content : Indique que la requête a été traitée avec succès, mais qu'il n'y a pas de contenu à renvoyer.
#### 3xx (Redirection) :
- 301 Moved Permanently : Indique que la ressource demandée a été déplacée de manière permanente vers une nouvelle URL.
- 302 Found : Indique que la ressource demandée se trouve temporairement à une autre URL. (Note : bien que largement utilisé, 302 a été remplacé par 303 et 307 dans certaines situations.)
- 304 Not Modified : utile pour le caching

#### 4xx (Erreur client) :
- 400 Bad Request : Indique que la requête du client est incorrecte ou mal formée.
- 401 Unauthorized : Indique que l'accès à la ressource est refusé en raison d'une authentification incorrecte ou absente.
- 403 Forbidden : Indique que le serveur comprend la requête du client, mais refuse de l'exécuter.
- 404 Not Found : Indique que la ressource demandée n'a pas été trouvée sur le serveur.

#### 5xx (Erreur serveur) :
- 500 Internal Server Error : Indique une erreur interne du serveur, souvent due à un dysfonctionnement du serveur.
- 502 Bad Gateway : Indique que le serveur, en agissant comme une passerelle, a reçu une réponse invalide depuis le serveur en amont.
- 503 Service Unavailable : Indique que le serveur n'est pas prêt à gérer la requête. Cela peut être dû à une surcharge temporaire ou à la maintenance du serveur.