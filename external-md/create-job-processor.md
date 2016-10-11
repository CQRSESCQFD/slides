### Exemple de processor
 
<pre>
<code data-trim data-noescape>
CommandProcessor[UpdateJob, Job] {
    cmd => new CommandProcessor[UpdateJob, Job] {
    
    override def validator =
        StateIsNotNull[Job] |+| StatusIsOneOf(InReview, Pending)
   
    override def events(context: CommandContext) = (state: Job) =>
        List(JobDescriptionUpdated(
             context, 
             FieldUpdate(state.description, cmd.job.description))
            )
</code>
</pre>