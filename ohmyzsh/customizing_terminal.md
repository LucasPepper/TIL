# Customizing the Terminal using zsh
[Getting zsh](https://github.com/ohmyzsh/ohmyzsh)

[new-line](https://medium.com/@renan.garcia/como-ter-um-terminal-mais-produtivo-e-cool-no-linux-8224d771a26)

Edit the *~/.oh-my-zsh/themes/agnoster.zsh-theme* file with your favorite editor, like this:
```
$ nano ~/.oh-my-zsh/themes/agnoster.zsh-theme
```
Add this function on the code:

```
prompt_newline() {
  if [[ -n $CURRENT_BG ]]; then
    echo -n "%{%k%F{$CURRENT_BG}%}$SEGMENT_SEPARATOR
%{%k%F{blue}%}$SEGMENT_SEPARATOR"
  else
    echo -n "%{%k%}"
  fi

  echo -n "%{%f%}"
  CURRENT_BG=''
}
```
Finally, add *prompt_newline* in build_prompt, as following:

```
## Main prompt
build_prompt() {
  RETVAL=$?
  prompt_status
  prompt_virtualenv
  prompt_context
  prompt_dir
  prompt_git
  prompt_bzr
  prompt_hg
  prompt_newline
  prompt_end
}
```
