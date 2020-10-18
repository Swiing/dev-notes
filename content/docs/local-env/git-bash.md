---
title: git-bash
date: 2020-10-18T00:00:00+01:00
weight: 2
linktitle: git-bash
type: book
---
# Using Git bash

In non-administrator role, $HOME is set to the U: drive. To solve this:
```bash
export HOME=/c/Users/vaad7484
```
I can check with echo $HOME.
Source: https://stackoverflow.com/questions/14774159/git-warning-unable-to-access-p-gitconfig-invalid-argument

Also:
```bash
cd /c/
```

## setting up the SSH key

At times, git-bash does not seem to execute the setup of ssh by default.
This will result in e.g. npm install fail with:
```bash
Permission denied (publickey).
```
It seems this happens when the window runs with administrator privileges
(since the ssh I have does not belong to the administration profile, but
to vaad7484 profile). I can open a new git-bash without administrator rights.

In case it would still not work, I need to add my key manually:
```bash
ssh-add ~/.ssh/id_rsa
```
Note: if I run as administrator, then I should use the path `~/../vaad7484/.ssh/id_rsa`
or simply `/c/Users/vaad7484/.ssh/id_rsa`
If I get the error:
```bash
Could not open a connection to your authentication agent.
```
I need to start the ssh-agent first:
```bash
eval `ssh-agent -s`
```
Cf. https://stackoverflow.com/questions/17846529/could-not-open-a-connection-to-your-authentication-agent

## Using git in git-bash
I am sometimes logged as administrator, sometimes as vaad7484 and this seems to
confuse git at times:
```bash
fatal: Unable to create 'C:/cygwin64/home/vaad7484/bitbucket/parser/.git/index.lock': Permission denied
```
Solution is to use the other account.