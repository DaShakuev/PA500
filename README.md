# Модуль для работы с эхолотом PA500

Этот модуль предоставляет простой интерфейс для взаимодействия с эхолотом PA500 через последовательный порт.

## Обзор

Класс `PA500` обрабатывает чтение данных о глубине с устройства PA500 через указанный последовательный порт. Данные поступают в формате `"XXX.XXXm"` (например, `050.000m` для 50 метров) и могут передаваться через сигнал.

## Особенности

- **Настройка последовательного порта:** Имя порта и скорость передачи могут быть заданы при инициализации.
- **Автоматическая обработка данных:** Класс отслеживает входящие данные и обрабатывает их для извлечения информации о глубине.
- **Передача данных через сигнал:** Глубина передаётся через сигнал `sendDistance(float)`.

## Использование

1. Создайте экземпляр класса `PA500`:
   ```cpp
   PA500 sonar("/dev/ttyUSB1", 9600);
2. Подключите сигнал sendDistance(float) к вашему методу обработки данных:
   ```cpp
   connect(&sonar, &PA500::sendDistance, this, &YourClass::handleDepthData);
3. Реализуйте метод в вашем классе для обработки данных о глубине:
   ```cpp
   void YourClass::handleDepthData(float depth) {
     // Обработка данных о глубине, например, запись или отображение
   }
   
## Конструктор

   ```cpp
   PA500(const QString &portName = "/dev/ttyUSB1", int baudrate = 9600);
   ```
**portName**: Имя последовательного порта (по умолчанию: /dev/ttyUSB1).\
**baudrate**: Скорость передачи данных (по умолчанию: 9600).

## Сигнал

**sendDistance(float d)**: Сигнал, который передаёт данные о глубине, когда получены корректные данные. Глубина передаётся как значение типа **float** в метрах.

## Пример

```cpp
#include "PA500.h"

PA500 sonar("/dev/ttyUSB1", 9600);

connect(&sonar, &PA500::sendDistance, [](float depth) {
    qDebug() << "Получена глубина:" << depth << "м";
});
```
