# Activate venv with one-word command

## Usage

Run `vvv` anywhere down the directories hierarchy where there a venv around.

```sh
~ $ cd Projects/Superproject/Source/backend/
backend $ vvv
Activated: /Users/Anatoly/Projects/Superproject/venv/bin/activate
(venv) backend $ ./manage.py runserver
...
```



## Installation

Add this to your `~/.bashrc` or `~/.zshrc`:


```sh
function vvv {
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
