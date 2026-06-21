# SSH Keys auf Server

## Ziel
Ein Key erstellt werden und der vorhandene auf den Server kopiert werden. Es wir geht dabei um einen Schlüssel (Auf dem Client) und ein Schloss auf dem Server für Passwortlosen Zugang.

## Kontext
- Server Client Kommandozeilensteuerung
- Wichtig, um später immer wieder mit dem Schlüssel auf den Server zu kommen.

## Schritte

1. Key erstellen:

```
ssh-keygen -t ed25519 -C "Homeserver" -f ~/.ssh/homeserver
```

"homeserver" stellt dabei den Namen der .pub Datei dar, die sich im Nutzerverzeichnis unter .ssh finden.
2. Key übertragen: 
Ein vorhandener key in .ssh kann über:

```
ssh-copy-id -i ~/.ssh/homeserver.pub user@server-ip
```
übertragen werden.

3. Config anpassen:

im .ssh Ordner findet sich eine config Datei. Darin muss festgelegt werden, welcher Nutzer auf Welche IP verlinkt ist und wo der Key abliegt:

	Host homeserver
	  HostName 192.168.1.55
	  User tobias
	  IdentityFile ~/.ssh/homeserver

4.  Einloggen:
   
   Nun kann über jede Kommandozeile auf einem Gerät mit dem Schlüssel auf den Server eingewählt werden:
   
```
ssh -i ~/.ssh/homeserver tobias@192.168.1.55
```

Beim ersten Mal wird noch der Key verifiziert durch Eingabe des Passwortes.

5. Zusatz: Passwortloser Zugang:

auf dem Server in /etc/ssh/sshd_config passowordauthentication und usepam auf "no" setzen. 
sudo nano /etc/ssh/sshd_config.d/*.conf hier auch. 
Anschließend 
```
sudo systemctl restart ssh
```

unbedingt vorher mit einem zweiten terminal ausprobieren. 
## Probleme/Risiken
- Verlust des Schlüssels = Verlust des Geräts -Backups erstellen.
## Verknüpfungen
[SSH erklärt: So greifen Profis auf Server zu - YouTube](https://www.youtube.com/watch?v=V3L7cRRrKJc) Abgerufen 06.04.2026