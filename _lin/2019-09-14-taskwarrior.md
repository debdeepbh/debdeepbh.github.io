---
title: A quick guide to managing tasks using taskwarrior
tags: taskwarrior productivity todo 
---

[Taskwarrior](https://taskwarrior.org/) is a command-line based productivity software. You can use it to maintain a simple shopping list, but it is capable of much more. It is lightweight, open-source and most importantly, terminal-based. This makes it much more powerful than other TODO lists such as [Trello](https://trello.com/).

It is easy to run a Taskwarrior server locally and manage tasks  over a group of people.

### Install
* On Arch, it is called just `task`
```
pacman -S task
```
* On Ubuntu
```
sudo apt-get install taskwarrior
```

### Run
 Then run it using `task`. You'll be prompted to create the config file. Say yes.
 Modify the `.taskrc` file to use the light-256 theme, which works best with white terminal background. If you ever consider shifting to a darker terminal, consider exploring other themes. I recommended dark-256, obviously.
 
`git add` the files: `.taskrc`, and the directory `.task` so that you can have them forever.
 
### Basic commands
* Create a task: `task add "Name of the task"`
* List the tasks and their IDs: `task`
* Mark a task done: `task ID done (IDs are 1, 2 3, ... etc)`
* Delete a task (including one that is done): `task ID delete`
* Modify a task name: `task ID modify "new and modified task description"`
* Add comments to already-existing task description (annotate): `task ID annotate "and another thing"`
* Add more info to a task: `task ID modify project:projectname due:duedate`
* Modify many tasks to add a common project name: `task ID1 ID2 ID3 modify project:projectname`
* Schedule a task to automatically disappear after a given time: `task 1 modify until:eoy`
* Schedule a task to automatically appear after a given time: `task 1 modify wait:30th`
* Modify (e.g. change tagnames) a set of tasks by some attribute (e.g. project) : `task project:projectname modify +tagname`

#### Print [next] tasks with specific attributes:
* print all tasks in the "prj" project: `task project:prj`
* print all tasks in the "prj" project and remove their tags: `task project:prj tag:`
* take all the tasks with "prj" project name and remove tag names and give them the tag name "newtag": `task project:prj tag: modify +newtag`
* print all tasks which are started: `task started (write "task reports" to see all possible options)`


### Best practices for a functional workflow 
This part is taken from [best practices](http://taskwarrior.org/docs/best-practices.html) suggested by the author.

* Assign a project to your tasks if possible:
```
task ID modify project:Home
```

* Assign due dates where appropriate, for the important tasks:
```
task ID modify due:31st
```

* When you start working on a task, mark it started:
```
task ID start
```

* If you know the priority of a task:
```
task ID modify priority:M
```

* Add useful tags to a task:
```
task ID modify +problem +house
```

* Add the special tag `+next` to a task, to boost its urgency:
```
task ID modify +next
```

* Represent dependencies, where appropriate, because there is a big difference in the urgency of a blocking task, than that of a blocked task:
```
task ID modify depends:OTHER_ID
```

* Try not to have large, long-term tasks that will sit on your list forever. It can be very satisfying and motivating to complete tasks, so create more, but smaller, tasks. 

### Adding due dates:

The rules for date and time format can be changed from `rc.dateformat` setting, but the default setting prints the date in the British format.

__Example:__

```
task add Open the store due:2015-01-31T08:30:00
task add Pay the rent due:eom
```

Here the synonym `eom` means 'end of the month'. Synonyms are a useful shortcut to entering lengthy dates. Here is the full set:

`now
today 	
sod 	
eod 	
yesterday
tomorrow
monday 
january
later 
someday
soy 	
eoy 	
soq 	
eoq 	
som 	
socm 	
eom
eoc
`

Here, `eo`=_end of_, `so`=_starting of_ (the next), `soc`=_starting of the current_, `d`=_day_, `w`= _week_, `m`=_month_, `y`=_year_, `q`=_quarter_ etc. See [here](http://taskwarrior.org/docs/dates.html) for more details.


The `rc.dateformat` setting in `taskrc` allows you to specify other formats for date input. It supports standard date and time formats (without the `%`).

### Recurring task
 A recurring task is a task with a due date that keeps coming back as a reminder. Here is an example:
```
task add Pay the rent due:1st recur:monthly until:2015-03-31
```

### Formatting the report
To get rid of unnecessary info that is displayed, [this page](http://taskwarrior.org/docs/verbosity.html)
 can be a lifesaver.
Here is what I found most useful.

Adding the line
`verbose=no`
to the file `.taskrc` will help you get rid of the footnote and header.

Here is an example of a custom report called "verybasic" which contains very specific columns that we want, in our desired order. Either add the following lines to `.taskrc` or add `task ` to the beginning of every line and run individually in terminal (both have the same effect):
```
report.verybasic.description='A list with very basic information, created by me.'
report.verybasic.columns=id,project,tags,description.count,due
report.verybasic.sort=start-,urgency-
report.verybasic.filter=status:pending
```
To make this report your default output report, add to your `.taskrc`:
```
default.command=verybasic
```
or, issue this command in terminal: `task config default.command 'verybasic'`

To see this custom report in action, just run `task verybasic`. Detailed documentation found [here](http://taskwarrior.org/docs/tutorials/report.html).

### Other useful commands
* To undo a change that you have made:
```
task undo
```

* Task warrior has a very good calendar display with useful info showing. Use
```
task calendar
```
You can combine more commands to generate desired output.

* You can use a task warrior front-end called `vit`. Compile from the AUR (on Arch). Alternatively, [here](https://github.com/scottkosty/vit) is the github.

### Syncing your tasks through a remote server and access it on Android

The website [freecinc](https://freecinc.com/) provides a service to host your tasks so that you do not need to set up your own server. To use this, simply log in to the website and follow their instruction. After you are done, in order to sync manually, run `task sync` in your client and done. To automate it, add this to your `crontab -e`:
```
# Syncing task warrior
3 */2 * * * task sync && notify-send "Syncing Tasks"
```
which sends out a little notification every time syncing is performed.

#### Mirakel (Caution: Outdated. Use [Task Warrior for Android](https://play.google.com/store/apps/details?id=kvj.taskw&hl=en_US) instead)
On Android, the app [Mirakel](https://mirakel.azapps.de/) (Caution: outdated) gives you a way to upload a specially created config file so that you can sync with your server (freecinc, in this case). Format of this config file:

```
username: foo
org: bar
user key: <your key here> 
server: localhost:6544
client.cert:
-----BEGIN CERTIFICATE-----
…
-----END CERTIFICATE-----
Client.key:
-----BEGIN RSA PRIVATE KEY-----
…
-----END RSA PRIVATE KEY-----
ca.cert:
-----BEGIN CERTIFICATE-----
…
-----END CERTIFICATE-----
```

Get your username, org and server from the line starting with `taskd.credentials=` in the file `~/.taskrc`. The format of that line is 
```
	taskd.credentials=org\/username\/user_key
```
Note that the org comes before the username. Get your server from the line staring with `taskd.server=`.
Finally, insert the contents of the file `*.cert.pem`, `*.key.pem`, `*.ca.key`.
Save it with any name and send it to the mobile phone so that you cam import it into Mirakel.


__Tips:__
 Use arithmetic operations in attributes:
```
 	task add newtask due:2days scheduled:due-1day
```


#### inthe.AM
My new favourite is [inthe.AM](https://inthe.am/). This one has a web front-end as well as a nice server. Works similarly. You have to login with your email.

To use Mirakel effectively, I use several UDAs which are defined in my `taskrc`.

#### Another Andriod App 
[Task Warrior for Andriod](https://play.google.com/store/apps/details?id=kvj.taskw&hl=en_US) is the most functional development so far, although it is a bit buggy at times.

### Process Management

It is easy to set up [Kanban](https://en.wikipedia.org/wiki/Kanban_(development)) or [GTD](https://en.wikipedia.org/wiki/Getting_Things_Done) with  Taskwarrior. There are many extensions. [Here](https://taskwarrior.org/tools/) is a whole list of tools developed around it. Here are a few.  

* [GTD with Taskwarrior](https://taskwarrior.org/news/news.20150627.html)
* [taskwarrior-kanban]( https://github.com/j-jith/taskwarrior-kanban)
* [Pomodoro with taskwarrior](https://github.com/coddingtonbear/taskwarrior-pomodoro)
