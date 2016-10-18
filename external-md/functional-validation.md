#### Validation avec scalaz

```scala
def StateIsNotNull[E <: AnyRef]: Validator[E]=Reader {state=>
  if (state == null) StateShouldNotBeNull.failureNel[List[AnyEvent]]
  else Nil.successNel[CommandError]
}

def StatusIsOneOf(head: JobStatus,tail:JobStatus*): Validator[Job]={
  val statuses = head :: tail.toList
  Validator[Job] {
    job =>
      if(statuses.contains(job.status)) Nil.successNel[CommandError]
      else WrongJobStatus.failureNel[List[AnyEvent]]
  }
}
//possibilité de les combiner
StateIsNotNull[Job] |+| StatusIsOneOf(InReview, Pending)
```



#### Conversion des erreurs de validation en code http

```scala
def toError(key : String): (List[CommandError] => Result) =  {
    case StateShouldNotBeNull :: Nil => NotFound(key)
    case JobV.WrongJobStatus :: Nil => Conflict(key)
}
```

Note:
* Pas de gestion des erreurs multiples, mais le besoin ne s'est pas fait ressentir vis à vis des clients
* besoin de standardiser les clés pour un usage avec les properties bundles (i18n)




#### Validation niveau 2 métier (régles métiers) cas passant

<img class="stretch" src="/schemas/3-from-http-to-command.png"/>




####Contexte et traitement d'une commande

```scala
case class CommandContext(issuer: Identity,
                          when: DateTime,
                          command: Cmd,
                          commandId: CommandId)

trait CommandProcessor[C <: Cmd, E] extends Serializable {
  def validator: Validator[E]
  def events(context: CommandContext): E=> List[BusinessEvent]
}

type CommandValidation = ValidationNel[CommandError, List[AnyEvent]]
type Validator[E]      = scalaz.Reader[E, CommandValidation]

trait CommandError
case object NotRelevantCommand extends CommandError
```

Note:
* Définir a quoi servent les différentes variables // issuer avec jwt
* Ajouter + infos sur reader ???
* Ajouter + infos sur Validation
* Faut t'il faire apparaître commandId ???
