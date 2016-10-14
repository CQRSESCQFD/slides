## Des événements différents

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
