## What is the .bashrc File in Linux?

The .bashrc file is a bash shell configuration file.

This is how a .bashrc file looks when opened with a text editor. This file is used to initialise the interactive terminal session on your system. A detailed look into the contents will show you all the configurations for your interactive bash shell session. Let’s see how can we take advantage of the .bashrc file on our system.

## What is the use of the .bashrc file?

The most common use of the .bashrc file is to set up custom environment variables for different users. It helps a user set up their preferences for the bash shell.

Being a shell script, the .bashrc file can be used to do virtually anything that a user is allowed to do.

Being invoked as soon as the bash shell is opened in the interactive mode, the .bashrc file can be used to set up custom commands for your personal use.

Further, you can set up aliases for your bash session. It can limit the length of shell history as well. Essentially, by editing the .bashrc file using any text editor, a user can set system parameters and create environment variables in a way where their customizations will be available in every future session.

## What is the .bash_profile file in Linux?

The .bash_profile file is another bash shell script file which we can see as a config file. It is stored at ~/.bash_profile.

However, unlike the .bashrc file, it gets executed every time a user logs into a system.

In simple words, it is invoked when you enter your username and password to log in on your Linux system. This login can be both local or remote. It is different from a regular bash shell invocation and is seen as a login shell mode session.

Like we discussed earlier, the dot signifies that this is a hidden file. It contains a set of data which defines all the configurations for the current login shell for the user. These configurations include setting up or editing things like the environment variables, shell history, completion, command aliases among others. Each user has their own .bash_profile file which stores all the configurations for the particular user. Whenever we create a new user on our system, Linux will generate a new default .bash_profile file for it.

This is how a .bash_profile file looks when opened with a text editor. This file is used to initialise the current user session on your system. A detailed look into the contents will show you all the configurations for your bash login shell session. Let’s see how can we take advantage of the .bash_profile file on our system.

## What can we do with the .bash_profile file?

The most common use of the .bash_profile file is to set up custom environment variables for different users. In practice, the usage of the .bash_profile file is the same as the usage for the .bashrc file. Most .bash_profile files call the .bashrc file for the user by default. Then why do we have two different configuration files? Why can’t we do everything using a single file?

Well, the short answer is freedom and convenience. The longer answer is as follows: Suppose, You wish to run a system diagnostic every time you log in to your Linux system. You can edit the configuration file to print the results or save it in a file. But you only wish to see it at startup and not every time you open your terminal. This is when you need to use the .bash_profile file instead of .bashrc
