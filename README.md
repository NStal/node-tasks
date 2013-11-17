node-tasks
==========

A very handy nodejs async lib to handle some named limited parallel works. 

```coffee-script
Tasks = require "node-tasks"
tasks = new Tasks("initDb","setupSocket","loadCustomConfig");
tasks.on "done",() => 
  console.log "done!"
  console.log tasks.hasDone  # => true
  task.done("loadCustomConfig") # => nothing happend we won't fire `done` twice unless you reset it
  # you can reset it if you want
  tasks.reset()
  console.log tasks.hasDone # => false
  
setTimeout (() ->
  tasks.done "initDb"
  ),100

setTimeout (() ->
  tasks.done "setupSocket"
  ),100

setTimeout (() ->
  tasks.done "loadCustomConfig"
  ),100
try 
  tasks.done "invalid Task"
catch e
  console.log e  # => unknown task invalid Task

```
