### Event handler

Consiste à appliquer la modification de l'événement sur l'état

```
val jobLenser = Lenser[Job] // macro monocle
val description = jobLenser(_.description)

object JobEventHandler {
   case JobDescriptionUpdated.operation(FieldUpdate(_, updated)) => 
      description.set(updated)(job)

}
```


<aside class="notes">
    Usage des lensers : plutôt pratique et succinct, facile à combiner<br/>
    + Difficile à écrire avec optional profond
</aside>