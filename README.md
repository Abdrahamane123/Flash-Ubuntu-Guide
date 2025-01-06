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

### Option 1 : Utiliser les images intégrées dans Raspberry Pi Imager

1. Téléchargez et installez [Raspberry Pi Imager](https://www.raspberrypi.com/software) sur votre ordinateur.
2. Ouvrez Raspberry Pi Imager.
   ![image](https://github.com/user-attachments/assets/627bf0d7-381b-4076-8c00-e8760a53889d)
3. Cliquez sur **Choose model** puis choisissez le model de votre raspberry pi

4. Cliquez sur **Choose OS**, puis **Other general-purpose OS** et sélectionnez :
   - **Ubuntu** dans la liste des systèmes d'exploitation disponibles.
   - Choisissez la version souhaitée : **Ubuntu Desktop** ou **Ubuntu Server**.
   ![image](https://github.com/user-attachments/assets/574d12a1-3de9-4a21-bc07-76c56c9c4aa3)

4. Cliquez sur **Choose Storage** et sélectionnez votre carte microSD.
5. Cliquez sur **Write** pour commencer l'écriture de l'image sur la carte SD.

*(Insérer ici une capture d'écran montrant la sélection de la carte SD et l'étape de confirmation d'écriture)*

### Option 2 : Télécharger une image Ubuntu depuis le site officiel

1. Accédez au [site officiel d'Ubuntu](https://ubuntu.com/download/raspberry-pi).
2. Téléchargez l'image souhaitée (Desktop ou Server).
3. Passez ensuite à **l'Étape 2** pour écrire l'image manuellement.

*(Insérer ici une capture d'écran du site officiel d'Ubuntu, montrant le téléchargement des images Desktop et Server)*

---

## Étape 2 : Écrire l'image sur la carte SD

Si vous avez déjà utilisé **Option 1** (Raspberry Pi Imager), cette étape est terminée. Sinon, procédez comme suit :

1. Insérez la carte microSD dans le lecteur de cartes de votre ordinateur.
2. Lancez votre logiciel d'écriture d'images :
   - Avec Raspberry Pi Imager :
     - Cliquez sur **Choose OS**, puis **Use Custom** pour charger l'image téléchargée.
   - Avec Balena Etcher :
     - Sélectionnez l'image Ubuntu.
     - Sélectionnez la carte SD.
     - Cliquez sur **Flash!**.
   - Avec `dd` (Linux/macOS) :
     ```bash
     sudo dd if=/path/to/ubuntu-image.img of=/dev/sdX bs=4M conv=fsync
     ```
     (Remplacez `/dev/sdX` par l'identifiant de votre carte SD, vérifiable avec `lsblk`.)

*(Insérer ici une capture d'écran montrant l'utilisation de "Use Custom" dans Raspberry Pi Imager ou l'interface de Balena Etcher)*

---

## Étape 3 : Configurer et démarrer le Raspberry Pi

1. Insérez la carte microSD dans le Raspberry Pi.
2. Connectez un écran, un clavier, une souris (pour Desktop), ou configurez un accès SSH (pour Server).
3. Démarrez le Raspberry Pi et suivez les instructions de configuration initiale.

*(Insérer ici une capture d'écran du premier écran visible après le démarrage)*

---

## Étape 4 : Passer de Desktop à Server (ou l'inverse)

### Passer de Server à Desktop

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

### Passer de Desktop à Server

1. Désinstallez l'environnement Desktop pour alléger le système :
   ```bash
   sudo apt purge ubuntu-desktop
   sudo apt autoremove
   ```
2. Redémarrez le Raspberry Pi :
   ```bash
   sudo reboot
   ```

*(Insérer ici une capture d'écran de la commande `sudo apt purge ubuntu-desktop`)*

---

## Remarques et conseils

- Si vous utilisez Raspberry Pi Imager, assurez-vous d’avoir une connexion Internet stable pour télécharger l’image directement.
- Sauvegardez vos données avant de flasher une nouvelle image ou de basculer entre les versions.
- Si vous rencontrez des problèmes, consultez la [documentation officielle](https://ubuntu.com/tutorials) ou ouvrez une issue dans ce dépôt.

---

Tu peux maintenant insérer tes captures d'écran aux endroits mentionnés. Dis-moi si tu veux que j'ajoute des détails supplémentaires !
