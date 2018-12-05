## How to access to PSQL console

Attraverso l'installazione standard di postgres, in automatico viene creato un utente specifico sul sistema operativo: *postgres* 

Ed a seconda delle configurazioni presenti nel file: *pg_hba.conf* si possono avere diverse modalità di accesso ai database.

Di default è impostata la modalità indent, la quale utilizza l'utente del sistema operativo per tentare l'accesso alla basedati postgres,  quindi una volta effettuato il login con un utente adeguato è possibile accedere come segue:

```bash
$sudo su - postgres
$psql
```



Per modificare tale modalità di accesso e passare a quella calssica, usando *username* e *password* è necessario modificare il file: */var/lib/pgsql/11/data/pg_hba.conf* sostituendo la modalità *indent* con la modalità *md5* se si utilizzano password criptate altrimenti *password*

```bash
# TYPE  DATABASE        USER            ADDRESS                 METHOD

# "local" is for Unix domain socket connections only
local   all             all                                     md5
# IPv4 local connections:
host    all             all             127.0.0.1/32            md5
# IPv6 local connections:
host    all             all             ::1/128                 md5
# Allow replication connections from localhost, by a user with the
# replication privilege.
local   replication     all                                     md5
host    replication     all             127.0.0.1/32            md5
host    replication     all             ::1/128                 md5

```

Una volta effettuate queste modifiche è possibile eseguire l'accesso come segue:

```bash
psql --username [username] --password
```





Risorse utili: 

- https://www.liquidweb.com/kb/what-is-the-default-password-for-postgresql/
- https://www.postgresql.org/docs/11/auth-pg-hba-conf.html