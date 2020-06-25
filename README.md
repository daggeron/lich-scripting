# lich-scripting
Various scripts I maintain


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
command_watcher.on("helloworld") do |args|
  Utitilies::send_formatted("**Hello world**")
end

#After script is running type :sy or sym or symbo or symbol
#Will also not suppress the base symbol command
command_watcher.on("symbol", "sy[mbol|mbo|mb|m]*", false) do |args|
  Utitilies::send_formatted("**Sent symbol command**")
end

#Start monitoring for supplied commands
command_watcher.start

#After 10 seconds say hello again
helloworld2 = timers.after(10) {
  Utitilies::send_formatted("!!HELLO WORLD AGAIN!!")
}



#Every 5 second beep basically
every_five_seconds = timers.every(5) { 
  Utitilies::send_formatted("**Another 5 seconds**")
}
#For more timer examples
#https://github.com/socketry/timers


mutex = Mutex.new
resource = ConditionVariable.new

a = Thread.new {
  mutex.synchronize {
    resource.wait(mutex)
  }
}

a.join

```
