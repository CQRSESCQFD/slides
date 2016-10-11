### Event handler

Consiste à appliquer la modification de l'événement sur l'état

<pre>
<code data-trim data-noescape>
// macro monocle
val description = Lenser[Job](_.description)

object JobEventHandler {
   case JobDescriptionUpdated.operation(FieldUpdate(_, updated)) => 
      description.set(updated)(job)
}
</code>
</pre>


<aside class="notes">
    Usage des lensers : plutôt pratique et succinct, facile à combiner<br/>
    + Difficile à écrire avec optional profond
</aside>