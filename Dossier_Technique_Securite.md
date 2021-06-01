<center> <h1>Dossier Technique Securite - Groupe 7</h1> </center>

> **Membres :** François BONNIN - Rémi FALCATI - Clément OSCHE

> **Schéma de l'Infrastructure :** 
>> ![](https://cdn.discordapp.com/attachments/758265932057149450/839080360751005696/SchC3A9ma.png)

## Installations de VMs :
### Paramètres PFSense :

1. Mettre les paramètres de la carte réseau 1 sur **Nat** : 
   ![](https://cdn.discordapp.com/attachments/758265932057149450/839079099703099472/unknown.png)

<br>

2. Mettre les paramètres de la carte réseau 2 sur **Lan Segment** et créer le segment **_B2-DMZ_** :
   ![](https://cdn.discordapp.com/attachments/758265932057149450/839079061455241226/unknown.png)

<br>

3. Mettre les paramètres de la carte réseau 3 sur **Lan Segment** et créer le segment **_B2-Lan_** :
   ![](https://cdn.discordapp.com/attachments/758265932057149450/839079132863397898/unknown.png)

### Configurations des Ips PFSense :

1. Addressage IP de l'interface **WAN - em0** :
![](https://cdn.discordapp.com/attachments/758265932057149450/839090786943500308/unknown.png)

<br>

2. On assigne l'interface :
- **WAN**  = em0
- **LAN**  = em2
- **WebServ** = em1
   ![](https://cdn.discordapp.com/attachments/758265932057149450/839772234716807199/unknown.png)
   ![](https://cdn.discordapp.com/attachments/758265932057149450/839772494029258762/unknown.png)
   
<br>

1. Addressage IP de l'interface **Lan - em1** :
![]()

### Paramètres Vm Windows 10 (Pc-Client) :

1. Modifier les paramètres de la carte réseau sur le segment **_B2-Lan_** :
   ![](https://cdn.discordapp.com/attachments/758265932057149450/839762471728185374/unknown.png)

<br>

2. Adressage IPs sur l'interface Windows :
   ![](https://cdn.discordapp.com/attachments/758265932057149450/839762579999293440/unknown.png)

<br>

## Configurations de l'interface Web PFSense :

1. Accès à l'interface web en rentrant l'IP de l'interface **Wan** de PFSense sur le navigateur sur le **Pc-Client** :
   ![](https://cdn.discordapp.com/attachments/758265932057149450/839767850528538644/unknown.png)

<br>


2. Paramètres PFSense :
   -  Aller dans "Système -> Setup Wizard" 
        ![](https://cdn.discordapp.com/attachments/758265932057149450/839795066126073907/unknown.png)


> **! Changer le mot de passe de l'interface web PFSense !**
![](https://cdn.discordapp.com/attachments/758265932057149450/839796872420130856/unknown.png)

<br>

3. Configurations de l'interface **_DMZ_** :
    - On active l'interface
    - On lui met une IP static (indiqué dans le schéma initial)
![](https://media.discordapp.net/attachments/758265932057149450/839797729483030528/unknown.png?width=1037&height=683)

<br>

4. Ajout de règles :
   - Aller dans "Firewall/Rules/(L'interface réseau voulu)". Dans un permier temps nous irons dans l'interface **_LAN_**
   <br>
   - On autorise le Port "**_80_**" sur le port "**_TCP_**"
   ![](https://cdn.discordapp.com/attachments/758265932057149450/839806063443312650/unknown.png)
   <br>
   - Ensuite on fait la même chose pour les autres règles : 
      Port 443 -> HTTPS
      Port 53 -> DNS
   ![](https://cdn.discordapp.com/attachments/758265932057149450/839806440046198794/unknown.png)


## Configuration d'un nouveau windows serveur :

1. Choix des IPs :
   ![](https://cdn.discordapp.com/attachments/758265932057149450/841613571024093214/unknown.png)
   <br>

2. Installation des services AD DS :
   ![](https://cdn.discordapp.com/attachments/758265932057149450/841617665469579274/unknown.png)
   ![](https://cdn.discordapp.com/attachments/758265932057149450/841617951391088680/unknown.png)
   <br>


3. Création d'une nouvelle partition (D:/) :
   ![](https://cdn.discordapp.com/attachments/758265932057149450/841618978799747092/unknown.png)
   <br>

4. Configuration des services de domaine  AD DS :
   ![](https://cdn.discordapp.com/attachments/758265932057149450/841619314133827614/unknown.png)
   <br>

5. Ajout du poste client à L'AD  DS :
   ![](https://cdn.discordapp.com/attachments/758265932057149450/844113192124022784/unknown.png)
   ![](https://cdn.discordapp.com/attachments/758265932057149450/844116973569966080/unknown.png)


## Mise en place du Proxy :

1. Installation de **Squid** sur le PfSense
   ![](https://cdn.discordapp.com/attachments/758265932057149450/844144291798581288/unknown.png)
   <br>


2. Port utilisé pour le proxy : **3128**
   <br>

3. Activation du proxy :
   ![](https://cdn.discordapp.com/attachments/758265932057149450/844148631899602944/unknown.png)
   <br>

## GPO :

1. Création d'une unité d'organisation appelé Ordinateurs pour la mise en place d'une stratégie de groupe (GPO)
   ![](https://cdn.discordapp.com/attachments/758265932057149450/844850639263367188/unknown.png)
   ![](https://cdn.discordapp.com/attachments/758265932057149450/844880415591890974/unknown.png)
   <br>

2. La configuration Visibilité de la page des paramètres est un objet de stratégie GPO permettant de supprimer la visibilité et l'accessibilité de certains paramètres Windows
   ![](https://cdn.discordapp.com/attachments/758265932057149450/844882094765113354/unknown.png)

   <br>

3. Activation du controle d'accès
   ![](https://cdn.discordapp.com/attachments/758265932057149450/844884425095643136/unknown.png)
   <br>

4. Bloquer un site
   ![](https://cdn.discordapp.com/attachments/758265932057149450/844887734241591346/unknown.png)
   <br>

5. On entre l'adresse ip du serveur pfsense et le port 318
   ![](https://cdn.discordapp.com/attachments/758265932057149450/844887469103251486/unknown.png)
   <br>

6. Téléchargement des modèles gpo destinés à Firefox et importation dans le dossier PolicyDefinitions situé dans D:\ADDS\SYSVOL\domain\Policies\PolicyDefinitions
   ![](https://cdn.discordapp.com/attachments/758265932057149450/845098600811593798/unknown.png)
   <br>

7. Dans les paramètres de notre stratégie de groupe, le dossier Mozilla apparait, on peut alors activer les paramètres de proxy
   ![](https://cdn.discordapp.com/attachments/758265932057149450/845100943792144434/unknown.png)
   <br>

8. Téléchargement des fichiers admx de Edge.
Ajout des 3 fichiers msedge.admx, msedgeupdate.admx et msedgewebview2.admx + le dossier FR + le dossier en-US dans notre dossier PolicyDefinitions
![](https://cdn.discordapp.com/attachments/758265932057149450/847602839240966234/unknown.png)
<br>

9. Une fois les fichiers installés, ils s'affichent dans le modèle d'administration de l'éditeur de gestion de stratégies de groupe
![](https://cdn.discordapp.com/attachments/758265932057149450/849201000958525490/unknown.png)
<br>

10. Création de paramètre proxy pour firefox
    - On active les  paramètre du proxy
    - On interdit la modification des paramètres du proxy
    - On rentre l'HTTP du proxy  : **192.168.15.54**
    - On selecctionne le **SOCKS** -> **SOCKS  V5**
![](https://cdn.discordapp.com/attachments/758265932057149450/849202063266283564/unknown.png)
<br>

11. On applique ces paramètres
![](https://cdn.discordapp.com/attachments/758265932057149450/849202767804628992/unknown.png)
<br>

12. Notre GPO s'affiche correctement dans les stratégies de groupe actives
![](https://cdn.discordapp.com/attachments/758265932057149450/849202980610637844/unknown.png)
<br>

13. Si l'on se rend à présent sur notre Mozilla Firefox dans notre PC Client, les paramètres proxy sont correctement configurés et bloqué
![](https://cdn.discordapp.com/attachments/758265932057149450/849203542509617182/unknown.png)

## Reverse Proxy :

1. Installer les packages Squid dans _System/Package Manager/Available Packages_. Rechercher _squid_ et cliquer sur **Install**.
 <br>

2. Créer la règle "System Tunables" dans _System/Advanced/System Tunables_, cliquer sur **New** et remplisser le champ **Tunable** avec la valeur `net.inet.ip.portrange.reservedhigh` et indiquez **0** comme valeur. Si l'on n'ajoute pas cette option, nous ne pouvons pas utiliser les ports 80 et 443 avec Squid, car ils sont déjà réservés.
![](https://cdn.discordapp.com/attachments/522143202426224654/846539879465877504/unknown.png) 
<br>

3. Activation de l'HTTP Reverse Proxy dans _Services/Squid Reverse Proxy_ dans la section **General**
   ![](https://cdn.discordapp.com/attachments/758265932057149450/849190901502443530/unknown.png)

4. Configurer Squid Reverse Proxy dans _Services/Squid Reverse Proxy_ et ajouter un élément dans la section **Web Servers**. Ainsi on va pouvoir ajouter un serveur web.
![](https://cdn.discordapp.com/attachments/758265932057149450/849177522746556447/unknown.png)
![](https://cdn.discordapp.com/attachments/758265932057149450/849177674650877952/unknown.png)

On retrouve ainsi nos 2 serveurs web bien ajouté :
![](https://cdn.discordapp.com/attachments/758265932057149450/849177696189284373/unknown.png)
<br>

5. Pour associer à un nom de domaine, il faut se rendre dans la section Mappings, ajouter avec Add et sélectionner le serveur qui hébergent le site. Puis entrer le nom de domaine `site0.contoso.web` dans le champ URI.
![](https://cdn.discordapp.com/attachments/758265932057149450/849178114273968128/unknown.png)
On fait la même chose pour `site1.contoso.web` et on obtient les deux règles suivantes.
![](https://cdn.discordapp.com/attachments/758265932057149450/849205722167902218/unknown.png)
<br>

6. Il nous faut ouvrir le port 80 sur l'interface WAN afin de pouvoir tester le reverse proxy
![](https://cdn.discordapp.com/attachments/758265932057149450/849181653477752862/unknown.png)

7.  Comme nous n'avons pas acheter le nom de domaine `site0.contoso.web`, il est nécessaire de configurer
sur notre pc client, un fichier hosts dans lequel nous allons dire à notre pc que le nom de domaine
`site0.contoso.web` correspond à l'ip 192.168.5.50:
Ainsi si vous êtes sur Windows, dans le fichier unité système:\Windows\System32\Drivers\etc\hosts, si
vous êtes sur Linux c'est dans le fichier /etc/hosts rajouter une ligne contenant :
`192.168.5.54 site0.contoso.web` : 
![](https://cdn.discordapp.com/attachments/758265932057149450/849215342370750474/unknown.png)
<br>

8. On test l'URL dans notre navigateur et on peut constater que le reverse proxy est bien mis en place
![](https://cdn.discordapp.com/attachments/758265932057149450/849217233892409344/unknown.png)
