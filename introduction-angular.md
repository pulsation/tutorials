#Introduction à AngularJS

AngularJS est un *framework javascript open source* développé par Google. Il fournit un modèle structurant pour les *applications WEB*, tout en permettant entre autres d'enrichir le vocabulaire HTML (framework déclaratif). Il offre aussi la possibilité de réaliser des applications WEB monopages (SPA pour *Single Page Applications*).

####Exemples

Voici quelques applications réalisés avec AngularJS:

* http://sbb.cellfinder.org/ (exploration d'anatomie)
* http://public.opendatasoft.com/explore/ (explorateur de données ouvertes)
* http://www.vevo.com/ (plateforme de diffusion vidéo)
* http://app.hya.io/ (synthétiseur)

D'autres exemples sont disponibles sur https://builtwith.angularjs.org/ .

####Valeur ajoutée

Avec des frameworks traditionnels tels que JQuery ou Dojo, la dynamisation d'une page WEB passe par la manipulation directe des instances des éléments HTML qu'elle contient (éléments du DOM), le plus souvent à l'aide de sélecteurs. Il est par conséquent nécessaire de se préoccuper tout particulièrement du fonctionnement du navigateur, ainsi que de l'organisation visuelle de la page HTML lors de la réalisation de l'application. 

Or, l'organisation des éléments visuels ne représente pas forcément la façon dont on souhaite organiser l'application en elle-même.

AngularJS encapsule le dialecte utilisé par JQuery dans une couche bas niveau, ce qui ne rend plus nécessaire la manipulation directe des éléments du DOM lors de la réalisation d'une application. 

En effet, il fournit un mécanisme de liaison *forte et implicite* (on n'a plus besoin de l'exprimer avec du code redondant) entre la vue (page affichée dans le navigateur) et les données qui doivent être représentées visuellement (couche ViewModel).

D'autre part, le paradigme MVW (pour Model View Whatever, proche en réalité de MVVM, *Model / View / ViewModel*) sur lequel est basé AngularJS,  permet de structurer d'emblée le code javascript en *couches logicielles* dont les responsabilités sont bien définies :

* Une couche modèle (*Model*), qui représente les entités à manipuler (par exemple, des objets issus de web services).
* Une couche Vue (*View*), qui est la représentation visuelle des données.
* Une couche  *Whatever* (littéralement, "peu importe", en référence aux querelles de clocher) composée entre autres :
    * Du *ViewModel*, qui est une représentation directe des données représentées dans la vue, et permet de faire le lien entre modèle et vue.
    * De *contrôleurs* qui constituent le liant entre ces données, et permettent de les manipuler.

Enfin, le système de directives permet de créer des composants réutilisables, et de les combiner pour en faire des widgets (composants d'interface graphique) plus complexes.

###Préparation des exercices

* Lancer google chrome en désactivant les contrôles de same origin policy (nécessaire pour les appels de webservices tiers dans les exercice 8, 9 et 10) - par exemple sous windows: 
    * créer un raccourci de Chrome sur le bureau.
    * cliquer avec le bouton droit dessus pour accéder à ses propriétés.
    * ajouter dans le champ cible tout à la fin : –disable-web-security .
* Se rendre sur le site http://plnkr.co/ une fois Chrome lancé à partir de ce raccourci.
* Cliquer sur launch the editor.
* dans le volet de droite, dans search package, taper angular-ui puis tapper sur enter.
* Cliquer sur la baguette magique située à droite de angular-ui-bootstrap ainsi que celle de angular-ui.

###Pour aller plus loin
* https://docs.angularjs.org/guide/introduction 
* https://docs.angularjs.org/guide/providers 

##Associer entre les données et leur représentation

Comme indiqué précédemment, AngularJS se base sur une implémentation du dialecte proposé par jQuery (avec lequel il est compatible) pour manipuler le DOM à bas niveau. Cela lui permet de fournir un système de liaison (ou *binding*) bidirectionnelle entre les éléments de la vue et les variables qui leurs sont associées. Il en résulte une mise à jour immédiate et implicite de la vue lorsque le contenu des variables change par programmation, et inversement.

###Exercice 1 : Création d'une application

Dans le fichier *script.js*, ajouter

    var app = angular.module('hinnoya', ['ui']);

###Exercice 2 : Création d'un contrôleur

A la suite de la ligne précédente, ajouter :

    app.controller('MainCtrl', function($scope) {
    }); 

`$scope` représente la couche *ViewModel*, et est injecté automatiquement dans le contrôleur lors de son appel par Angular par un mécanisme d'inversion de contrôle (IOC).

###Exercice 3 : Affectation d'une valeur à une variable du ViewModel

A l'intérieur des accolades précédentes du contrôleur `MainCtrl`, ajouter la ligne suivante :

    $scope.name = "Jean-Pierre";

Cela permet d'initialiser la variable `name` qui va être utilisée dans le template.

Le fichier *script.js* devrait maintenant ressembler à ceci:

    // Code goes here
    var app = angular.module('hinnoya', ['ui', 'ngResource']);
    
    app.controller('MainCtrl', function($scope) {
        $scope.name = "Jean-Pierre";
    }); 

###Exercice 4 : Ajout d'une variable de template

Les variables de templates sont définies par des doubles accolades. Par exemple la variable associée à `$scope.moustache` dans le code Javascript sera représentée par `{{moustache}}` dans le code HTML.

Dans la fenêtre d'édition d'*index.html*, apparait le texte 

    <h1>Hello Plunker!</h1>

Remplacer le mot `Plunker` par `{{name}}` pour obtenir:

    <h1>Hello {{name}}!</h1>

Lorsque l'on clique sur *Run*, le texte *Bonjour Jean-Pierre !* devrait apparaitre.

###Pour aller plus loin

https://docs.angularjs.org/guide/databinding 

##MVW

AngularJS est basé sur le paradigme *Model View Whatever*, relativement proche de MVVM (*Model View ViewModel*), dont le principe est d'organiser l'application en différentes couches logicielles.

La couche *View* est la représentation visuelle des données manipulées par l'utilisateur dans l'interface graphique. Dans le cas d'AngularJS, elle est décrite directement en HTML.

La couche *ViewModel* correspond à la représentation programmatique de ces données visuelles. Lorsqu'on utilise Angular, il s'agit de l'idiome `$scope`.

Enfin, la couche *Model* décrit les données représentées par l'application ainsi que les traitements qui leurs sont appliqués. Dans le cas d'AngularJS, elles sont manipulées par des contrôleurs (au sens MVC). Il est tout à fait possible de déléguer la gestion de la couche modèle à un serveur distant par l'intermédiaire de "resources" RESTful.

D'autre part, par le biais de l'idiome `$watch`, il est possible de déclencher une fonction écouteur dès qu'une variable de `$scope` est mise à jour.

###Exercice 5 : Ajout d'une balise `<input>` liée à une variable du viewmodel

Dans index.html, ajouter la ligne suivante à la suite de la ligne qui débute par `<h1>` :

    <input type="text" ng-model="name"></type>

L'attribut *ng-model* permet d'indiquer à quelle variable contenue dans `$scope` cet élément visuel est lié. Ainsi, lorsque l'on modifie la valeur située dans le champ de saisie défini par la balise input, la valeur de la variable du ViewModel name sera automatiquement mise à jour.

D'autre part, la variable de template `{{name}}` associée à cette variable du ViewModel `$scope` sera elle aussi automatique mise à jour et affichée dynamiquement dans la page HTML lorsque la valeur du champ de saisie aura été modifiée.

###Exercice 6 : Mise en place d'un observateur

Dans *index.html*, ajouter à la suite de la ligne contenant la balise `<input>` que nous venons de définir la ligne suivante :

    <div class="alert-info">
      <div class="glyphicon glyphicon-info-sign"></div> 
      Longueur du texte: {{nameLength}} caractères
    </div>

Dans *script.js*, initialiser la valeur de la variable `nameLength` de `$scope` à 0 au sein du contrôleur:

    $scope.nameLength = 0;

Ajouter un observateur de type `$watch` sur la variable name du ViewModel :

    $scope.$watch('name', function (newValue, oldValue) {
    });

Dans cet écouteur, mettre à jour la variable `nameLength` du ViewModel `$scope` en ajoutant entre les accolades :

    $scope.nameLength = newValue.length;

Le code Javascript du contrôleur devrait alors ressembler à :
    
    app.controller('MainCtrl', function($scope) {
        $scope.name = "Jean-Pierre";
        $scope.nameLength = 0;
        $scope.$watch('name', function (newValue, oldValue) {
            $scope.nameLength = newValue.length;
        });    
    }); 
    
###Pour aller plus loin
* https://docs.angularjs.org/api/ng/type/$rootScope.Scope 
* https://docs.angularjs.org/api/ngResource/service/$resource 
* https://plus.google.com/+AngularJS/posts/aZNVhj355G2 

##Injection de dépendances

Dans un module Angular, les méthodes de type fabrique (ou *factory*) permettent de créer des objets que l'on pourra injecter dans d'autres modules. C'est de cette façon que sont injectés les *services* (qui pourraient correspondre à des *singletons*).

###Exercice 7 :Ajout d'un module

Cliquer sur l'icône correspondant à un livre complètement à droite de la page Plunker (*find and external libraries*).

Rechercher *angular-resource* puis cliquer sur la baguette magique à côté du résultat pour l'inclure. Cela ajouter automatiquement la balise 

    <script data-require="angular-resource@*" data-semver="1.2.14" src="http://code.angularjs.org/1.2.14/angular-resource.js"></script>

correspondante dans le code HTML.

Dans *script.js*, ajouter `'ngResource'` au même niveau qu'`'ui'` lors de la définition de l'application :
    
    var app = angular.module('hinnoya', ['ui', 'ngResource']);

###Exercice 8 : Création d'une factory *Weather* pour étendre un composant Angular existant

Ajouter au dessus de la définition du contrôleur dans *script.js* :

    app.factory('Weather', ['$resource', function ($resource) {
    }]);

Cette factory va retourner le résultat de l'appel d'un webservice dont l'URL est pré-configurée. Pour cela, insérer entre ses accolades : 

    return $resource('http://api.openweathermap.org/data/2.5/weather?q=:place');
    
La factory devrait au final ressembler à ceci:

    app.factory('Weather', ['$resource', function ($resource) {
        return $resource('http://api.openweathermap.org/data/2.5/weather?q=:place');
    }]);

###Exercice 9 : Injection dans le contrôleur

Ajouter la factory Weather à injecter parmi les paramètres du contrôleur, à la suite de `$scope` :

    app.controller('MainCtrl', function($scope, Weather) {
    [...]

###Exercice 10 : Appel d'un webservice

Dans *script.js*, Appeler la resource qui correspond au webservice, et lorsque la requête HTTP est exécutée,  affecter la bonne valeur à la variable `weather` de `$scope` :

    $scope.weather = "Unknown";
    Weather.get({place: "Lyon,France"}).$promise.then(function (data) {
        $scope.weather = data.weather[0].description;
    });

Ajouter la variable de template correspondante dans *index.html* :

    <div class="alert-success">
      <div class="glyphicon glyphicon-cloud"></div>
      La météo aujourd'hui: {{weather}}
    </div>

###Pour alle plus loin
* https://docs.angularjs.org/guide/di 
* https://docs.angularjs.org/api/ngResource/service/$resource 


##Directives

Les directives sont instanciées par le système d'injection de dépendances, et permettent d'augmenter le vocabulaire HTML des vues AngularJS.

###Exercice 11 : Définition d'une directive

Ajouter après la définition du contrôleur :

    app.directive('address', function () {
        return {
            template: '<p>Adresse</p>'
        };
    });

Il est maintenant possible d'utiliser une balise `<address>` directement dans le code HTML :

    <address></address>

###Exercice 12 : Paramétres de la directive

Au dessus du template de la directive, on peut définir des paramètres que l'on pourra donner à la balise :

    scope: {
      street : '=',
      city: '='
    }

Puis ensuite, modifier le template pour les prendre en compte :

    template: '<p><div class="glyphicon glyphicon-road"></div> {{street}}, {{city}}</p>'

Et enfin, modifier l'appel à la balise :

    <address street="'50 cours de la République'" city="'Villeurbanne'"></address>

###Pour aller plus loin
https://docs.angularjs.org/guide/directive 

## Intégralité du code source de l'exercice

L'ensemble du code source est disponible sur http://plnkr.co/edit/YjqYsh .