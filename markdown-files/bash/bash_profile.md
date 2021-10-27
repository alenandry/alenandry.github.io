Apart from having a home directory to create and store files, users need an environment that gives them access to the tools and resources. When a user logs in to a system, the user’s work environment is determined by the initialization files. These initialization files are defined by the user’s startup shell, which can vary depending on the release. The default initialization files in your home directory enable you to customize your working environment.

Below are Various Initialization file for Bash Shell

-   The  **/etc/profile** file is a systemwide file that the system administrator maintains. This file defines tasks that the shell executes for every user who logs in. The instructions in the file usually set the shell variables, such as PATH, USER, and HOSTNAME.
-   The  **~/.bash_profile** file is a configuration file for configuring user environments. The users can modify the default settings and add any extra configurations in it.
-   The  **~/.bash_login** file contains specific settings that are executed when a user logs in to the system.
-   The file is yet another configuration file that is read in the absence of the ~/.bash_profile and ~/.bash_login files.
-   The  **~/.bash_logout** file contains instructions for the logout procedure.

## Configuring the .bash_profile File

The .bash_profile file is a personal initialization file for configuring the user environment. The file is defined in your home directory and can be used for the following:

- Modifying your working environment by setting custom environment variables and terminal settings

- Instructing the system to initiate applications

  ## Bash Profile

  ```js
  
  [[ $- != *i* ]] && return
  
  colors() {
  	local fgc bgc vals seq0
  
  	printf "Color escapes are %s\n" '\e[${value};...;${value}m'
  	printf "Values 30..37 are \e[33mforeground colors\e[m\n"
  	printf "Values 40..47 are \e[43mbackground colors\e[m\n"
  	printf "Value  1 gives a  \e[1mbold-faced look\e[m\n\n"
  
  	# foreground colors
  	for fgc in {30..37}; do
  		# background colors
  		for bgc in {40..47}; do
  			fgc=${fgc#37} # white
  			bgc=${bgc#40} # black
  
  			vals="${fgc:+$fgc;}${bgc}"
  			vals=${vals%%;}
  
  			seq0="${vals:+\e[${vals}m}"
  			printf "  %-9s" "${seq0:-(default)}"
  			printf " ${seq0}TEXT\e[m"
  			printf " \e[${vals:+${vals+$vals;}}1mBOLD\e[m"
  		done
  		echo; echo
  	done
  }
  
  [ -r /usr/share/bash-completion/bash_completion ] && . /usr/share/bash-completion/bash_completion
  
  # Change the window title of X terminals
  case ${TERM} in
  	xterm*|rxvt*|Eterm*|aterm|kterm|gnome*|interix|konsole*)
  		PROMPT_COMMAND='echo -ne "\033]0;${USER}@${HOSTNAME%%.*}:${PWD/#$HOME/\~}\007"'
  		;;
  	screen*)
  		PROMPT_COMMAND='echo -ne "\033_${USER}@${HOSTNAME%%.*}:${PWD/#$HOME/\~}\033\\"'
  		;;
  esac
  
  use_color=true
  
  # Set colorful PS1 only on colorful terminals.
  # dircolors --print-database uses its own built-in database
  # instead of using /etc/DIR_COLORS.  Try to use the external file
  # first to take advantage of user additions.  Use internal bash
  # globbing instead of external grep binary.
  safe_term=${TERM//[^[:alnum:]]/?}   # sanitize TERM
  match_lhs=""
  [[ -f ~/.dir_colors   ]] && match_lhs="${match_lhs}$(<~/.dir_colors)"
  [[ -f /etc/DIR_COLORS ]] && match_lhs="${match_lhs}$(</etc/DIR_COLORS)"
  [[ -z ${match_lhs}    ]] \
  	&& type -P dircolors >/dev/null \
  	&& match_lhs=$(dircolors --print-database)
  [[ $'\n'${match_lhs} == *$'\n'"TERM "${safe_term}* ]] && use_color=true
  
  if ${use_color} ; then
  	# Enable colors for ls, etc.  Prefer ~/.dir_colors #64489
  	if type -P dircolors >/dev/null ; then
  		if [[ -f ~/.dir_colors ]] ; then
  			eval $(dircolors -b ~/.dir_colors)
  		elif [[ -f /etc/DIR_COLORS ]] ; then
  			eval $(dircolors -b /etc/DIR_COLORS)
  		fi
  	fi
  
  	if [[ ${EUID} == 0 ]] ; then
  		PS1='\[\033[01;31m\][\h\[\033[01;36m\] \W\[\033[01;31m\]]\$\[\033[00m\] '
  	else
  		PS1='\[\033[01;32m\][\u@\h\[\033[01;37m\] \W\[\033[01;32m\]]\$\[\033[00m\] '
  	fi
  
  	alias ls='ls --color=auto'
  	alias grep='grep --colour=auto'
  	alias egrep='egrep --colour=auto'
  	alias fgrep='fgrep --colour=auto'
  else
  	if [[ ${EUID} == 0 ]] ; then
  		# show root@ when we don't have colors
  		PS1='\u@\h \W \$ '
  	else
  		PS1='\u@\h \w \$ '
  	fi
  fi
  
  unset use_color safe_term match_lhs sh
  
  alias cp="cp -i"                          # confirm before overwriting something
  alias df='df -h'                          # human-readable sizes
  alias free='free -m'                      # show sizes in MB
  alias np='nano -w PKGBUILD'
  alias more=less
  
  xhost +local:root > /dev/null 2>&1
  
  complete -cf sudo
  
  # Bash won't get SIGWINCH if another process is in the foreground.
  # Enable checkwinsize so that bash will check the terminal size when
  # it regains control.  #65623
  # http://cnswww.cns.cwru.edu/~chet/bash/FAQ (E11)
  shopt -s checkwinsize
  
  shopt -s expand_aliases
  
  # export QT_SELECT=4
  
  # Enable history appending instead of overwriting.  #139609
  shopt -s histappend
  
  #
  # # ex - archive extractor
  # # usage: ex <file>
  ex ()
  {
    if [ -f $1 ] ; then
      case $1 in
        *.tar.bz2)   tar xjf $1   ;;
        *.tar.gz)    tar xzf $1   ;;
        *.bz2)       bunzip2 $1   ;;
        *.rar)       unrar x $1     ;;
        *.gz)        gunzip $1    ;;
        *.tar)       tar xf $1    ;;
        *.tbz2)      tar xjf $1   ;;
        *.tgz)       tar xzf $1   ;;
        *.zip)       unzip $1     ;;
        *.Z)         uncompress $1;;
        *.7z)        7z x $1      ;;
        *)           echo "'$1' cannot be extracted via ex()" ;;
      esac
    else
      echo "'$1' is not a valid file"
    fi
  }
  # source "$HOME/.cargo/env"
  # source /opt/anaconda/bin/activate google
  
  
  #yay绑定powerpill 命令改为yiy
  # Downgrade permissions as AUR helpers expect to be run as a non-root user. $UID is read-only in {ba,z}sh.
  # alias yay="sudo -u alen /usr/bin/yay --pacman powerpill"
  # alias yiy=yay  # For convenience
  source /usr/share/nvm/init-nvm.sh
  alias run_java="bash /home/alen/code/java_code/run_java.sh"
  
  
  export PATH=/home/alen/.cargo/bin:$PATH
  
  ```

  