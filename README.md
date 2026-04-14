Bonjour je m'apelle Nicolas et je vais vous présenter mon projet windows core 

Ce proejt va ce concentré sur comment intégré un rockylinux sur un domaine AD core w2022 qui fera égalment office de serveur dhcp et dns pour notre rocky

une fois installer voici notre interface d'accueil

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
Add-DnsServerPrimaryZone -Name "lab.local" -ZoneFile "lab.local.dns" \t
#Ajouter un enregistrement A pour le serveur lui-même
Add-DnsServerResourceRecordA -Name "win-core" -ZoneName "lab.local" -IPv4Address 192.168.1.10

#Pour vérifier les résultat

<img width="807" height="221" alt="image" src="https://github.com/user-attachments/assets/8d47dc2d-05b0-4388-86b8-8bc4d17e9d58" />

<img width="807" height="487" alt="image" src="https://github.com/user-attachments/assets/c3218fd6-d00b-461e-90c1-6e3c0531659e" />

ou avec nslookup

<img width="671" height="136" alt="image" src="https://github.com/user-attachments/assets/a9d75ce3-37fe-4e02-9845-8067e74d1fc4" />

