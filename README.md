 Deploy Technik Camp info-beamer
================================
![Technik Camp](https://github.com/ffbsee/ffbsee-grafik/blob/master/events/technikcamp2019-sticker.svg "Technik Camp 2019")

Dies ist ein Ansible Playbook um info-beamer mit dem Fahrplan auf dem Technik Camp zu deployen.

 clonen
-----------
```bash
git clone --recursive https://github.com/ffbsee/ansible-deploy-camp-displays.git

# Clone the Submodules too
cd ansible-deploy-camp-displays
git submodule update --init --recursive
```

 Wie geht das mit dem info-beamer deployen?
-----------------------------------------------
1. Du hast einen Raspberry Pi, der mit Rasbian-lite geflashed ist
2. Du kannst dich per ssh auf dem raspberry pi anmelden
3. Erstelle den User ``ansible`` Manuell auf dem raspberry pi.
```
# Beispiel
## add sudo
sudo adduser ansible

## add sudo permissions
echo 'ansible ALL=NOPASSWD: ALL' | sudo EDITOR='tee -a' visudo
```
4. Der User ``ansible`` hat auch deinen ssh key
```
# Beispiel
ssh-copy-id ansible@<dein_raspi>
```
5. dieses git sollte deinen ssh key und benutzer kennen, sonst darfst du dich nicht mehr anmelden.
   Wichtige Dateien hierfür sind:
```text
files/ssh_public_keys/ # hier sollten deine ssh public keys hin - so wie die der anderen auch
group_vars/all.yml # hier wird definiert welcher ssh key zu welchen user gehört. Und welche user es überhaupt gibt. und wer root darf. trag dich ein. als user und als root!
```
6. Der raspberry pi muss in der Datei ``ansible/host.ini`` ergänzt werden. Lass dich an der anderen config inspirieren
7. Der Ordner ``$HOME/ansible/`` sollte bei dir exestieren!
8. Nun kannst du das ansible ``site.yml`` ausführen:
```bash
# führe ansible aus
ansible-playbook site.yml
```


