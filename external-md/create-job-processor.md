### Exemple de processor
 
```scala 
implicit val updateJobProc = CommandProcessor[UpdateJob, Job] {
  cmd =>
    new CommandProcessor[UpdateJob, Job] {
    
    override def validator =
      StateIsNotNull[Job] |+| StatusIsOneOf(InReview, Pending)
   
    override def events(context: CommandContext) = (state: Job) =>
      ??? // TODO 
        
    }
}
```