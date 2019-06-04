Pakete für ROS erstellen
========================

Dieses Mini-Tutorial dient als kurze Einführung in ROS.
Gedacht ist diese Einführung für all jene, die bisher noch keine Erfahrungen mit ROS gemacht haben und einen Einstiegspunkt suchen.

## ROS Umgebung auf den NetBoot Rechnern einrichten ##

Damit alle ROS-Befehle, die im Terminal eingegeben werden, auch funktionieren muss zunächst die passende Datei (`setup.bash`) gesourced werden.
Eine genauere Beschreibung befindet sich im offiziellen [ROS-Wiki](http://wiki.ros.org/ROS/Tutorials/InstallingandConfiguringROSEnvironment). 

``` shell
source /opt/ros/kinetic/setup.bash
```

Dieser Befehl muss jedes Mal, wenn ein neues Terminal geöffnet wird ausgeführt werden.
Da dies aber recht umständlich ist, ist es sinnvoll sich einen entsprechenden Eintrag in der eigenen `~/.bashrc` anzulegen (genaueres dazu siehe unten).

## Catkin Workspace anlegen ##

Als Nächstes wird ein Ordner benötigt, in dem später der zu erstellende Code abgelegt werden kann.
Dieser Ordner wird Catkin-Workspace genannt.
Um einzelne Pakete für ROS zu erstellen wird catkin als Build-System von ROS verwendet (Info siehe [hier](http://wiki.ros.org/catkin/conceptual_overview)).

Die nächsten Befehle legen einen Ordner mit dem Namen `catkin_ws` (der einen Unterordner `src` enthält) in dem eigenen Home-Verzeichnis an.
Danach wird in diesen Ordner gewechselt und dort der Befehl `catkin_make` ausgeführt, der weitere Ordner und Dateien anlegt.
Damit ist dieser Ordner jetzt ein gültiger catkin-Workspace.

``` shell
mkdir -p ~/catkin_ws/src
cd ~/catkin_ws/
catkin_make
```

Damit ROS diesen Ordner als aktuellen Catkin-Workspace erkennt, muss hier auch eine entsprechende Setup-Datei gesourced werden:

``` shell
source devel/setup.bash
```


## ROS Package erstellen ##

Der genaue Ablauf (mit Hintergrund-Informationen) ist [hier](http://wiki.ros.org/ROS/Tutorials/CreatingPackage) nachzulesen.
Um ein Paket zu erstellen wechseln wir in den `src` Ordner in unserem Catkin-Workspace und führen folgenden Befehl aus:

``` shell
catkin_create_pkg beginner_tutorials std_msgs roscpp
```

Dieser Befehl legt ein neues Paket mit dem Namen `beginner_tutorials` an, welches von den Paketen `std_msgs` und `roscpp` abhängig ist.
Anschließend kann das Paket gebaut werden:

``` shell
cd ~/catkin_ws
catkin_make
source ~/catkin_ws/devel/setup.bash
```

