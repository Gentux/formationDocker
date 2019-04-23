# Atelier SystemD 1: Lancer un container avec SystemD

On va d'abord écrire le fichier qui décrit notre service pour systemd.

On le place ensuite dans `/etc/systemd/system/backend.service`

Ensuite on le démarre en l'activant afin qu'il démarre tout avec la machine:

```
sudo systemctl daemon-reload
sudo systemctl enable backend.service
sudo systemctl start backend.service
```

Pour vérifier, nous pouvons observer les logs avec 

```
sudo journalctl -fu backend.service
```
