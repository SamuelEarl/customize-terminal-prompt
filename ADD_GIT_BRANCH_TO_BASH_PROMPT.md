Add the following config to the bottom of your `~/.bashrc` file. I think the following config has to come after the configs that are listed earlier in the `.bashrc` file that reference the `PS1` variable. I think as long as the following config is listed after those already-existing configs, then you should see your git branch just fine.

For more information and ideas search for "customize bash prompt".

**Advanced Version:**

```
#######################################
# START: Add git branch to bash prompt
#######################################
# Add git branch, if it's present, to PS1.
parse_git_branch() {
  GIT_BRANCH="$(git branch 2> /dev/null | sed -e '/^[^*]/d' -e 's/* \(.*\)/(\1)/')"
  # printf "$GIT_BRANCH"
  # If the previous command returns an empty string (i.e. there is no git branch in the current directory),
  # then return that empty string. This will leave the git branch empty in the command prompt.
  if [ -z "$GIT_BRANCH" ]; then
    echo "$GIT_BRANCH"
  # Otherwise, return the git branch with a space after it so there is
  # separation between the file path and the git branch in the bash prompt.
  else
    echo "$GIT_BRANCH "
  fi
}
# Uncomment to use color prompt.
# color_prompt=yes
if [ "$color_prompt" = yes ]; then
  PS1='\[\e[1;34m\]\w \[\e[1;32m\]$(parse_git_branch)\[\e[0m\]$ '
else
  PS1='\w $(parse_git_branch)$ '
fi
unset color_prompt force_color_prompt

# Special Characters: https://www.gnu.org/savannah-checkouts/gnu/bash/manual/bash.html#Controlling-the-Prompt
# \w = Path to current working directory

# Color and formatting reference: https://misc.flogisoft.com/bash/tip_colors_and_formatting
# \e[0m  = reset
# \e[1m  = bold
# \e[30m = black foreground
# \e[31m = red foreground
# \e[32m = green foreground
# \e[34m = blue foreground
#######################################
# END: Add git branch to bash prompt
#######################################
```

---

**Simpler Version:**

```
# Add git branch, if it's present, to PS1.
parse_git_branch() {
  git branch 2> /dev/null | sed -e '/^[^*]/d' -e 's/* \(.*\)/(\1)/'
}
if [ "$color_prompt" = yes ]; then
  PS1='\[\033[01;34m\]\w\[\033[01;31m\]$(parse_git_branch)\[\033[00m\]\$ '
else
  PS1='\w$(parse_git_branch)\$ '
fi
unset color_prompt force_color_prompt
```