Add the following config to the bottom of your `~/.bashrc` file. I think the following config has to come after the configs that are listed earlier in the `.bashrc` file that reference the `PS1` variable. I think as long as the following config is listed after those already-existing configs, then you should see your git branch just fine.

For more information and ideas search for "customize bash prompt".

```
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

# Special Characters: https://www.gnu.org/savannah-checkouts/gnu/bash/manual/bash.html#Controlling-the-Prompt
FILE_PATH="\w" # Path to current working directory.

# Color and formatting reference: https://misc.flogisoft.com/bash/tip_colors_and_formatting
RESET="\e[0m"
BOLD="\e[1m"
BLACK_FG="\e[30m"
BLACK_BG="\e[40m"
WHITE_FG="\e[97m"
WHITE_BG="\e[107m"
RED_FG="\e[31m"
RED_BG="\e[41m"
GREEN_FG="\e[32m"
GREEN_BG="\e[42m"
BLUE_FG="\e[34m"
BLUE_BG="\e[44m"
CYAN_FG="\e[36m"
CYAN_BG="\e[46m"
LIGHT_GRAY_FG="\e[37m"
LIGHT_GRAY_BG="\e[47m"

# Comment out to use non-formatted prompt.
use_formatted_prompt=yes

if [ "$use_formatted_prompt" = yes ]; then
  # white foreground, black background
  PS1="${BOLD}${WHITE_FG}${BLACK_BG}${FILE_PATH} $(parse_git_branch)$ ${RESET} "
  # black foreground, white background
  # PS1="${BOLD}${BLACK_FG}${WHITE_BG}${FILE_PATH} $(parse_git_branch)$ ${RESET} "

  # Examples showing different colors and formats:
  # PS1="${BOLD}${WHITE_FG}${GREEN_BG}${FILE_PATH} ${BLUE_BG} $(parse_git_branch)${BLACK_FG}${LIGHT_GRAY_BG} $ ${RESET} "
  # PS1="${RED_FG}${WHITE_BG}${FILE_PATH}${RESET} ${CYAN_FG}$(parse_git_branch)${RESET}$ "
else
  PS1='\w $(parse_git_branch)$ '
fi
```
