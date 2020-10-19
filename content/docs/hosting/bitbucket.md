---
title: Bitbucket
date: 2020-10-19T08:16:14.054Z
weight: 10
linktitle: ""
type: book
---
## create repo

Create first repo at bitbucket.org.
Then:

```bash
cd /path/to/my/repo
git remote add origin https://<username>@bitbucket.org/<username>/<reponame>.git
git push -u origin --all # pushes up the repo and its refs for the first time
git push origin --tags   # pushes up any tags
```

Nota: beware origin is in the form https://..., unlike what bitbucket indicates
by default. If I follow the default, but I also use a deployment key, I get 
error when pushing: 

```
conq: repository access denied. access via deployment key is read-only
fatal: Could not read from remote repository.
```

## Push (at each session)

```
git add .
git commit -m "..."
git push -u origin master
```

## Setting my development environment (once for all)

### SSL

To be noted, as outlined at [git-please-tell-me-who-you-are-error](http://stackoverflow.com/questions/11656761/git-please-tell-me-who-you-are-error)
there are two types of keys for bitbucket:

* deployment key, read-only (setup per repo)
* SSH key, read/write (setup in user account)

My keys are in `c:\Users\vaad7484\.ssh` (this is where it installed first by 
default), but then I had to copy to `u:\.ssh` (this is seen as `~\.ssh`), as
needed (by ?I forgot which step effectively requires this, but it definitely 
does. I think it is linked to setting up my environment to work with bitbucket).
=> I found out that reason why there are two places is:

* when I run as administrator $HOME == c:\Users\vaad7484
* otherwise $HOME == u:\

I need to launch git bash to initialize the ssh agent.

To make sure ssh is effectively up, 

```
$ ssh-add -l
```

should respond something like:

```
4096 SHA256:qbLf0A/w... /u//.ssh/id_rsa (RSA)
```

<https://confluence.atlassian.com/bitbucket/set-up-ssh-for-git-728138079.html>

To be noted that the private key ends up in Heroku (environment variable), but 
it is in fact a base64 version of the key.
=> To do so, I need to add a GIT_SSH_KEY to my heroku project (e.g. via the dashboard)
populated with my private key
LS0tLS1\*\*\*\*LQ0K

**NOTA**: it seems my id_rsa is 
for readonly, while id_rsa2 allows write in bitbucket (e.g. git push)

### Bitbucket

### Heroku

### Binding heroku to bitbucket

As per: <http://fiznool.com/blog/2015/05/20/an-alternative-to-npm-private-modules/>

Another good reading was http://stackoverflow.com/questions/10869796/npm-private-git-module-on-heroku

Those screenshots re-assured as to what to copy for the public key https://confluence.atlassian.com/bitbucket/add-an-ssh-key-to-an-account-302811853.html

Note:

* `deploy_key` is in fact `id_rsa`
* the ssh url for a given repo can be copied directly in bitbucket web interface
* obvious (but I first failed to do it), the imported repo hosted in Bitbucket must have a `package.json`file.
* my private & public keys are stored locally at C:\Users\vaad7484.ssh\