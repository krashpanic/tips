
#How to manage multiple git accounts :



* Create a key pair for your Pivotal email address you use in github.com

```
ssh-keygen -t rsa -b 4096 -C "<your pivotal email id>"
Generating public/private rsa key pair.
Enter file in which to save the key (/Users/nsuvarna/.ssh/id_rsa):
/Users/johndoe/.ssh/id_rsa_pivotal
```
* Copy to clipboard

```
 pbcopy < ~/.ssh/id_rsa_pivotal.pub
```

* Add the key to github settings :

https://help.github.com/articles/adding-a-new-ssh-key-to-your-github-account/

* Create a key pair for your  email address you use for your personal github repo

```
ssh-keygen -t rsa -b 4096 -C "<your pivotal email id>"
Generating public/private rsa key pair.
Enter file in which to save the key (/Users/nsuvarna/.ssh/id_rsa):
/Users/johndoe/.ssh/id_rsa_personal
```

```
cat ~/.ssh/config

Host pivotal
 Hostname github.com
 User git
 IdentityFile ~/.ssh/id_rsa_pivotal
 PubkeyAuthentication yes
Host personal
 Hostname github.com
 User git
 IdentityFile ~/.ssh/id_rsa_personal
 PubkeyAuthentication yes
```

* Clear out currently stored identities

```
ssh-add -D
```

* Add in personal key (you may be prompted for your keypairs password)

```
ssh-add ~./ssh/id_rsa_personal
```
 
* And work

```
ssh-add ~./ssh/id_rsa_pivotal
```

* Print a list of loaded keys to make sure both are loaded

```
ssh-add -l
```

* Now you’ve got your keys in place, let’s poke github and see if it recognizes us

```
ssh -T pivotal


Warning: Permanently added the RSA host key for IP address '192.30.252.130' to the list of known hosts.
Hi nikhilsuvarna! You've successfully authenticated, but GitHub does not provide shell access.
```

```
ssh -T <personal>

Hi johndoe! You've successfully authenticated, but GitHub does not provide shell access.
```

```
git config --global -l

user.name=johndoe
user.email=johndoe@gmail.com
credential.helper=osxkeychain
filter.lfs.clean=git lfs clean %f
filter.lfs.smudge=git lfs smudge %f
filter.lfs.required=true
```

* Getting your pivotal code from github :

Normally you’d go to the github project site and grab the clone URL and be off to the races.

Something like

```
 git clone ssh://pivotal/pivotal-cf/GSS-troubleshooting.git

```
```
git config --local -l
```
```
  git config --local user.name "Nikhil Suvarna"
  git config --local user.email "nsuvarna@pivotal.io"
  git config --local github.username "nikhilsuvarna"
```

* Generate token : https://help.github.com/articles/creating-an-access-token-for-command-line-use/


```
 git config --local github.token "036c0ca0283355698fda7e94a60eb4f9172c8054"
 ```
