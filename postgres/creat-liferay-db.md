## Creare un nuovo database postgresql per liferay



Creazione utente

```bash
createuser [username]
```

Impstazione password utente

```bash
alter user [username] with encriypted password '[password]'
```

Creazione di un nuovo database

```sql
postgres=> CREATE DATABASE [database] ENCODING 'UTF8';
```

Grant dei permessi dell'utente

```sql
postgres=> GRANT ALL PRIVILEGES ON DATABASE [database] TO [username];	
```

