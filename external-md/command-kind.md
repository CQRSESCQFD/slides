## Des événements différents

```
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

