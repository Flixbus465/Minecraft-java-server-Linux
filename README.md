# Minecraft-java-server-Linux
# 🧱 Minecraft Java Server unter Linux

Willkommen! Diese Anleitung zeigt dir Schritt für Schritt, wie du unter Linux einen Minecraft Java Server aufsetzt – inklusive Java-Installation, Server-Download, Portfreigabe und Startskript. Ideal für Freunde, LAN-Partys oder deinen eigenen Online-Server.

---

## 📦 Voraussetzungen

- Linux (Ubuntu, Debian, Arch, etc.)
- Java 17 oder neuer
- Root- oder sudo-Zugriff
- Zugriff auf deinen Router zur Portfreigabe
- Optional: `screen` für Dauerbetrieb im Hintergrund

---

## 🔧 Java 17 installieren

### Ubuntu/Debian:
```bash
sudo apt update
sudo apt install openjdk-17-jre-headless
```

### Arch Linux:
```bash
sudo pacman -S jdk17-openjdk
```

### Version prüfen:
```bash
java -version
```

---

## 📂 Minecraft Server einrichten

### Ordner erstellen:
```bash
mkdir minecraft-server
cd minecraft-server
```

### PaperMC herunterladen (empfohlen):
```bash
wget https://api.papermc.io/v2/projects/paper/versions/1.20.4/builds/latest/downloads/paper-1.20.4-latest.jar -O server.jar
```

📎 Alternativ: [Minecraft Vanilla Server](https://www.minecraft.net/de-de/download/server)

---

## ▶️ Startskript erstellen

### Neue Datei `start.sh`:
```bash
nano start.sh
```

Inhalt einfügen:
```bash
#!/bin/bash
cd "$(dirname "$0")"
java -Xmx2G -Xms1G -jar server.jar nogui
```

Speichern mit `CTRL+O`, schließen mit `CTRL+X`

Dann ausführbar machen:
```bash
chmod +x start.sh
```

---

## 🚀 Server das erste Mal starten

```bash
./start.sh
```

Ergebnis: Der Server wird sich sofort beenden, weil du der EULA noch nicht zugestimmt hast.

### EULA akzeptieren:
```bash
nano eula.txt
```

Ändere:
```
eula=false
```
zu:
```
eula=true
```

Jetzt kannst du den Server erneut starten:
```bash
./start.sh
```

---

## 🌐 Portfreigabe im Router

Damit andere Spieler über das Internet beitreten können:

1. Öffne deinen Router im Browser (z. B. `http://fritz.box`)
2. Navigiere zu **Portfreigaben** oder **NAT / Portweiterleitung**
3. Erstelle eine neue Freigabe:

   - **Port extern**: 25565  
   - **Port intern**: 25565  
   - **Protokoll**: TCP (ggf. auch UDP)  
   - **Ziel-IP**: lokale IP deines Servers (z. B. 192.168.178.23)

4. Speichern und ggf. Router neustarten

### Eigene IP-Adresse herausfinden:
```bash
ip a
```

### Öffentliche IP anzeigen:
🔗 [https://www.wieistmeineip.de](https://www.wieistmeineip.de)

---

## 🔥 Firewall öffnen (Ubuntu/Debian mit UFW)

```bash
sudo ufw allow 25565/tcp
```

---

## 💻 Im Hintergrund laufen lassen (optional)

Installiere `screen`:
```bash
sudo apt install screen
```

Server starten mit `screen`:
```bash
screen -S minecraft
./start.sh
```

Zum Verlassen (ohne Beenden): `CTRL + A`, dann `D`  
Wieder verbinden:
```bash
screen -r minecraft
```

---

## ⚙️ Server konfigurieren

In der Datei `server.properties` kannst du u. a. einstellen:

```properties
motd=Mein Minecraft Server
gamemode=survival
difficulty=normal
max-players=10
white-list=true
online-mode=true
```

Zum Bearbeiten:
```bash
nano server.properties
```

---

## 🔗 Nützliche Links

| Beschreibung                 | Link |
|-----------------------------|------|
| Java 17 (Oracle Archiv)     | https://www.oracle.com/java/technologies/javase/jdk17-archive-downloads.html |
| Minecraft Server (Vanilla)  | https://www.minecraft.net/de-de/download/server |
| PaperMC Server              | https://papermc.io/downloads |
| Öffentliche IP anzeigen     | https://www.wieistmeineip.de |
| Fritzbox Oberfläche         | http://fritz.box |

---

## ✅ Fertig!

Dein Server läuft jetzt unter Linux! 🎉 Freunde können über deine öffentliche IP auf Port `25565` beitreten. Beispiel:

```text
123.45.67.89:25565
```

---

## 📜 Zusammenfassung des Startskripts

```bash
#!/bin/bash
cd "$(dirname "$0")"
java -Xmx2G -Xms1G -jar server.jar nogui
```

Du kannst die RAM-Werte nach Wunsch anpassen, z. B. `-Xmx4G` für 4 GB.

---

## 🧠 Tipps

- Immer ein Backup machen, bevor du den Server updatest
- Paper ist schneller und stabiler als Vanilla
- Verwende `whitelist.json`, um nur bestimmten Spielern Zugriff zu geben
- Nutze `ops.json`, um Admins festzulegen

---

## ☕ Viel Spaß beim Bauen & Zocken!

Wenn dir dieses Projekt hilft, gib ihm gerne einen ⭐ auf GitHub :)
