# Formation Docker

## Prérequis

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
echo "Environment=\"HTTP_PROXY=http://cg_pssmaj:********@orion.dsic.minint.fr:3128\"" >> /etc/systemd/system/docker.service.d/http-proxy.conf
echo "Environment=\"HTTPS_PROXY=http://cg_pssmaj:********@orion.dsic.minint.fr:3128\"" >> /etc/systemd/system/docker.service.d/http-proxy.conf
echo "Environment=\"NO_PROXY=minint.fr,localhost,127.0.0.1\"" >> /etc/systemd/system/docker.service.d/http-proxy.conf

systemctl restart docker

exit
```

## Atelier #1

Prise en main de *docker* et téléchargement d'un container tout prêt

## Atelier #2

Ecrire un fichier Dockerfile puis construire son propre container

## Atelier #3

Utilisation d'un container

## Atelier #4

Mettre une API Python dans un container

## Atelier #5

Créer et utiliser les volumes dans mes container

## Atelier #6

Utiliser des container dans des services SystemD

## Atelier #7

Debug et résolutions des problèmes
