## Django installation (from the [Django Girls tutorial](https://tutorial.djangogirls.org/))

make a venv called `myvenv` in cd
```bash
python3 -m venv myvenv
```

start the venv
```bash
source myvenv/bin/activate
```

install pip
```bash
python -m pip install --upgrade pip
```

make a requirements.txt in cd
> Django~=2.2.4

install packages
```bash
pip install -r requirements.txt
```

## Set-up

create a project

```bash
django-admin startproject mysite .
```

migrate (update) changes
```bash
python manage.py migrate
```

run server
```bash
python manage.py runserver
```
