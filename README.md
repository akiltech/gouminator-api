# gouminator-api
api pour le gouminator

Nous utilisons une formule simple pour calculer le goumin __G__ en fonction du niveau de rayonnement __r__

```
G = 4/3 * π * r^3
```
Cette formule represente en fait le calcul du volume d'une sphere en fonction du rayon.

# Dependencies:

Les dependences sont en relation a votre choix de framework

# Installation

```bash
git clone https://github.com/akiltech/gouminator-api
cd gouminator
```                                                   

# 1. Rest API
Nous voulons creer un service REST qui prend comme parameter le niveau de rayonnement __r__ et nous retourne un object JSON avec le resultat du calcul du Goumin.

* Mettez en place votre framework de choix pour la creation d'une architecture REST(Custom/Symfony/Laravel/ExpressJS)
* Votre API devrait etre accessible sur le port `4001` `http://localhost:4001`
* Creez une route GET `/goumin/:rayonnement` ex `/goumin/5` qui prend un parametre `rayonnement`. Le parametre peut aussi etre envoye en query string ex: `/goumin?rayonnement=5`). La route retourne le resultat dans le format JSON suivant:

```
{
    rayonnement: 5,
    goumin: 200
}
```
La route doit **valider** que le parametre `rayonnement` est 
1. Fourni 
2. Est un nombre
3. Est moins ou egal a 100

*Pour chaque type d'erreur de validation, retournez un message de validation approprie si la validation echoue*

* Pour la valeur du Goumin, il faut l'arrondir au nombre entier superieur si le premier decimal est superieur a 5, sinon au nombre entier lui meme si elle est inferieure.
Example: 456.5569696 devient 457 mais 454.213232 devient 454.

* Tester et verifier que la route marche localement mais aussi qu'elle peut etre accedee par des applications venant de different domaines. Par example si votre api sera deployee sur www.goumin.com, l'equipe front end de l'application www.gouminator.com doit toujours pouvoir effectuer l'appel vers `/goumin` pour retourner le resultat.


* Cache: Sauvegardez le resultat de chaque calcul dans une base de donnee. A chaque nouvelle requete, verifier si le resultat est dans la base de donnee, si oui, retournez ce resultat, si non, faites le calcul , sauvegardez le resultat avant de le retourner

* Ajoutez au moins un test unitaire pour cette route et assurez vous que le(s) test(s) passe.

* Ajoutez une nouvelle route POST `/goumins` qui prend une liste de rayonnements en POST DATA et retourne une liste de goumins pour chacun des rayonnements dans la liste initiale. La logique doit marcher de la meme maniere que la route individuelle. Si la valeur du goumin pour le rayonnement existe dans la base de donnee, elle est retournee, sinon elle est calculee, sauvegardee et retournee vers la liste.

Example: 

Format du POST 
```
[5,10,3,22]
```

Format du JSON retourne:

```
[
    {
        rayonnement: 5,
        goumin: 200
    },
    {
        rayonnement: 10,
        goumin: 100
    }
    ...
]
```
* Sauvegardez votre application dans votre compte [Github](https://www.github.com)/[Gitlab](https://www.gitlab.com)

# 1. Bonus
* Ajoutez une pipeline CI pipeline pour deployer votre application ([CircleCI](https://circleci.com/), [TravisCI](https://travis-ci.org/))
* Deployez votre application sur la plateforme de votre choix
