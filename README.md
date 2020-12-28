# MVC-Core
![Logo UCA - IUT|](images/Logo_IUT-icon.png)
## Introduction
Le Patron de Conception  « MVC » s'inscrit dans le cadre d'une architecture à 3 niveaux :

* Données : données persistantes (e.g. base de données) ;
* Service : logique de l'application ;
* Présentation : HTML, CSS, Javascript, Web Services...

 Pour une application Web, le MVC se situe dans le niveau *Présentation* de l'architecture ci-dessus :
* Données : ...;
* Service : ...;
* Présentation :
    * Le Contrôleur : intercepte la requête HTTP et renvoie la réponse HTTP ;
    * Le Modèle : stocke les données à afficher / traiter ;
    * La Vue: organise la sortie / l'affichage.

Le cycle de vie d'une requête HTTP typique :

1. L'utilisateur envoie la requête HTTP ;
2. Le contrôleur l'intercepte ;
3. Le contrôleur appelle le service approprié ;
4. Le service appelle le DAO approprié, qui renvoie des données persistantes (par exemple) ;
5. Le service traite les données et renvoie les données au contrôleur ;
6. Le contrôleur stocke les données dans le modèle approprié et appelle la vue appropriée ;
7. La vue est instanciée avec les données du modèle et renvoyée en tant que réponse HTTP.

Ceci peut se schématiser de la façon suivante :

# MVC-Core version 02
![Logo UCA - IUT|](images/Logo_IUT-icon.png)
## Introduction
Nous allons utiliser à partir de maintenant le logiciel gestionnaire de dépendances écrit en PHP **Composer**.
Celui-ci va nous permettre de :
* déclarer et d'installer les bibliothèques dont votre projet principal a besoin,
* gérer les dépendances desdites bibliothèques,
* mettre à jours lesdites bibliothèques,
* de bénéficier d'une solution d'auto-chargement des différentes classes du projet : plus de **include_once** ou de **require_once** à gérer.

[Composer](https://getcomposer.org/)

```
Installation de « Composer » (il est nécessaire d'avoir déjaà installé PHP) :

$ # macOS
$ brew install composer
$ # Linux
$ apt-get install composer
$ aptitude install composer
```
```
$ # Version 01 => 02
$ rsync	-auv mvc-core_01/ mvc-core_02/
$ cd mvc-core_02/
$ composer -n init \
	--name "jmbruneau/mvc-core" \
	--description "Basic MVC PHP Framework" \
	--author "Jean-Michel BRUNEAU <jean-michel@netspace.mc>" \
	--type "project" \
	--license "GPL"

$ cat composer.json
{
    "name": "jmbruneau/mvc-core",
    "description": "Basic MVC PHP Framework",
    "type": "project",
    "license": "GPL",
    "authors": [
        {
            "name": "Jean-Michel BRUNEAU",
            "email": "jean-michel@netspace.mc"
        }
    ],
    "require": {}
}
```
## Installation des dépendances :

Recherche d'une bibliothèque :

```
$ composer search composer/
```

### L'« autoloader »
```
$ composer require composer/composer
$ ls vendor/
autoload.php  bin  composer  justinrainbow  psr  react  seld  symfony
```
### Configuration de l'« autoloader » de type « classmap <br />(c.f. documentation de Composer)
```
$ # Edition de composer.json et ajouts des dossiers contenant nos différentes classes
$ nano composer.json
	"require" : {},
	"autoload" : {
		"classmap": [
			"controllers",
			"dao",
			"data",
			"etc",
			"models",
			"views"
		]
	}
$ composer dump-autoload -o
```
### Inclusion de **vendor/autoload.php** dans **index.php**
```
require __DIR__ . '/vendor/autoload.php';
```
> Il est ensuite nécessaire de mettre en place les différents **espaces de nom** dans l'ensemble des fichiers de notre projet.
> L'espace de nom du projet est ici « mvcCore »
> Il faut ensuite supprimer l'ensemble des include, include_once, require, requice_once présent dans les scripts.
> Enfin, il faut vérifier que tout fonctionne correctement ;)

### Framework HTML, CSS & Javascript « Bootstrap »
```
$ # Get bootstrap
$ composer search bootstrap
$ composer require twbs/bootstrap
$ # See css and js files
$ ls vendor/twbs/bootstrap/dist/js/
$ ls vendor/twbs/bootstrap/dist/css/
$ # Make the ad-hoc links (development version)
$ cd css
$ ln -s ../vendor/twbs/bootstrap/dist/css/bootstrap.css bootstrap.css
$ # Optional : for debuging purpose
$ ln -s ../vendor/twbs/bootstrap/dist/css/bootstrap.css.map bootstrap.css.map
$ cd ../js
$ ln -s ../vendor/twbs/bootstrap/dist/css/bootstrap.js bootstrap.js
$ # Optional : for debuging purpose
$ ln -s ../vendor/twbs/bootstrap/dist/css/bootstrap.js.map bootstrap.js.map
```
> Il est ensuite nécessaire d'intégrer « bootstrap.css » et « bootstrap.js » au niveau de notre template…

[Bootstrap documentation](https://getbootstrap.com/docs/4.5/components/forms/)
### Installation de « jQuery »
[jQuery download](https://jquery.com/download/)

```
$ cd js
$ # Download jquery library (development version)
$ wget https://code.jquery.com/jquery-3.5.1.js
$ # Download jquery library (production version)
$ wget https://code.jquery.com/jquery-3.5.1.min.js
$ # Make the ad-hoc link (development version)
$ ln -s jquery-3.5.1.js jquery.js
$ # Make the ad-hoc link (production version)
$ # ln -s jquery-3.5.1.min.js jquery.js
```
## Améliorations et modifications (c.f. version 01)

### Model.php : abstract class, abstract method(s), factorisation(s)

>
>
>

### Controller.php : bstract class, abstract method(s), factorisation(s)

>
>
>

### View.php : bstract class, abstract method(s), factorisation(s)

>
>
>

# MVC-Core version 03
![Logo UCA - IUT|](images/Logo_IUT-icon.png)
## Introduction
```
$ rsync -auv mvc-core_02/ mvc-core_03/
$ cd mvc-core_03/
$ git commit -a -m 'version 03'
```
## Améliorations et optimisations (c.f. version 02)

### Création d'un dossier « helpers/ » pour y placer nos classes « utilitaires »
* Prise en compte de ce dossier dans la configuration de l'autoloader

```
	"autoload" : {
		"classmap" : [
			"controllers",
			"dao",
			"data",
			"etc",
			"helpers",
			"models",
			"views"]
	}
```
* Mise en place d'une classe « Url » permettant de manipuler les URLs avec comme espace de nom « mvcCore\Helpers ».
Ne pas oublier d'effectuer :

```
$ composer dump-autoload -o
ou
$ composer update
```
### data/Cars.php
* Erratum: brend => brand (marque) !

### models/OrderModel.php
* Erratum: brend => brand (marque) !

### views/templates/OrderCreate.tpl.php
* Erratum: brend => brand (marque) !

### Controller.php
* Mise en place progressive des méthodes abstraites relatives aux différentes opérations du CRUD : create(), read(), update() et delete().
* Définition d'une méthode abstraite « imput() » pour capter et assigner les différentes proprétés d'un modèle.
* Intégration d'une méthode display() pour l'affichage du modèle dans un template donné.
* Intégration d'une méthode redirect() pour effectuer des redirections HTTP.
* Intégration d'une méthode persit() pour effectuer une persistance des données du modèle dans la base de données.
* Gestion des erreurs (try catch throw)…

### controllers/OrderController.php
* Déplacement des propriétés spécifiques à la vue dans celle-ci, soit ici dans la classe « OrderCreateView.php ».
* Définition de la méthode « imput() » rélative au modèle « Order ».
* Mise en oeuvre d'un méthode privée pour le calcul du prix total : _total_price().
* Intégration de la méthode read().

### View.php
* Création d'un sous-dossier par Modèle dans le dossier « views/ », soit ici du dossier « Order/ »
* Actualiser alors l'autoloader avec la commande « composer update »
* Définition d'une méthode abstraite setProperties()

### dao/DAO.php
Intégration des méthodes :
* create() (à la place de persit() dans la version 02),
* read(),
* update(),
* et delete().
* Gestion des erreurs (try catch throw)…

### etc/Config.php
* Ajout de paramètres par défaut pour l'action et le modèle
* Syntaxe HTML versus XHMTL pour les *required*, *selected* et *checked*

### Porte d'entrée « index.php »

* Définition d'un variable globale $GLOBALS['request'] avec les paramètres via *index.php*
* Gestion des erreurs (try catch)
* Commentaires ;)

# MVC-Core version 04
![Logo UCA - IUT|](images/Logo_IUT-icon.png)
## Introduction
```
$ rsync -auv mvc-core_03/ mvc-core_04/
$ cd mvc-core_04/
$ git commit -a -m 'version 04'
```
## PHP

* Elimination des balises de fermeture de PHP "?>" pour éviter des potentiels saut de ligne avant le *<!DOCTYPE html>*
* Ajout d'un fichier .htaccess afin de rediriger toute URL vers le point d'entré unique « index.php » (sécurité renforcée).
* Nom de la session personnalisée : Config::SESSION_NAME = 'MVCCORE'.

## Ajout de fonctionnalités

* dossier admin/ pour une partie administration (modifications ad-hoc .htaccess)
* début de mise en place de commentaires conforme à PHPdoc :
    * https://github.com/phpDocumentor/fig-standards/blob/master/proposed/phpdoc.md
    * https://manual.phpdoc.org/HTMLSmartyConverter/HandS/phpDocumentor/tutorial_tags.pkg.html(e.g. la classe mvcCore\Helpers\Url)

## Ajout des classes liées au différentes actions pour le modèle « Order » intégrées dans le contrôleur OrderControleur.php

* View :
    * OrderReadView.php
    * OrderUpdateView.php
    * OrderDeleteView.php
    * factorisation du code avec la définition d'un *trait* **OrderView.php**
* Template :
    * OrderRead.tpl.php
    * OrderUpdate.tpl.php
    * OrderDelete.tpl.php

## Chiffrement des certaines données pour être conforme à la législation : Commission Nationale de l'Informatique et des Libertés (CNIL) et au Règlement Général sur la Protection des Données (RGPD).

Mise en place d'une classe de chiffrement et déchiffrement : \Helpers\Crypt :
* Chiffrement des données avant leurs persistances en base de données.
* Déchifrement des données après leurs lectures en base de données.

# MVC-Core version 05
![Logo UCA - IUT|](images/Logo_IUT-icon.png)
## Introduction
```
$ rsync -auv mvc-core_04/ mvc-core_05/
$ cd mvc-core_05/
$ git commit -a -m 'version 05'
```
## Mode développement et production

> Création de 2 fichiers de configurations spécifiques :
* Config.dev.php
* Config.prod.php

## Mise en place d'une classe « Template »
L'objectif est de 
