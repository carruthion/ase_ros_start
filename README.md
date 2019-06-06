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

## Alias in der .bashrc anlegen ##

Damit alle Befehle nicht bei jedem neuen Terminal eingegeben werden müssen, bietet es sich an, ein alias Befehl in der `.bashrc` anzulegen.

``` shell
echo "source /opt/ros/kinetic/setup.bash" >> ~/.bashrc
echo "alias ros='cd ~/catkin_ws && source devel/setup.bash'" >> ~/.bashrc
source ~/.bashrc
```

Jetzt kann mit dem Befehl `ros` direkt in den Catkin-Ordner gewechselt werden.
Zusätzlich werden auch alle nötigen Setup-Dateien gesourced.

## QtCreator als IDE für ROS einrichten ##

Zum Einstieg ist es leichter eine passend eingerichtete IDE zur Programmierung in ROS einzusetzen, darum wird hier die Einrichtung von QtCreator beschrieben.
Die genaue Beschreibung findet sich [hier](https://wiki.ros.org/IDEs#QtCreator) im ROS-Wiki.

Zunächst ist es wichtig, dass QtCreator aus einem Terminal (in dem alle Files schon gesourced wurden) gestartet wird.
Ein passender Starter für die NetBoot Maschienen befindet sich in diesem Repo (`qtcreator.desktop`).
Dieser Starter kann einfach auf den Desktop kopiert werden:

```shell
cp qtcreator.desktop ~/Desktop/
```

Bevor QtCreator verwendet werden kann, muss schon ein catkin-Workspace mit mindestens einem Package existieren.
Jedes Package kann dann später einzeln im QtCreator geöffnet werden.

Ist dies der Fall, so wird der QtCreator über den vorher angelegten Starter geöffnet.
Danach kann auf der Willkommen-Seite 'Open Project' ausgewählt werden.

[Open Project](./images/qt_open.png "Qt Projekt öffnen")

Als Projektdatei wird dann die `CMakeLists.txt` aus dem Ordner `catkin_ws/src/<package_name>` geöffnet.

[Open Cmake](./images/qt_openProject.png "CMakeLists öffnen")

Anschließend wird auf den `Run CMake` Button gedrückt, danach wird der Vorgang mit `Finish` abgeschlossen.

Jetzt sollte das Projekt passend konfiguriert sein, um mit ROS arbeiten zu können.

## Pub/Sub Beispiel ##

Ein Beispiel für einen einfachen Publisher und Subscriber findet sich [hier](http://wiki.ros.org/ROS/Tutorials/WritingPublisherSubscriber%28c%2B%2B%29).
