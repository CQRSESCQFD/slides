 ## Anatomie d'une commande


```
sealed trait Cmd
sealed trait UserCmd extends Cmd
sealed trait JobCmd extends Cmd

case object CreateJob extends JobCmd
case class UpdateJobDescription(description : String) extends JobCmd
case class AddSkill extends UserCmd
```

<aside class="notes">
    Qu'est ce qu'une commande ? <br/>
    Qu'est ce qu'une SAGA<br/>
    <mark>Saga</mark>: cas d'usage : creation d'un devis = ajout skill sur provider (si besoin) + création devis <br/>
</aside>