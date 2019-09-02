## Creare un nuovo database postgresql per liferay



Creazione utente

```bash
createuser [username]
```

Impstazione password utente

```bash
alter user [username] with encriypted password '[password]'
```

Oppure:

```bash
postgres=# create user myuser with encrypted password 'mypass';
```





Creazione di un nuovo database

```bash
postgres=# CREATE DATABASE [database] ENCODING 'UTF8';
```

Grant dei permessi dell'utente

```bash
postgres=# GRANT ALL PRIVILEGES ON DATABASE [database] TO [username];	
```

