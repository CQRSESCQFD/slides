## CRQS

* <mark>C</mark>ommand <mark>Q</mark>uery <mark>R</mark>esponsability <mark>S</mark>egregation
* Greg Young

<aside class="notes">
 Ici on raconte l'état du code avant le refactoring
 On parle aussi de Write-model VS Read-model
</aside>



## CQRS + CRUD

* première partie du refactoring
* on remplace les écritures directes par des commandes

<aside class="notes">
Préciser que CQRS ne présuppose rien sur le stockage
</aside>



## CQRS + ES

* deuxième étape
* on remplace l'effectuation des commandes par des emissions d'événements



## CQRS+ES à Hamak

![](images/cqrs-hamak.png)


## CQRS + ES = **<3**<!-- .element: class="fragment highlight-red" data-fragment-index="1" --->

<aside class="notes">
    Le combo CQRS+ES est plutôt naturel
    C'est ce qui est fourni par Akka-persistence
</aside>



## CQRS+ES à Hamak

* 1 commande => N événements
* 1 flux eventstore par entité
* Snapshots dans mongo
* 1 snapshot après chaque commande

<aside class="notes">
    <ul>
        <li>Parler des queries sur 1 entité VS queries sur +s entités</li>
        <li>Noter que c'est le read-model du pauvre</li>
    </ul>
</aside>