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
    echo ""
    cd $D
    read -r -p "$FILE not found, do you want to create venv? [y/N]" ans
    if [[ "ans" =~ ^[Yy]$ ]]; then
        if python3 -m venv venv; then
            source $FILE
            echo "$FILE was created and activated"
            return 0
        else
            echo "Not sucsecfully"
            return 1
        fi
    fi
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
    cd $D
    read -r -p "$FILE not found, do you want to create venv? [y/N]" ans
    switch %ans
        case y Y
            if python3 -m venv venv; then
                source $FILE
                echo "$FILE was created and activated"
                return 0
            else
                echo "Not sucsecfully"
                return 1
            end
        case '*'
            return 1
    end
end
```
