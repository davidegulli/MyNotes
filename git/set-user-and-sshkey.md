## Setup user and Ssh Key



#### Setup user credential

```bash
git config --local --add user.name "Davide Gulli"
git config --local --add user.email "davide.gulli@gmail.com"
git config --local --add credential.username "davide.gulli@gmail.com"
```



Per modificare l'author del un commit appena esegui

```bash
git commit --amend --reset-author
```



#### Setup ssh key

Impostando la chiave ssh non sarà più necessario inserire la password per eseguire le azioni che richiedono l'autenticaziane da parte dell'utente.



##### Generate ssh keys

```bash
ssh-keygen -t rsa -b 4096 -C "davide.gulli@gmail.com" -f ~/.ssh/rsa_dg_gmail
```



Per evitare di dover inserire la passphrase della ssh key ogni qual volta venga utilizzata, è possibile configurare il ssh agent.

```bash
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/rsa_dg_gmail
```



##### Github:

https://help.github.com/articles/adding-a-new-ssh-key-to-your-github-account/



##### Gitlab:

https://docs.gitlab.com/ce/ssh/README.html



##### Store Credential

``` bash
git config credential.helper store
git push http://example.com/repo.git
Username: <type your username>
Password: <type your password>
```

https://stackoverflow.com/questions/11403407/git-asks-for-username-every-time-i-push











