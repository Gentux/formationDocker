# Préparation des atelier docker

Docker doit être installé sur votre poste.

L'utilisateur courant doit appartenir au group `docker` pour éviter d'avoir à exécuter toutes les commandes en `sudo`.

```sh
sudo usermod -aG docker $USER
```

Un proxy http doit être configuré pour Docker.

```sh
sudo -s

mkdir /etc/systemd/system/docker.service.d

echo "[Service]" > /etc/systemd/system/docker.service.d/http-proxy.conf
echo "Environment=\"HTTP_PROXY=http://orion_user:********@orion.dsic.minint.fr:3128\"" >> /etc/systemd/system/docker.service.d/http-proxy.conf
echo "Environment=\"HTTPS_PROXY=http://otion_user:********@orion.dsic.minint.fr:3128\"" >> /etc/systemd/system/docker.service.d/http-proxy.conf
echo "Environment=\"NO_PROXY=minint.fr,localhost,127.0.0.1\"" >> /etc/systemd/system/docker.service.d/http-proxy.conf

systemctl daemon-reload && systemctl restart docker

exit
```
