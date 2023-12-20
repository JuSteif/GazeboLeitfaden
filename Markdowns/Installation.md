# Installation

## Vorbereitung

Gazebo hat Gazebo-Classic abgelöst. Wenn versucht wird, Gazebo parallel zu Gazebo-Classic zu installieren, wird Gazebo-Classic deinstalliert.

Es werden folgende Tools benötigt:

- lsb-release
- wget
- gnupg

Diese werden mit den folgenden Befehlen installiert:

```
sudo apt-get update

sudo apt-get install lsb-release wget gnupg
```

## Installation von Harmonic

Die Installation von Harmonic ist für Ubuntu 22.04 vorgesehen.

Im ersten Schritt müssen die Repositories den Packetquellen hinzugefügt werden.
```
sudo wget https://packages.osrfoundation.org/gazebo.gpg -O /usr/share/keyrings/pkgs-osrf-archive-keyring.gpg

echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/pkgs-osrf-archive-keyring.gpg] http://packages.osrfoundation.org/gazebo/ubuntu-stable $(lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/gazebo-stable.list \> /dev/null
```

Im nächsten Schritt kann Gazebo installiert werden.
```
sudo apt-get update

sudo apt-get install gz-harmonic
```

## Installation von Garden

Die Installation von Harmonic ist für Ubuntu 20.04 vorgesehen.

Zunächst müssen die Repositories den Packetquellen hinzugefügt werden.
```
sudo wget https://packages.osrfoundation.org/gazebo.gpg -O /usr/share/keyrings/pkgs-osrf-archive-keyring.gpg

echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/pkgs-osrf-archive-keyring.gpg] http://packages.osrfoundation.org/gazebo/ubuntu-stable $(lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/gazebo-stable.list \> /dev/null
```

Im nächsten Schritt kann Gazebo installiert werden.
```
sudo apt-get update

sudo apt-get install gz-garden
```

[Main Page](../README.md)
