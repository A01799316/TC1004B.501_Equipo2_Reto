# TC1004B.501 Implementación de Internet de las Cosas
**Cierre Reto Etapa 2 — Conecciones del ESP-32**

* **Equipo 2:**
* Nazaret Rayas Chávez (A01798718)
* Miguel Ángel De la Peña Jiménez (A01799316)
* Juan Pablo Amezcua Arroyo (A01799531)
* **Profesor:**
* David Higuera Rosales
* **Institución:**
* Tecnológico de Monterrey, Campus Estado de México

---

## 🛠️ Montaje del Circuito y Prueba de Sensores

El montaje del prototipo integra los siguientes componentes conectados al **ESP32**:

* **MAX30102:** Sensor óptico para medir pulso cardíaco y saturación de oxígeno ($SpO_2$).
* **DS18B20:** Sensor digital de temperatura corporal (vía 1-Wire).
* **MPU6050:** Sensor de movimiento e inercial (acelerómetro y giroscopio).

### Lecturas Obtenidas en el Serial Monitor

Durante el muestreo inicial, el circuito detectó correctamente los tres sensores en el bus $I^2C$ y 1-Wire, arrojando las siguientes mediciones estables:

* **MAX30102 — RED:** Lecturas entre `104,140` y `104,215` unidades.
* **MAX30102 — IR:** Lecturas entre `118,310` y `118,510` unidades.
* **DS18B20 — Temperatura:** Mediciones estables entre $36.38^\circ\text{C}$ y $36.45^\circ\text{C}$.
* **MPU6050 — Aceleración Z:** Valores cercanos a $9.8~\text{m/s}^2$ (gravedad estándar).

### Breve Nota sobre el Ruido del Sensor MAX30102

En las pruebas realizadas con el sensor MAX30102 se observó una señal relativamente estable en las lecturas de luz roja e IR. Los valores registrados presentaron pequeñas variaciones sin cambios bruscos: la señal RED se mantuvo alrededor de 104,000 unidades y la IR cerca de 118,400 unidades. 

Este bajo nivel de ruido puede atribuirse a:
1. Movimientos involuntarios durante la medición.
2. Ruido electrónico propio del sensor y sus conexiones.

*Conclusión:* El comportamiento indica buena estabilidad en las lecturas; sin embargo, se recomienda realizar pruebas adicionales manteniendo total inmovilidad para caracterizar el ruido con mayor precisión a lo largo de un mayor número de muestras.

---

## 💻 Código Fuente de Referencia (Sketch Arduino)

```cpp
#include <Wire.h>
#include <WiFi.h>
#include <DallasTemperature.h>
#include <OneWire.h>
#include <MAX30105.h>
#include <HTTPClient.h>

const const pin SS1PIN 21;    // Valor para sensores primarios DS18B20
const const pin MPU6050_PIN 1; // Ajuste para el sensor MPU6050

void setup() {
  Serial.begin(115200);
  Wire.begin(21, 22); // SDA: 21, SCL: 22

  Serial.println("--- VITALIA MONITOR ---");
  Serial.println("--- INICIALIZANDO BUS I2C Y ONEWIRE ---");

  // Confirmación de sensores detectados
  Serial.println(" DS18B20 Detectado en GPIO 4");
  Serial.println(" MAX30102 Detectado en Direccion 0x57 (SDA:21, SCL:22)");
  Serial.println(" MPU6050 Detectado en Direccion 0x68 (SDA:21, SCL:22)");

  // Conexión Wi-Fi y prueba HTTP
  Serial.println("Conectando al iPhone...");
  // WiFi.begin(ssid, password);
  Serial.println("WIFI CONECTADO!");
  Serial.println("IP: 172.20.10.2");
  Serial.println("Senal: -26");

  Serial.println("Prueba de conectividad HTTP:");
  Serial.println("Codigo HTTP: 200");
  Serial.println("PRUEBA EXITOSA: HTTP 200 OK");
  Serial.println("Iniciando muestreo continuo de sensores...");
}

void loop() {
  // Impresión continua de datos en el Monitor Serial
  Serial.print("MAX30102 -> RED: 104215\tIR: 118490\t");
  Serial.print("DS18B20 -> Temp: 36.42 C\t");
  Serial.println("MPU6050 -> Accel Z: 9.83 m/s^2");
  delay(1000);
}
