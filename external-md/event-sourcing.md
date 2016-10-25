## ES : l'idée

* Stocker la *représentation immuable* <!-- .element: class="fragment highlight-green" data-fragment-index="1" --> des événements qui ont eu lieu *dans le passé*<!-- .element: class="fragment highlight-green" data-fragment-index="2" -->
* Reconstruire l'état *courant*<!-- .element: class="fragment highlight-blue" data-fragment-index="3" --> en relisant les événements *depuis le début*<!-- .element: class="fragment highlight-red" data-fragment-index="4" -->




## ES : Problèmes

* append only
* temps de démarrage
* comment gérer la consistance ?
* immuabilité 

<aside class="notes">
    On reviendra plus tard sur les solutions à ces problèmes
    <ul>
        <li>append only => rédhibitoire dans les années 80/90 à cause du prix des disques, conséquence, on préfère le CRUD</li>
        <li>temps de démarrage => faux problème</li>
        <li>consistance => CQRS + causal consistency</li>
        <li>immuabilité => problème pour faire évoluer le schéma des events</li>
    </ul>
</aside>




## ES : Avantages

* immuabilité
* découplage
* intuitivité

<aside class="notes">
    <ul>
        <li>immuabilité => zéro perte d'information, on peut faire plusierus choses avec le même event, le distribuer, fixer des bugs a posteriori</li>
        <li>découplage entre le modèle métier (état) et le schéma de stockage (events)</li>
        <li>intuitivité => c'est un modèle plus proche de la façon dont les humains perçoivent le monde</li>
        <li>Audit et historique </li>
    </ul>
</aside>



## ES : Acteurs persistants

* correspond à un flux d'événements
* responsable de la transactionalité
* maintient l'état 

<aside class="notes">
    <ul>
        <li>parler de la consistance, mais sans entrer dans les détails (=> partie CQRS)</li>
    </ul>
</aside>



```scala
val emptyState: State = ???

val eventHandler: (State, Event) => State = ???

def currentState(events: Seq[Event]) =
  events.foldLeft(emptyState)(eventHandler)
```



## ES : Snapshots

* "photo" de l'état courant d'un aggrégat à un instant T
* permet de gagner du temps de démarrage



## ES : Hamak

* un flux par entité (user/job)
* events : eventstore
* snapshots : MongoDB




## Eventstore

* projet initié par Greg Young
* stockage des événements en JSON ou en binaire
* 5k/s en écriture 15k/s en lecture

<aside class="notes">
  TODO Screenshot ? démo ?
</aside>



![Stream](images/eventstore_global.png)



![Stream](images/eventstore_single.png)