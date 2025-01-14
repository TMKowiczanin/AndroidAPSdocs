# Настройки xDrip+

Если это еще не сделано, скачайте [xDrip+](https://github.com/NightscoutFoundation/xDrip)

Для передатчиков G6, изготовленных после осени/конца 2018 года, используйте одну из [последних версий ночных сборок xDrip+ ](https://github.com/NightscoutFoundation/xDrip/releases). У этих трансмиттеров новая прошивка и последняя стабильная версия xDrip+ (2019/01/10) с ней не работает.

**На данный момент возникают проблемы с ночными сборками после 2019/05/21, требующими калибровки G6.**

## Основные настройки для всех систем мониторинга

* Правильно вводите адрес локатора вашего сайта (URL) включая **S** в конце http**s**:// (не http://)
   
   напр. https://API_SECRET@imyavashegosaita.herokuapp.com/api/v1/
   
   -> Сэндвич-меню (левый верхний угол домашнего экрана) -> Настройки-> Загрузка в облако-> Синхронизация с Nightscout (REST-API) -> Базовый URL

* Отключите `Автоматическую Калибровку` Если отмечено поле `Автоматическая Калибровка`, одноразово активируйте `Данные загрузки`, а затем удалите флажок для `Автоматической Калибровки` и снова отключите `Скачать данные`, иначе ваши назначения (инсулин & углеводы) будут дважды добавлены в Nightscout.

* Нажмите на `Дополнительные опции`
* Отключите `Загружать назначения` и `Восполнять пропущенные данные`
* Опция `Оповещение о сбоях` также должна быть отключена. Иначе вы будете получать сигнал каждые 5 минут если wifi/мобильная сеть слабые или сервер недоступен.
   
   ![основные настройки xDrip+ 1](../images/xDrip_Basic1.png)
   
   ![основные настройки xDrip+ 2](../images/xDrip_Basic2.png)

* **Взаимодействие с приложениями (Inter-app settings)** (Трансляция) Для пользования AndroidAPS данные должны перенаправляться; вам следует активировать трансляцию xDrip+ в настройках Inter-App.

* Для того чтобы не было расхождений между приложениями, необходимо активировать `Отправлять отображаемое значение Гк`.
* Если вы также активировали `Принимать назначения (Accept treatments)` и трансляцию в AndroidAPS, то xDrip+ получит информацию об инсулине, углеводах и базальной скорости от AndroidAPS и сможет прогнозировать гипогликемию и т. д. более точно.
   
   ![основные настройки xDrip+ 3](../images/xDrip_Basic3.png)

## xDrip+ & Dexcom G6

### Настройки для работы с Dexcom

* Откройте настройки отладки G5/G6 -> Сэндвич-Меню (сверху слева на домашнем экране) -> Настройки -> Настройки отладки G5/G6 ![открыть настройки xDrip+](../images/xDrip_Dexcom_SettingsCall.png)

* Активируйте следующие параметры
   
   * `Использовать коллектор OB1`
   * `Нативный Алгоритм` (важно, если вы хотите использовать супер микроболюс SMB)
   * `Поддержка G6`
   * `Разрешить разъединение OB1`
   * `Разрешить OB1 инициировать сопряжение`
* Все другие опции должны быть отключены
* Настройте уровень предупреждения о низком заряде батареи на 280 (внизу настроек отладки G5/G6)
   
   ![настройки отладки xDrip+ G5/G6](../images/xDrip_Dexcom_DebugSettings.png)

### Профилактические перезапуски не рекомендуются

Автоматическое продление работы сенсоров Dexcom (`упреждающие перезапуски, preemtive restarts`) не рекомендуется, так как может привести к скачкам значений ГК на 9 день после перезапуска.

![xDrip+ после превентивного перезапуска](../images/xDrip_Dexcom_PreemptiveJump.png)

Применение G6 немного сложнее, чем казалось раньше. Для правильного применения необходимо иметь в виду следующие моменты:

* Если вы используете нативные данные с кодом калибровки в xDrip или Spike, в целях безопасности не следует разрешать упреждающий (preemptive) перезапуск датчика.
* Если все же упреждающие перезапуски необходимы, то они должны происходить в то время, когда есть возможность следить за изменениями и при необходимости калибровать. 
* Если вы перезапускаете сенсор, делайте это либо без заводской калибровки для безопасных результатов в дни 11 и 12, либо будьте готовы калибровать и следить за изменениями.
* "Предварительное погружение" (установка сенсора намного раньше его старта в приложении) G6 с заводской калибровкой приведет к отклонениям в данных. Если вы все же делаете "предварительное погружение", то для получения лучших результатов вам, вероятно, придется калибровать сенсор.
* Если вы не планируете отслеживать все возможные отклонения, то лучше вернуться к традиционному режиму калибровки и использовать систему как G5.

Подробнее о деталях и причинах этих рекомендаций читайте [полную статью](http://www.diabettech.com/artificial-pancreas/diy-looping-and-cgm/) опубликованную в Tim Street на [www.diabettech.com](http://www.diabettech.com).

### Первое подключение трансмиттера G6

**Для второго и следующего трансмиттера смотрите [Продление срока работы трансмиттера](../Configuration/xdrip#extend-transmitter-life) ниже.**

* Для передатчиков G6, изготовленных после осени/конца 2018 года, используйте одну из [последних версий ночных сборок xDrip+ ](https://github.com/NightscoutFoundation/xDrip/releases). У этих трансмиттеров новая прошивка и последняя стабильная версия xDrip+ (2019/01/10) с ней не работает.
* Выключите оригинальный ресивер Dexcom (если используете).
* Удерживайте на главном экране xDrip+ иконку капли крови для активации кнопки `Мастер выбора источника ГК`.
* Использование Мастера выбора источника ГК обеспечивает настройки по умолчанию, включая OB1 & нативный режим 
   * Мастер позволит провести начальную настройку.
   * Вам понадобится серийный номер трансмиттера, если вы пользуетесь им впервые.

* Введите серийный номер нового трансмиттера (на упаковке трансмиттера или на его обратной стороне)
   
   ![серийный № трансмиттера Dexcom](../images/xDrip_Dexcom_TransmitterSN.png)

* Вставьте новый сенсор (только при замене)

* Поместите трансмиттер в платформу сенсора
* Выполните Старт сенсора (только при замене) -> В нижней части экрана через несколько минут появится предупреждение о прогреве сенсора `Осталось x,x часов`. -> Если сообщение об оставшемся времени не появляется через несколько минут выполните остановку и новый запуск сенсора.
* Перезапустите коллектор (состояние системы - если не заменяете сенсор}
* Не включайте оригинальный ресивер Dexcom (если им пользуетесь) до появления первых данных в xDrip+.
* Удерживайте на главном экране xDrip+ иконку капли крови для активации кнопки `Мастер выбора источника ГК`.
   
   ![xDrip+ трансмиттер Dexcom 1](../images/xDrip_Dexcom_Transmitter01.png)
   
   ![xDrip+ трансмиттер Dexcom 2](../images/xDrip_Dexcom_Transmitter02.png)
   
   ![xDrip+ трансмиттер Dexcom 3](../images/xDrip_Dexcom_Transmitter03.png)
   
   ![xDrip+ трансмиттер Dexcom 4](../images/xDrip_Dexcom_Transmitter04.png)

### Состояние батареи трансмиттера

* Статус батареи может быть виден в окне состояния системы (сэндвич-меню вверху слева на главном экране)
* Сделайте свайп влево, чтобы увидеть второй экран. ![xDrip+ первый трансмиттер 4](../images/xDrip_Dexcom_Battery.png)

* Точные величины, когда наступает "смерть" трансмиттера из-за низкого заряда батареи, неизвестны. Следующая информация была размещена в сети после "смерти" трансмиттера: дней передачи: 151 напряжение A: 297 напряжение B: 260 Сопротивление: 2391

### Увеличение срока работы трансмиттера

* При продлении срока действия трансмиттера работа сенсора будет остановлена. Поэтому проводить эту манипуляцию следует перед заменой сенсора или быть готовыми к тому, что состоится двухчасовая фаза его прогрева.
* Переключитесь в `инженерный режим`: 
   * нажмите на пиктограмму шприца на главном экране xDrip+ справа
   * затем нажмите на значок микрофона в нижнем правом углу
   * В открывшемся текстовом окне впечатайте "включить инженерный режим" 
   * нажмите "Готово"
   * Если включен Google Speak, вы можете дать голосовую команду: "enable engineering mode" ("включить инженерный режим"). 
* Перейдите в настройки отладки G5 и отметьте `OB1 коллектор`.
* Дайте голосовую команду: “hard reset transmitter”(«жесткий сброс трансмиттера»)
* Голосовая команда будет выполнена при следующем получении данных трансмиттера
* Посмотрите на статус системы (сэндвич-меню -> системный статус) и убедитесь в результате
* Если вы видите сообщение "Состояние телефона: жесткий сброс возможно не произошел", просто перезапустите датчик на втором экране состояния системы и это сообщение должно исчезнуть.
   
   ![xDrip+ Жесткий сброс возможно не произошел](../images/xDrip_HardResetMaybeFailed.png)

* Срок работы трансмиттера будет сброшен до 0 в случае успеха.

### Замена трансмиттера

Для передатчиков G6, изготовленных после осени/конца 2018 года, используйте одну из [последних версий ночных сборок xDrip+ ](https://github.com/NightscoutFoundation/xDrip/releases). У этих трансмиттеров новая прошивка и последняя стабильная версия xDrip+ (2019/01/10) с ней не работает.

* Выключите оригинальный ресивер Dexcom (если используете).
* Остановить сенсор (только при смене сенсора)
   
   Убедитесь, что он действительно остановлен:
   
   На следующем экране "G5/G6 Status" найдите `Queue Items` (`Элементы в очереди`) на полпути вниз - там появится что-то вроде "Остановить Сенсор"
   
   Подождите, пока это происходит - обычно в течение нескольких минут.
   
   -> Как удалить трансмиттер без остановки сенсора, см. видео <https://youtu.be/AAhBVsc6NZo>.
   
   ![xDrip+ Остановка сенсора Dexcom 1](../images/xDrip_Dexcom_StopSensor.png)
   
   ![xDrip+ Остановка сенсора Dexcom 2](../images/xDrip_Dexcom_StopSensor2.png)

* Забыть устройство (в статусе системы)
   
   ![xDrip+ забыть устройство](../images/xDrip_Dexcom_ForgetDevice.png)

* Забыть устройство в настройках BT смартфона (трансмиттер будет изображаться там как DexcomXX; XX - последние две цифры номера серии трансмиттера)

* Удалите трансмиттер (и сенсор при замене)
* Удерживайте на главном экране xDrip+ иконку капли крови для активации кнопки `Мастер выбора источника ГК`.
* Использование Мастера выбора источника ГК обеспечивает настройки по умолчанию, включая OB1 & нативный режим 
   * Мастер позволит провести начальную настройку.
   * Вам понадобится серийный номер трансмиттера, если вы пользуетесь им впервые.
* Введите серийный номер нового трансмиттера.
* Вставьте новый сенсор (только при замене).
* Поместите трансмиттер в платформу сенсора
* Нажмите старт сенсора (только при смене сенсора)
   
   **Рекомендуется подождать около 15 минут между остановкой и запуском нового сенсора(до `Состояние сенсора: Остановлен` на втором экране состояния системы).**

* Перезапустите коллектор (состояние системы - если не заменяете сенсор}

* Не включайте оригинальный ресивер Dexcom (если им пользуетесь) до появления первых данных в xDrip+.
* Удерживайте на главном экране xDrip+ иконку капли крови для активации кнопки `Мастер выбора источника ГК`.
   
   ![xDrip+ трансмиттер Dexcom 1](../images/xDrip_Dexcom_Transmitter01.png)
   
   ![xDrip+ трансмиттер Dexcom 2](../images/xDrip_Dexcom_Transmitter02.png)
   
   ![xDrip+ трансмиттер Dexcom 3](../images/xDrip_Dexcom_Transmitter03.png)
   
   ![xDrip+ трансмиттер Dexcom 4](../images/xDrip_Dexcom_Transmitter04.png)

### Новый сенсор

* Выключите оригинальный ресивер Dexcom (если используете).
* При необходимости остановите сенсор
   
   Убедитесь, что он действительно остановлен:
   
   На следующем экране "G5/G6 Status" найдите `Queue Items` (`Элементы в очереди`) на полпути вниз - там появится что-то вроде "Остановить Сенсор"
   
   Подождите, пока это происходит - обычно в течение нескольких минут.
   
   ![xDrip+ Остановка сенсора Dexcom 1](../images/xDrip_Dexcom_StopSensor.png)
   
   ![xDrip+ Остановка сенсора Dexcom 2](../images/xDrip_Dexcom_StopSensor2.png)

* Протрите контакты (обратная сторона трансмиттера) спиртом и просушите.

* Если вы пользуетесь этой функцией, отключите `Restart Sensor` и `Preemptive restarts` (Сэндвич-меню -> Настройки -> Отладка G5/G6). Если вы пропустите этот шаг и оставите эти функции включенными, новый датчик не будет корректно запущен.
   
   ![xDrip+ профилактический перезапуск](../images/xDrip_Dexcom_Restart.png)

* Запустите сенсор
   
   **Рекомендуется подождать около 15 минут между остановкой и запуском нового сенсора (до `Состояние сенсора: Остановлен` на втором экране состояния системы).**

* Введите время установки
   
   * Для использования нативного режима G6 необходимо подождать 2 часа для прогрева (т.е. время установки -- сейчас).
   * Если вы используете алгоритм xDrip+, то можно установить время более 2 часов назад, чтобы избежать прогрева. Данные могут быть очень неточными. Поэтому это не рекомендуется.
* Введите код сенсора (на снимаемой фольге сенсора) 
   * Сохраните код на случай дополнительной переустановки (новый запуск после удаления трансмиттера)
   * Код также можно найти в логах [xDrip+ ](../Configuration/xdrip#retrieve-sensor-code): Нажмите 3-точечное меню на главном экране xDrip+ и выберите `Просмотр журналов событий`.
* При использовании G6 в "нативном режиме" калибровка не требуется. xDrip+ будет показывать данные автоматически после двухчасового прогрева.
* Не включайте оригинальный ресивер Dexcom (если им пользуетесь) до появления первых данных в xDrip+.
   
   ![xDrip+ Запуск сенсора Dexcom 1](../images/xDrip_Dexcom_SensorStart01.png)
   
   ![xDrip+ Запуск сенсора Dexcom 2](../images/xDrip_Dexcom_SensorStart02.png)

### Получение кода сенсора

* В последних ночных сборках код сенсора отображается в системном статусе (сэндвич-меню вверху слева на главном экране).
* Сделайте свайп влево, чтобы увидеть второй экран.
   
   ![xDrip+ Получение кода сенсора Dexcom 2](../images/xDrip_Dexcom_SensorCode2.png)

* Код сенсора Dexcom можно также найти в логах xDrip+.

* Нажмите 3 точки меню (сверху справа на главном экране)
* Выберите `Просмотр журналов событий` и выполните поиск слова "code"
   
   ![xDrip+ Получение кода сенсора Dexcom](../images/xDrip_Dexcom_SensorCode.png)

## xDrip+; Libre Freestyle

### Специфические настройки Libre

* Откройте настройки Bluetooth -> Сэндвич-меню (сверху слева на главном экране) -> Настройки -> прокрутить вниз -> Менее распространенные настройки -> Настройки Bluetooth
   
   ![xDrip+ настройки Libre Bluetooth 1](../images/xDrip_Libre_BTSettings1.png)

* Активируйте следующие параметры
   
   * `Включить Bluetooth` 
   * `Использовать сканирование`
   * `Всегда обнаруживать сервисы`

* Все другие опции должны быть отключены
   
   ![xDrip+ настройки Libre Bluetooth 2](../images/xDrip_Libre_BTSettings2.png)

### Подключите трансмиттер Libre и запустите сенсор

![xDrip+ запуск трансмиттера Libre & Сенсор 1](../images/xDrip_Libre_Transmitter01.png)

![xDrip+ запуск трансмиттера Libre & Сенсор 2](../images/xDrip_Libre_Transmitter02.png)

![xDrip+ запуск трансмиттера Libre & Сенсор 3](../images/xDrip_Libre_Transmitter03.png)