# lich-scripting
Various scripts I use


How to use oleani-lib.lic
Quick and dirty

```ruby
load 'scripts/oleani-lib.lic'

timers = Timers::Group.new
timer_thread = Thread.new {
  loop {
    sleep (0.1)
    timers.wait
  }
}


command_watcher = Utitilies::CommandMonitor.new

#After script is running type : helloworld
command_watcher.on("helloworld"") do |args|
  Utitilies::send_formatted("**Hello world**")
end

#After 10 seconds say hello again and then exit
helloworld2 = timers.after(10) {
  Utitilies::send_formatted("!!HELLO WORLD AGAIN!!")
  exit
}







mutex = Mutex.new
resource = ConditionVariable.new

a = Thread.new {
  mutex.synchronize {
    resource.wait(mutex)
  }
}

a.join

```
