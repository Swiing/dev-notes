---
title: Heroku
date: 2020-10-18T00:00:00+01:00
weight: 2
linktitle: Heroku
type: book
---
## Setting my windows local environment (at each session)

As per setup.bat, first thing I need to

```bash
$ set HOME=%USERPROFILE%
```

for heroku to run in bash (nota: not needed in git-bash).

## Creating new app

Assuming I have created first the app via the web interface (or `heroku create`)

```
$ git init
$ heroku git:remote -a thawing-bayou-62881
```

## Push (at each session)

```
git add .
git commit -m "..."
git push heroku master
```

## Removing Heroku caches (e.g. in node_modules/)

```bash
heroku config:set NODE_MODULES_CACHE=false
git commit -am 'disable node_modules cache' --allow-empty
git push heroku master
heroku config:unset NODE_MODULES_CACHE
```

More: https://devcenter.heroku.com/articles/nodejs-support#cache-behavior

## Useful commands

```bash
heroku login
heroku run bash
heroku local -f Procfile.local # to run locally the app
```

Nota on `heroku run bash`: it does not visibility on the file system as possibly
modified by the app (see http://qaoverflow.com/question/image-change-but-cannot-
see-it-in-herokus-folder/).

## Heroku asking for login/password

<https://stackoverflow.com/questions/27810419/git-push-heroku-master-is-still-asking-for-authentication>
```bash
username : blank
password : heroku auth token
```
where the auth token can be retrieved by 
```bash
$ heroku auth:token
```

## panic: mkdir U:.config: Cannot create a file when that file already exists.

This happens in user (not administrator) role. Solution is to change the home working directory:

```bash
$ export HOME=/c/cygwin64/home/vaad7484
```

## Ce programme est bloqu▒ par une strat▒gie de groupe.

Occurs e.g. when trying to run 

```bash
$ heroku git:clone -a lpp-static
```

however, heroku command is unknown in administrator role. Solution is to check the location:

```bash
$ type -a heroku
```

And then run full path in adminisatrator role, e.g.:

```bash
$ /c/"Program Files (x86)"/Heroku/bin/heroku git:clone -a lpp-static
```

(note the double quotes in the path to take into account the spaces)