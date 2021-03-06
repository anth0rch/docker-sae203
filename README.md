**Équipe :** Équipe n°5  

**Nom des membres de l'équipe :**  

Andoche Keran,  

Dinh Tran Thai Duc,  

Claccin Noemie,  

Rocha Anthony  


**Année :** 2021/2022   

**Département Informatique , IUT Le Havre - Sae2.03** 

--------------------------------------------------------------------------------

# Installation du service  multimédia Jellyfin sous débian avec l'aide d'un Dockerfile

1. Pour s'assurer l'installation du service sous débian, il faut ajouter cette ligne de commmande sous le Dockerfile :
```shell
FROM debian:latest
``` 
 #### Installation des paquetages

2. Pour s'assurer que l'installation se déroule correctement, on met à jour le système :
```shell
apt update -y && apt upgrade -y
```

3. On installe les paquetages ```sudo``` pour permettre de prendre les droits du root pour exécuter les commandes :
```shell
apt-get install sudo -y
```

4. On s'assure que l'on peut utiliser des référentiels accessibles  via le protocole HTTPS, tout en indiquant l'autorité de certification ```gnup2``` et de s'assurer le transfert des données avec ```git``` :

```shell
sudo apt install apt-transport-https ca-certificates gnupg2 curl git -y
```

5. Pour éviter que l'installation échoue, on importe  la clé et le référentiel Jellyfin GPG pour vérifier l’authenticité du paquet :
```shell
sudo wget -O- https://repo.jellyfin.org/jellyfin_team.gpg.key | gpg --dearmor | sudo tee /usr/share/keyrings/jellyfin.gpg
```

6. On remet à jour le système pour éviter et corriger d'éventuelles erreurs :

```shell
sudo apt update  -y && sudo apt upgrade -y
```

7. On peut désormais procéder à l'installation du serveur Multimédia Jellyfin :

```shell
sudo apt install jellyfin -y
```

8. Pour permettre de configurer les services qui sont lancés au démarrage, il faut installer ```systemctl``` :

```shell
apt install systemctl -y
```

9. Pour démarrer le service, on exécute la commande suivante :

```shell
sudo systemctl start jellyfin
```

10. Puis, pour activer le service au démarrage, il faut exécuté la commande suivante :

```shell
sudo systemctl enable jellyfin
```

11. Enfin, il faut s'assurer que l'on soit sur le port par défaut de Jellyfin qui est le port 8096 :
```shell
EXPOSE 8096
```
--------------------------------------------------------------------------------

## Instructions pour lancer Jellyfin grâce à Dockerfile

1. On vérifie si docker est installé :
```shell
docker --version
```

2. On clone le référentiel :
 ```shell
git clone git@github.com:anth0rch/docker-sae203.git
```

3. On accède au référentiel :
```shell
cd docker-sae203
```

4. On construit l'image décrite dans dockerfile avec docker build : 
```shell
docker build -t jellyfin .
```

5. On créé, on initialise un container à partir de l'image construite avec la commande suivante :
```shell
docker run --name jellyfin-conteneur -d -p 2783:8096 jellyfin
```

6. Puis, pour lancer le container, on exécute la commande suivante : 
```shell
docker start jellyfin-conteneur
```


8. On vérifie que l'application est en cours d'exécution. Pour ce faire, on ouvre un navigateur et on saisie dans la barre d'URL :  
  ```di-docker:2783``` ou bien ```localhost:2783```

9. On vérifie que le conteneur associé est actif :
```shell
docker ps
```

10. Puis , on arrête l'exécution du dockeur en cours si nous ne voulons plus l'utiliser :
```shell
docker stop jellyfin-conteneur
```








