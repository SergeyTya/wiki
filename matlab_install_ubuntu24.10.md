# Устанавливаем Matlab r2024a на ubuntu 24.10 (01.12.2024)

Информация о совместимости версий
https://www.mathworks.com/support/requirements/platform-road-map.html


### 1. Запуск установщика

Качаем установочный образ https://rutracker.org/forum/viewtopic.php?t=6511869 монтируем образ

Если установщик не запускается с ошибкой
```
terminate called after throwing an instance of 'std::runtime_error'
  what():  Failed to launch web window with error: Unable to launch the MATLABWindow application. The exit code was: 1
Aborted
```
 Копируем установочные файлы в папку на диске и выполняем

```
cd <matlab-installation-dir>
cd sys/os/glnxa64
mkdir exclude
mv libstdc++.so.6 libstdc++.so.6.0.28 exclude


cd <matlab-installation-dir>
cd bin/glnxa64
mkdir exclude
mv libstdc++.so.6* exclude/
```

https://github.com/mohammaddehnavi/mohi-docs/blob/main/Matlab/README.md#fix-install-matlab

### 2 После установки 

Если Simulink не запускается с ошибкой
```
GLIBCXX_3.4.29' not found
```
В папке с дистрибутивом выполняем

```
mkdir /sys/os/glnxa64/exclude
cd /sys/os/glnxa64
mv libstdc++.so.6* exclude
```
в папке exclude должно появится два файла
```
libstdc++.so.6  
libstdc++.so.6.0.28
```

### 3. Запуск

Создаем ярлык на рабочем столе 

```
[Desktop Entry]
Version=x.y
Name=Matlab r2024
Exec=/home/sergey/MATLAB/R2024a/bin/matlab -softwareopengl -desktop
Icon=/home/sergey/MATLAB/matlab.png
Terminal=false
Type=Application
Categories=Utility;Application;

```
https://www.mathworks.com/matlabcentral/answers/20-how-do-i-make-a-desktop-launcher-for-matlab-in-linux


### 4. Особенности 

4.1 Для устранения ошибки Out of memory можно использовать

```
ulimit -n 10000
```

4.2 Игнорируем предупреждение 

```
Gtk-Message: 10:32:31.466: Failed to load module "canberra-gtk-module"
```
https://www.mathworks.com/matlabcentral/answers/472134-gtk-message-10-32-31-466-failed-to-load-module-canberra-gtk-module

4.3 Для устранения проблем с CEF можно использовать 

```
export LD_LIBRARY_PATH=/usr/local/MATLAB/R2023b/cefclient/sys/os/glnxa64
```

https://ww2.mathworks.cn/matlabcentral/answers/364551-why-is-matlab-unable-to-run-the-matlabwindow-application-on-linux

