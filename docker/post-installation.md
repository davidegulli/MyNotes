## Post installation Tasks



#### Group setting

- Creare il gruppo docker per consentire ad un utente non-root di usare il servizio e dare modo al servizio di accedere ai volumi configurati

  ```bash
  sudo groupadd docker
  ```

- Aggiungere gli utenti necessari al nuovo gruppo *docker*

  ```bash
  sudo usermod -aG docker [user]
  ```

  E' necessario effettuare il logout dell'utente



---------------------------



#### Start on system boot

```bash
sudo systemctl enable docker
```

