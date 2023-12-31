﻿# ROS-Anbindung

## ROS-Bridge

Die ROS-Bridge ist ein über den Paketmanager zu installierendes ROS-Paket.
```
sudo apt-get install ros-${ROS_DISTRO}-ros-gz-bridge
```

Die Bridge unterstützt nicht alle Message- und Topic-Typen. Eine entsprechende Liste befindet sich unter folgendem Link:

[ros_gz_bridge](https://github.com/gazebosim/ros_gz/tree/ros2/ros_gz_bridge)

Der Aufruf der ROS-Bridge hat immer den gleichen Aufbau

```
ros2 run ros_gz_bridge parameter_bridge <TOPIC>@<ROS_TYPE><DIRECTION><GZ_TYPE>
```


Typ            | Beschreibung
---------------|---------------------------------------------------------------------------------
\<TOPIC\>      | Hier wird die Topic oder Message angegeben, die über die Bridge laufen soll.
\<ROS_TYPE\>  | Das ist die Message-Art, die im ROS-Netzwerk angezeigt wird.
\<DIRECTION\>  | Die Richtung wird angegeben, in der der Nachrichtenaustausch durchgeführt werden soll. „@" ist für eine bidirektionale Verbindung. „[" überträgt nur Nachrichten aus dem GZ-Netzwerk in das ROS-Netzwerk. „]" ist die entgegengesetzte Übertragungsrichtung.
\<GZ_TYPE\>   | Das ist die Message-Art, die im GZ-Netzwerk angezeigt wird.

## Umsetzung mit eigener Welt

Für die ROS-Anbindung wird die folgende Welt verwendet:

[project_world_camera_lidar64.sdf](../gz_project/project_world_camera_lidar64.sdf)

Der Roboter in dieser Welt verfügt über vier Topics, die Daten für Sensoren und Aktoren enthalten. Dazu gehören die LiDAR-, Kamera- und Bewegungsdaten.

Der LiDAR-Sensor publisht einen LaserScan seiner Umgebung. Dieser kann mit dem folgendem Terminalbefehl in eine ROS-Topic übersetzt werden.
```
ros2 run ros_gz_bridge parameter_bridge /lidar@sensor_msgs/msg/LaserScan[gz.msgs.LaserScan
```

Eine weitere Topic des LiDAR-Sensors ist die PointCloud. Sie ermöglicht das Verwenden mehrerer Layer des Sensors.
```
ros2 run ros_gz_bridge parameter_bridge /lidar/points@sensor_msgs/msg/PointCloud2[gz.msgs.PointCloudPacked
```

Die Kamera veröffentlicht in Bild auf der Topic /cam
```
ros2 run ros_gz_bridge parameter_bridge /cam@sensor_msgs/msg/Image[gz.msgs.Image
```

Die letzte Topic ist /cmd_vel, die den Roboter steuert. Sie ist vom Typ Twist und hat im Gegensatz zu den anderen Topics die umgekehrte Richtung, da der Roboter aus dem ROS-Netzwerk gesteuert werden soll.
```
ros2 run ros_gz_bridge parameter_bridge /model/vehicle_blue/cmd_vel@geometry_msgs/msg/Twist]gz.msgs.Twist
```

Die Visualisierung der Sensordaten erfolgt in Rviz2
```
rviz2
```

Dort muss der „Fixed Frame" geändert werden in „vehicle_blue/chassis/gpu_lidar". Der LiDAR benötigt diese Umwandlung um die Punkte korrekt darzustellen. Im Entity-Tree auf der linken Seite kann man unter „Add" neue Topics visualisieren. Wenn man im Fenster den Reiter „by Topic" auswählt, kann man sich den LaserScan und die PointCloud der Topic /lidar visualisieren oder das RawImage der /cam anzeige lassen. Die Topic /cmd_vel lässt sich mit dem Teleop_Twist_Keyboard ansprechen.
```
ros2 run teleop_twist_keyboard teleop_twist_keyboard
```

## Zusammenfassen mehrerer Bridges

Wenn mehrere Bridges gestartet werden sollen, kann man eine Launch-File als YAML-File schreiben. Ein Beispiel für die Bridge des Kamerabildes hat folgenden Aufbau.
```
- gz_topic_name: "/cam"
  ros_topic_name: "/cam"
  ros_type_name: "sensor_msgs/msg/Image"
  gz_type_name: "gz.msgs.Image"
```

Ein Beispiel mit allen vier Bridges aus dem Kapitel „Umsetzung mit eigener Welt" befindet sich unter folgendem Link:

[gz_project/bridge_runner.yaml](../gz_project/bridge_runner.yaml)

[Main Page](../README.md)
