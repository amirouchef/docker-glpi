**Install and run an GLPI instance with docker**  

**Tâche n°1 : Installer les paquets nécessaires permettant à apt d'utiliser les paquets sur HTTPS**  
sudo apt install  apt-transport-https  ca-certificates  curl  software-properties-common  

**Tâche n°2 : Ajouter la clé GPG du dépôt officiel de Docker au système**  
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add --  
sudo cp /etc/apt/trusted.gpg /etc/apt/trusted.gpg.d  

**Tâche n°3 : Ajouter le référentiel Docker aux sources APT**  
sudo  add-apt-repository  "deb [arch=amd64] https://download.docker.com/linux/ubuntu focal stable"  

**Tâche n°4 : Mettre à jour la base de données des paquets avec les paquets du référentiel Docker qui vient d'être ajouté**  
sudo apt update  

**Tâche n°5 : Vérifier le dépôt afin de s’assurer que l’installation est réalisée à partir du dépôt Docker (et non du dépôt Ubuntu par défaut)**  
apt-cache policy docker-ce  

**Tâche n°6 : Installer Docker**  
sudo apt install docker-ce  

**Tâche n°7 : Clonnee le git**  
git clone https://github.com/amirouchef/docker-glpi.git  

**Tâche n°8 : Deploy GLPI**  
cd docker-glpi  
sudo docker run --name mariadb -e MARIADB_ROOT_PASSWORD=root -e MARIADB_DATABASE=glpidb -e MARIADB_USER=glpi_user -e MARIADB_PASSWORD=glpi -d mariadb:10.7  
sudo docker build -t monglpi .  
docker run --name glpi --link mariadb:mariadb  -d -p 80:80 monglpi  

**Tâche n°9 : Finaliser l'installation depuis la navigateur**   
@IP pour la base de donner renseignez : database : mariadb | username : glpi_user| password : glpi  
