# vifm
## shell
### setup
#### colours
    rm -rf ~/.config/vifm/colors
    git clone https://github.com/vifm/vifm-colors ~/.config/vifm/colors
    //update
        cd ~/.config/vifm/colors
        git pull
    //set
        vim ~/.config/vifm/vifmrc
        //go to line 67, (or for vim /\<colorscheme\> )
        colorscheme [theme-name]
#### set settings for all users
    /usr/share/vifm/vifmrc - edit vifm settings

## keys     
### basic

cw - rename a file or files.

o - change file owner.                        

cg - change file group.                        

ga - calculate directory size

za - Toggle showing hidden files

zo - Show hidden files

zm - Hide hidden files			

gu, u - make names of selected files lowercase.

gU, U - make names of selected files uppercase.

s - open shell with current pwd

mx - create mark x
    m[a-z][A-Z][0-9]

'x - jump to mark x
    '[a-z][A-Z][0-9]
### panes
Ctrl-W h - switch to left pane (vifm-CTRL-W_h), Ctrl-W j - switch to pane below

Ctrl-W k - switch to pane above, Ctrl-W l - switch to right pane

Ctrl-W p - switch to previous window, Ctrl-W w - switch to other pane

Ctrl-W o - leave only one pane

Ctrl-W s - split window horizontally, Ctrl-W v - split window vertically
### change mode
ex - :ex
- visual

    :visual

    v
- preview

    :view

    w

### basic cmds

    :mkdir :copy :move

- show mountable drives

    :media

- copy pain path to unselected pain

    :sync

- run graphical program but keep vifm running

    :! [programToRunWith] [fileName] &
