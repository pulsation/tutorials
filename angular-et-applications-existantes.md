#Intégrer Angular dans des applications existantes

### Compatibilité avec les anciens navigateurs

Au moins deux options sont possibles à ce niveau. 

####Conserver le mode de compatibilité

Tout d'abord, le premier souci est de s'assurer de la compatibilité avec les navigateurs anciens, en particulier Internet Explorer. Typiquement, les versions d'IE, même récentes, peuvent tourner en "mode de compatibilité", afin de préserver l'affichage des applications anciennes.

Il est possible d'assurer une compatibilité jusqu'à jusqu'à IE7 en utilisant AngularJS 1.0.x. Dans ce cadre, il faut forcer l'ID de l'élément qui contiendra l'attribut *ng-app* :

    <body ng-app="myApp" id="ng-app">

 Ref.: <http://stackoverflow.com/a/15920889>

####Forcer la désactivation du mode de compatibilité

Il est aussi possible de forcer Internet Explorer à ne pas tourner en mode de compatibilité en ajoutant les attributs suivants au tag *html* :

    <html xmlns:ng="http://angularjs.org" id="ng-app" ng-app="myApp"> 
    
Ref.: <http://stackoverflow.com/a/25633673>

Cependant, cela peut rendre l'affichage de l'application complètement illisible.

###Cohérence des données

####Périmètre d'utilisation

AngularJS est conçu pour fonctionner de préférence avec des applications mono-pages. Il est cependant tout à fait possible de délimiter son périmètre d'utilisation au sein d'une page existante dans l'application, en déterminant quels tags porteront les attributs *ng-app* et *ng-controller*.

####Rechargement de page

Pour la même raison, les valeurs des formulaires ne sont pas prises en compte lorsqu'elles sont affectées de façon traditionnelle (par exemple, l'attribut *CHECKED* d'une case à cocher ne sera pas pris en compte).

Afin de charger les bonnes valeurs pour les champs concernés, il est possible de les initialiser avec l'attribut *ng-init*, afin qu'elles soient prises en compte après le rechargement d'une page de l'application.