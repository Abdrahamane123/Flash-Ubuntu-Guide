# Installer Ubuntu sur Raspberry Pi et passer de Desktop à Server (et inversement)

Ce guide explique comment écrire une image Ubuntu pour Raspberry Pi (Desktop ou Server) et comment basculer entre les deux versions. Les instructions incluent des étapes claires et des emplacements pour insérer vos propres captures d'écran.

---

## Prérequis

- Un Raspberry Pi (modèles supportés : Pi 3, Pi 4, Pi 400, etc.)
- Une carte microSD d'au moins 16 Go
- Un ordinateur avec un lecteur de cartes SD
- [Raspberry Pi Imager](https://www.raspberrypi.com/software) (ou un autre outil pour écrire l'image)
- (Optionnel) Une image Ubuntu Desktop ou Server téléchargeable [ici](https://ubuntu.com/download/raspberry-pi)

---

## Étape 1 : Préparer l'image Ubuntu

### **Option 1 : Utiliser les images intégrées dans Raspberry Pi Imager**

1. Téléchargez et installez [Raspberry Pi Imager](https://www.raspberrypi.com/software) sur votre ordinateur.
2. Ouvrez Raspberry Pi Imager.

   *![image](https://github.com/user-attachments/assets/cd82428e-4de7-4f30-b222-c547244cf6dd)*

3. Cliquez sur **Choose OS**, puis sur **Other general-purpose OS** et sélectionnez :
   - **Ubuntu** dans la liste des systèmes d'exploitation disponibles.
   - Choisissez la version souhaitée : **Ubuntu Desktop** ou **Ubuntu Server**.

   *![image](https://github.com/user-attachments/assets/ca9e4fbe-1ef3-404a-b5cb-e6b23d333914)*

4. Cliquez sur **Choose Storage** et sélectionnez votre carte microSD.

5. Appuyez sur **Ctrl+Maj+X** pour accéder aux options avancées. Cette étape est importante si vous avez choisi **Ubuntu Server**. Configurez les paramètres suivants :
   - Activez SSH.
   - Renseignez vos informations de réseau (SSID et mot de passe de votre routeur).
   - Configurez le nom d'utilisateur et le mot de passe par défaut.

![image](https://github.com/user-attachments/assets/76905ea2-c7ce-424f-88a4-2e01bd1fde7f)

![image](https://github.com/user-attachments/assets/52c94c91-f69e-4f70-a609-27aa669e693c)*

7. Cliquez sur **Write** pour commencer l'écriture de l'image sur la carte SD.

   *(Insérer ici une capture d'écran montrant la progression de l'écriture sur la carte SD)*

8. Une fois l'écriture terminée, insérez la carte SD dans votre Raspberry Pi.

---

### **Option 2 : Télécharger une image Ubuntu depuis le site officiel**

1. Accédez au [site officiel d'Ubuntu](https://ubuntu.com/download/raspberry-pi).
2. Téléchargez l'image souhaitée (Desktop ou Server).

   *(Insérer ici une capture d'écran du site officiel d'Ubuntu, montrant le téléchargement des images Desktop et Server)*

3. Passez à **l'Étape 2** pour écrire l'image manuellement.

---

## Étape 2 : Écrire l'image sur la carte SD

Si vous avez déjà utilisé **Option 1**, vous pouvez ignorer cette étape. Sinon, procédez comme suit :

1. Insérez la carte microSD dans le lecteur de cartes de votre ordinateur.
2. Utilisez l'un des outils suivants pour écrire l'image :

   - **Avec Raspberry Pi Imager** :
     - Cliquez sur **Choose OS**, puis sur **Use Custom** pour charger l'image téléchargée.
       
       *(Insérer ici une capture d'écran montrant l'utilisation de "Use Custom" dans Raspberry Pi Imager)*

   - **Avec Balena Etcher** :
     - Sélectionnez l'image Ubuntu téléchargée.
     - Sélectionnez la carte SD.
     - Cliquez sur **Flash!**.

       *(Insérer ici une capture d'écran de l'interface de Balena Etcher)*

   - **Avec la commande `dd` (Linux/macOS)** :
     ```bash
     sudo dd if=/path/to/ubuntu-image.img of=/dev/sdX bs=4M conv=fsync
     ```
     (Remplacez `/dev/sdX` par l'identifiant de votre carte SD, vérifiable avec `lsblk`.)

3. Une fois l'écriture terminée, insérez la carte SD dans votre Raspberry Pi.

---

## Étape 3 : Configurer et démarrer le Raspberry Pi

### **Pour Ubuntu Desktop :**
1. Connectez un écran, un clavier, et une souris à votre Raspberry Pi.
2. Démarrez le Raspberry Pi et suivez les instructions de configuration initiale.
3. Une fois terminé, l'interface graphique d'Ubuntu Desktop devrait apparaître.

   *(Insérer ici une capture d'écran de l'interface bureau d'Ubuntu Desktop après configuration)*

### **Pour Ubuntu Server :**
1. Assurez-vous que votre Raspberry Pi est connecté au même réseau que votre ordinateur (via Wi-Fi ou Ethernet).
2. Trouvez l'adresse IP de votre Raspberry Pi (par exemple, en utilisant votre routeur ou un outil tiers).
3. Connectez-vous en SSH à l'aide de cette commande (remplacez `192.168.X.X` par l'adresse IP réelle) :
   ```bash
   ssh pi@192.168.X.X
   ```
4. Acceptez les conditions en tapant `yes`, puis entrez le mot de passe que vous avez configuré.

   *(Insérer ici une capture d'écran montrant la connexion SSH réussie)*

---

## Étape 4 : Passer de Desktop à Server (ou l'inverse)

### **Passer de Server à Desktop**
1. Connectez-vous en SSH ou utilisez un terminal local.
2. Installez l'environnement Desktop :
   ```bash
   sudo apt update && sudo apt install ubuntu-desktop
   ```
3. Redémarrez le Raspberry Pi :
   ```bash
   sudo reboot
   ```

   *(Insérer ici une capture d'écran montrant l'installation du paquet `ubuntu-desktop`)*

### **Passer de Desktop à Server**
1. Désinstallez l'environnement Desktop pour alléger le système :
   ```bash
   sudo apt purge ubuntu-desktop
   sudo apt autoremove
   ```
2. Redémarrez le Raspberry Pi :
   ```bash
   sudo reboot
   ```

   *(Insérer ici une capture d'écran montrant la commande `sudo apt purge ubuntu-desktop`)*

---
