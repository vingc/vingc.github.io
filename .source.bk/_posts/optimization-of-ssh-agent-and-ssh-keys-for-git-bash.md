---
title: optimization of ssh-agent and ssh-add for git bash
date: 2017-03-05 23:18:41
tags: git-bash ssh-agent ssh-add
categories: technology
---



------



#### Background

Several days ago, To use github, i installed git in my new laptop for the first time, and encountered a problem about management of ssh-agent and ssh keys.

After starting a new "git bash" terminal, there was something wrong when pushed my new commit, see below picture:

![error](/images/ssh_error.png)

 

when used command "ssh-add -l" to check the private keys added, it returned an error, the key error message "Could not open a connection to your authentication agent" .



#### Resolution

After google, realized that "git bash" needs us to start the "ssh-agent" process before "ssh-add" and "git" command using ssh protocol. 

[resolution in StackOverFlow](http://stackoverflow.com/questions/17846529/could-not-open-a-connection-to-your-authentication-agent/10077302#10077302)

Sure, we can fix it manually, but why "git bash" doesn't start "ssh-agent" itself when the terminal launched？as we all know we always need it.

Now, lay the question aside firstly, i wanted to let git work elegantly.

Do we execute commands "eval \`ssh-agent -s\`" and "ssh-add ~/.ssh/github_rsa" every time when launch a "git bash" terminal?

 No, of course not, i can't bear this trouble, as a engineer who develops software to make life easier.

we can follow the "good" [tutorial](http://anterence.blogspot.com/2012/01/ssh-agent-in-msysgit.html) to let "git bash" start "ssh-agent" itself by appending the commands to the configuration file "$git_installed_directory/etc/bash.bashrc".

Have we done?

Ha, haven't, it's a good resolution, but not the best.

I tested the resolution by opening several "git bash" terminals at the same time, see the picture:

![multiple processes](/images/dup_ssh_processes.png)



There would be multiple processes if we opened several "git bash" terminals, each process per time.

This was not elegant. I couldn't bear this resolution too. I wanted to optimize it.



#### Final

New resolution:  check whether the ssh-agent has been started, it's dependent on the result to execute commands or not.

here is the code:

~~~shell
#start ssh-agent and add keys
SERVICE='ssh-agent'

if ps -ef|grep -u $SERVICE >/dev/null   #check whether the process started by current user exists 
then
   echo $SERVICE running.
else
   echo $SERVICE not running.
   ssh-agent > ~/.ssh/agent_env  #start the process,and dump the environment variables
   ssh-add ~/.ssh/github_rsa     #just for once,replace 'github_rsa' with your private key
fi
. ~/.ssh/agent_env   #export the environment variables
~~~

Add these lines into the end of the configuration file "$git_installed_directory/etc/bash.bashrc".

Things have been finished, although still had questions here.

* why do we need to add key each time when "ssh-agent" started? 
* where is it stored? Don't need to add it every time if keep it stored durably. 

Less procedure, launch faster. I will figure out.



#### ------2017-03-06------

continue...

I think the private key identities is stored in memory of ssh-agent process space, so when stop the process, the data would be lost, and don't need further tuning after trading off.



#### appendix

* [More information about ssh-add](https://www.freebsd.org/cgi/man.cgi?query=ssh-add&sektion=1)

