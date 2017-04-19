
# Creating a user account

First let's go over why you need a seperate user for running a webservice backend.


1. Don't run the risk of an incorrect script messing up entire system as possible with.
2. You can create your systemd service as a user service and thus have a much better unit organization.
3. No pesky permission problems with either MAC or DAC models. (Linux has both if you are not aware.)
4. Self contained environment where everything related to running the service can be easily found, instead of scattered all over the system.


Why not root? root account is meant for use as an administrative acccount, not an every day account. It's really dangerous and pretty much everything root touches is absolutely destroyed as far as permissions are concerned. Like it leads to intresting situations where a normal user can't even access their own home folder!

Okay so why not a user account for all of services on the server? 
Well other than the organizational benefits and modularity gains the thing is in production you should never run more than one app on a server, and then only one instance. Yes it is more effictions from both a resource and money POV to create additional isolated servers for each app instance. Or scaling up an instance.
As in selecting a higher end VPS with more CPU and RAM.



# So how do we do this thing?
Well first of all let's establish our goals and clearly describe what we want to achieve.

We want a user that can: 

1. Use ruby via rbenv and have latest available as default.
2. Use node via nvm and have latest available as deault.
3. start and create services.
4. Services should persist after user exits.
5. User should not be allowed to login via password.
6. User should specify authorized keys to allow ssh login.


We assume python is globally installed.


So let's create our user. For our example we will assume the user in named `taskarabia`

`useradd taskarabia` creates the user. At first the user does not have a password. We do not need to create a password as no password is valid and having it as none simply disables password login option. Which is what we want. Note that by default each user belongs to a group of the same name.

Second we need to add our authorized keys.
As root do

1. `su - taskarabia`
2. `mkdir ~/.ssh`
3. `exit`
4. `cp ~/.ssh/authorized_keys ~taskarabia/.ssh/`
5. `chown taskarabia:taskarabia ~taskarabia/.ssh/authorized_keys`
6. `su - taskarabia`
7. `chmod 700 .ssh`
6. `chmod a+r .ssh/authorized_keys`
7. `exit`

Now ssh as taskarabia user to complete the rest of the steps.

Next we install rbenv and nvm, you can [check here](../languages/README.md) for instructions on how.

And thats it. 
Oh one more thing. If you want sudo just do as root.

`usermod -a -G wheel taskarabia`

Oh actually that won't work as that way sudo will require a password and our user doesn't have a password remember? so what now?

Steps

1. Create a user group whose members won't require password for sudo.
2. Modify sudoers file for that behavior.

as root add group via `groupadd nopasswheel`

add your user to that group `usermod -aG nopasswheel taskarabia`.

Then as root edit the file `/etc/sudoers`  and add this at the end of the file `%nopasswheel ALL=(ALL) NOPASSWD: ALL`.

Relogin with taskarabia user if applicable and you are now a sudoer.
