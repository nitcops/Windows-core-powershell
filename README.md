Bonjour je m'apelle Nicolas et je vais vous présenter mon projet windows core 

Ce proejt va ce concentré sur comment intégré un rockylinux sur un domaine AD core w2022 qui fera égalment office de serveur dhcp et dns pour notre rocky

voici notre schéma réseau même si en pratique les client et les serveur ne devrai pas être dans le même sous réseaux/VLAN ici nous allons simplifié pour évité de que le sujet soit trop long

<img width="435" height="296" alt="image" src="https://github.com/user-attachments/assets/d0f2b2ab-5b3f-4a6d-ba76-18981df663e8" />


une fois notre w2022 installer voici notre interface d'accueil

<img width="980" height="523" alt="image" src="https://github.com/user-attachments/assets/aa27f546-5022-4b34-bf4c-23a47c2e0cd4" />

il nous suffit d'aller configuré notre premiére carte réseaux en ip fixe cela permettra plus tard d'avoir un réseaux privée entre notre server dhcp et rocky pour rocky puisse avoir une ip distribué par le dhcp

tapé 8 Paramètres réseau

<img width="804" height="503" alt="image" src="https://github.com/user-attachments/assets/25b1b2f0-7823-41e1-bfc6-84744180d065" />

puis 1 pour configuré les paramétre réseaux
<img width="804" height="290" alt="image" src="https://github.com/user-attachments/assets/0f1676ea-6ffd-4c78-9346-74e9b822aa87" />
<img width="813" height="510" alt="image" src="https://github.com/user-attachments/assets/653bb226-00ff-4b9a-8ed5-74667eb2b3eb" />

15

<img width="809" height="505" alt="image" src="https://github.com/user-attachments/assets/75b44c00-63a1-4bf4-ba6c-cc80277a6373" />

# Installation DNS et DHCP powershell
Install-WindowsFeature DNS -IncludeManagementTools

Install-WindowsFeature DHCP -IncludeManagementTools

<img width="803" height="222" alt="image" src="https://github.com/user-attachments/assets/21d1afef-42b2-4a7a-8630-6b2d4b900072" />

#Créer la zone DNS (ex: lab.local)

Add-DnsServerPrimaryZone -Name "lab.local" -ZoneFile "lab.local.dns" 

#Ajouter un enregistrement A pour le serveur lui-même

Add-DnsServerResourceRecordA -Name "win-core" -ZoneName "lab.local" -IPv4Address 192.168.1.10

#Pour vérifier les résultat

<img width="807" height="221" alt="image" src="https://github.com/user-attachments/assets/8d47dc2d-05b0-4388-86b8-8bc4d17e9d58" />

<img width="807" height="487" alt="image" src="https://github.com/user-attachments/assets/c3218fd6-d00b-461e-90c1-6e3c0531659e" />

ou avec nslookup

<img width="671" height="136" alt="image" src="https://github.com/user-attachments/assets/a9d75ce3-37fe-4e02-9845-8067e74d1fc4" />

Pour définir une etendu DHCP mes client recevrons donc une ip dans l'intervalle .50 > .100

<img width="818" height="50" alt="image" src="https://github.com/user-attachments/assets/6dbe1a1c-31bb-43bb-923b-4e4502fe11ed" />

#2. Définir le DNS que les clients recevront (l'IP de ton Windows Core)

<img width="816" height="53" alt="image" src="https://github.com/user-attachments/assets/0e51f4c8-3d24-4aa4-b374-4ce95880b60f" />

on peut déjà voir que la 2eme carte réseaux sur mon rocky récupére la premiére ip du bail dhcp

<img width="806" height="155" alt="image" src="https://github.com/user-attachments/assets/269a3076-6126-4929-8f6a-3ba7913b4280" />

on peu aussi voir quelle récupére le dns 

<img width="439" height="136" alt="image" src="https://github.com/user-attachments/assets/ba297ae6-ec5b-4a9f-9551-354200ee3fbb" />

passont à l'installation de l'active directory 

<img width="816" height="145" alt="image" src="https://github.com/user-attachments/assets/55f8a1a8-a06d-4aff-bf93-de650928bbd7" />

Promouvoir les serveur en DC

<img width="819" height="482" alt="image" src="https://github.com/user-attachments/assets/8911c6a6-4670-4668-9193-d88fd031d455" />

ensuite il va falloir crée un utilisateur pour notre rocky sur notre AD pour cela d'abord crée la variable contenant le mots de passe puis la commande New-ADUser

<img width="814" height="92" alt="image" src="https://github.com/user-attachments/assets/be0678e2-1b2b-4df8-8256-6d1d9cf68769" />



