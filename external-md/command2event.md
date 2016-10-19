## Structure d'un événement

```scala
trait BusinessEvent extends Event {
  def target: EntityId
  def who:    Identity
  def when:   DateTime
  def what:   Operation
  def why:    CommandRef
}
```




## Différents types d'opérations

```scala
sealed trait Operation
case class EntityCreation[Entity](initial: Entity) 
    extends Operation
case class FieldCreation[Field](is: Field) 
    extends Operation
case class FieldUpdate[Field](was: Field, becomes: Field) 
    extends Operation
case class FieldDeletion[Field](was: Field) 
    extends Operation
```

```scala
case JobStatusUpdated(
    jobId@JobId(_), _ , _ , FieldUpdate(_, Cancelled), _) =>
``` 
<!-- .element: class="fragment" -->

<aside class="notes">
    Besoins de serialisations différentes entre Creation et Update<br/>
    Faciliter la récupération de certains champ via pattern matching
</aside>



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
case class CommandRef(name: String, 
                      id: CommandId, 
                      n: Int = 0, 
                      of: Int = 0)
```