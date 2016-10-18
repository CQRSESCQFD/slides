## Une commande, un/des events

```scala
case object CreateJob extends JobCmd
object JobCreated extends EventCompanion[Job,  EntityCreation]

case class UpdateJobDescription extends JobCmd
object JobDescriptionUpdated extends 
       EventCompanion[String, FieldUpdate]

``` 
<aside class="notes">
    Granularité commande / event
    1 / 1 ou 1 -> N
</aside>



## Problème

* ça complique les traitements en aval

<aside class="notes">
    Quand une commande génère plusieurs events, on ne veut pas envoyer plusieurs fois le même email (par exemple)
</aside>



## Solution

* on contextualise les événements en y ajoutant des métadonnées

```scala
// TODO ajouter la classe de métadonnées
```


