#### Validation métier (cas OK)

<img class="stretch" src="/schemas/3-from-http-to-command.png"/>




#### Validation métier (cas KO)
<img class="stretch" src="/schemas/2-from-http-to-command-missing-field.png"/>

<aside class="notes">
    Validation d'une commande, réutilisation des contraintes,
</aside>




####Contexte et traitement d'une commande
```scala
import scalaz._, Scalaz._
```
<!-- .element class="fragment" -->

```scala
type CommandValidation = ValidationNel[CommandError, List[Event]]
```
<!-- .element class="fragment" -->

```scala
type Validator[State]  = scalaz.Reader[State, CommandValidation]
```
<!-- .element class="fragment" -->

```scala
case class CommandContext(issuer: Identity,
                          when: DateTime,
                          command: Cmd,
                          commandId: CommandId)
```
<!-- .element class="fragment" -->

```scala
trait CommandProcessor[C <: Cmd, State] extends Serializable {
  def validator: Validator[State]
  def events(context: CommandContext): State => List[Event]
}

```
<!-- .element class="fragment" -->

Note:
* Définir a quoi servent les différentes variables // issuer avec jwt
* Ajouter + infos sur reader ???
* Ajouter + infos sur Validation
* Faut t'il faire apparaître commandId ???




#### exemples de validator

```scala
def StateIsNotNull[E <: AnyRef]: Validator[E] = Reader { state =>
  if (state == null) StateShouldNotBeNull.failureNel[List[Event]]
  else Nil.successNel[CommandError]
}

def StatusIsOneOf(head: JobStatus,tail:JobStatus*): Validator[Job]={
  val statuses = head :: tail.toList
  Validator[Job] {
    job =>
      if(statuses.contains(job.status)) Nil.successNel[CommandError]
      else WrongJobStatus.failureNel[List[Event]]
  }
}
//possibilité de les combiner
StateIsNotNull[Job] |+| StatusIsOneOf(InReview, Pending)
```

