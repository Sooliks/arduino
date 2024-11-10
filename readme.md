### Arduino HID mouse
## RU

- Для начала приобритите `Arduino Leonardo R3 ATMEGA32U4`, `ARDUINO USB HOST SHIELD` и паяльник если его нет.
<br></br>
- Скачайте и установите [Arduino IDE](https://www.arduino.cc/en/software).
<br></br>
- Скачайте и распакуйте архив скачанный с репозитория в `C:\Users\ваше_имя_пользователя\Documents\Arduino\HID_Arduino` или если у вас мышка logitech G-серии скачайте [this](https://github.com/SunOner/usb-host-shield-mouse_for_ai_aimbot) и распакуйте скачанный архив с репозитория в `C:\Users\ваше_имя_пользователя\Documents\Arduino\hidmousereport`
<br></br>
- Скачайте и распакуйте [этот](https://github.com/felis/USB_Host_Shield_2.0/releases/tag/1.6.2) архив и распакуйте в `C:\Users\ваше_имя_пользователя\Documents\Arduino\libraries\USB_Host_Shield_2.0-1.6.2`
<br></br>
- Спаяйте на плате 3 контакта чтобы получилось как на изображении. (Для увеличения напряжения)
	- ![](https://github.com/SunOner/HID_Arduino/blob/main/docs/media/host_shield_board.gif)
<br></br>
- Откройте файл `C:\Users\ваше_имя_пользователя\Documents\Arduino\HID_Arduino\HID_Arduino.ino` или `C:\Users\ваше_имя_пользователя\Documents\Arduino\hidmousereport\hidmousereport.ino` если у вас мышка logitech G-серии
<br></br>
- Подключите плату `ARDUINO USB HOST SHIELD` к `Arduino Leonardo` и подключите к ПК `ARDUINO`.
<br></br>
1. Выберите устройство
2. Напишите в поисковике "leonardo"
3. Выберите устройство
4. Выберите порт к которому подключено устройство
5. Загрузите программу на устройство
![](https://github.com/SunOner/HID_Arduino/blob/main/docs/media/host_shield_ide_select_board_en.png)
<br></br>
- Подключите мышь к host shield.
<br></br>
- Проверьте мышь на работоспособность. Если всё работает как нужно то у вас всё получилось и повезло с моделью мыши. Но если что-то работает не правильно вам дальше. (Для logitech G-серии дальнейшие действия не требуются.)
<br></br>
- Откройте в блокноте файл `C:\Users\ваше_имя_пользователя\Documents\Arduino\libraries\USB_Host_Shield_2.0-1.6.2\settings.h`
<br></br>
- Измените `#define ENABLE_UHS_DEBUGGING 0` на `#define ENABLE_UHS_DEBUGGING 1`
<br></br>
- Загрузите скрипт на устройство.
<br></br>
- В Arduino ide откройте вкладку Tools->Serial Monitor.
	- ![](https://github.com/SunOner/HID_Arduino/blob/main/docs/media/serial_monitor.png)
<br></br>
- Выберите 9600 baud
	- ![](https://github.com/SunOner/HID_Arduino/blob/main/docs/media/baud.png)
<br></br>
- Вы должны увидеть данные которые пересылает мышка на host shield.
<br></br>
- Переключитесь на вкладку `hidcustom.h` и взгляните на структуру `struct MYMOUSEINFO`
<br></br>
- В моем случаи это выглядит так:
	- ![](https://github.com/SunOner/HID_Arduino/blob/main/docs/media/struct.png)
<br></br>
- У меня в начале пересылаются байты кнопок мыши, но у вас может пересылаться что-то другое, к примеру координаты мыши по X-горизонтали.
<br></br>
- Тогда вам нужно будет изменить структуру `MYMOUSEINFO` так что-бы в начале стояла переменная `uint16_t dX;`.
<br></br>
- В некоторых случаях нужно будет изменить `uint16_t` по `оси X` или `uint16_t` по `оси Y` на `uint8_t` .
<br></br>
- Проделайте это со всеми выходными данными и приведите структуру в норму.
<br></br>
- Не забудьте отключить после всех проделанных действий `#define ENABLE_UHS_DEBUGGING 0` в `settings.h`.
