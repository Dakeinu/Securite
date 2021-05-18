<center> <h1>Dossier Technique Securite</h1> </center>

> **Membres :** François BONNIN - Rémi FALCATI

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




