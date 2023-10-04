# Activate venv with one-word command

## Usage

Run `vv` anywhere down the directories hierarchy where there a venv around.

```sh
~ $ cd Projects/Superproject/Source/backend/
backend $ vv
Activated: /Users/Anatoly/Projects/Superproject/venv/bin/activate
(venv) backend $ ./manage.py runserver
...
```



## Installation

Add this to your `~/.bashrc` or `~/.zshrc`:


```sh
function vv {
    D=`pwd`
    local FILE="venv/bin/activate"

    while [[ "$PWD" != "/" ]]
    do
        if [ -f $FILE ];
        then
            source $FILE
            echo "Activated: `pwd`/$FILE"
            cd $D
            return
        fi
        cd ..
    done
    echo "$FILE not found"
    cd $D
    return
}
```


Or add this to your `~/.config/fish/config.fish`:

```fish
function vv
    set -l D (pwd)
    set -l FILE "venv/bin/activate.fish"

    while test "$PWD" != "/"
        if test -f $FILE
            source $FILE
            echo "Activated: "(pwd)/$FILE
            cd $D
            return
        end
        cd ..
    end
    echo "$FILE not found"
    cd $D
end
```
