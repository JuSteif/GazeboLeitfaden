# Bewegen von Modellen

## Anpassung der SDF-File

Um ein Modell bewegen zu können, wird ein Plugin unter dem model-Tag hinzugefügt. Für diesen Schritt wird das Robotermodell aus dem Kapitel „Modelle" benötigt.
```
<plugin filename="gz-sim-diff-drive-system" name="gz::sim::systems::DiffDrive">
    <left_joint>left_wheel_joint</left_joint>
    <right_joint>right_wheel_joint</right_joint>
    <wheel_separation>1.2</wheel_separation>
    <wheel_radius>0.4</wheel_radius>
    <odom_publish_frequency>1</odom_publish_frequency>
    <topic>cmd_vel</topic>
</plugin>

```

In diesem Beispiel wird ein Achsdifferentialantrieb verwendet. Dieser benötigt die beiden Joints, an denen die Räder sitzen, und deren Umfang für die Simulation der Achse. Der Antrieb kann über die Topic /cmd\_vel gesteuert werden. Dabei handelt es sich um eine Twist-Message, die analog zur ROS-Topic verwendet wird.

Das Robotermodell aus dem Kapitel „Modelle" wird um das Differential erweitert:

[ModellLinksJointsDiff.xml](../snippets/ModellLinksJointsDiff.xml)

## Topics und Messages der Bewegung

Eine beispielhafte Welt mit dem Roboter befindet sich unter folgendem Link:

[moving_roboter.sdf](../demo_worlds/moving_roboter.sdf)

Beim Start der Welt wird mit dem Drücken des Playbuttons die Simulation gestartet.
```
gz sim moving_roboter.sdf
```

In einem neuen Terminal wird zum Bewegen des Roboters der folgende Befehl aufgerufen:
```
gz topic -t "/cmd_vel" -m gz.msgs.Twist -p "linear: {x: 0.5}, angular: {z: 0.05}"
```

Der Roboter fährt eine Kreisbahn. Dabei haben die Parameter folgende Bedeutung:

-t: Die Topic, die angesprochen wird

-m: Der Typ der Nachricht

-p: Die Daten, die gesendet werden
