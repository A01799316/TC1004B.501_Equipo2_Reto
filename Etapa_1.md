# TC1004B.501 Implementación de Internet de las Cosas
**Cierre Reto Etapa 1 — Monitoreo Biométrico Remoto**

* **Equipo 2:**
* Nazaret Rayas Chávez (A01798718)
* Miguel Ángel De la Peña Jiménez (A01799316)
* Juan Pablo Amezcua Arroyo (A01799531)
* **Profesor:**
* David Higuera Rosales
* **Institución:**
* Tecnológico de Monterrey, Campus Estado de México

---

## 1. Resumen Ejecutivo del Proyecto
El objetivo principal del proyecto es diseñar, construir e implementar un sistema de adquisición, transmisión, almacenamiento y visualización de datos biomédicos en tiempo real. La solución está orientada al monitoreo remoto de personas de la tercera edad o en situación de vulnerabilidad.

### Variables Monitoreadas
* **Oxigenación sanguínea (SpO₂):** Medida con el sensor MAX30102 mediante señales ópticas.
* **Frecuencia cardíaca:** Estimación de latidos por minuto (LPM) con el sensor MAX30102.
* **Temperatura corporal:** Registrada mediante sensor infrarrojo MLX90614 / DS18B20.
* **Monitoreo del descanso/sueño:** Estimación de movimiento e interrupciones utilizando el acelerómetro/giroscopio MPU6050 combinado con el MAX30102.

---

## 2. Estructura de la Arquitectura de 5 Capas

| Capa | Tecnologías Utilizadas | Descripción y Responsabilidad |
| :--- | :--- | :--- |
| **Percepción** | ESP32, MAX30102, MLX90614, MPU6050 | Adquisición de datos biomédicos y patrones de movimiento desde la muñequera ergonómica. |
| **Red** | Wi-Fi, MQTT (Mosquitto / HiveMQ Cloud) | Conexión del dispositivo wearable a la red y transmisión de telemetría de manera segura. |
| **Procesamiento** | Node-RED, MySQL | Validación de mensajes, cálculo de métricas derivadas, filtrado y almacenamiento con marcas de tiempo. |
| **Aplicación** | Grafana / Node-RED Dashboard | Visualización en tiempo real de signos vitales, tendencias históricas y gestión de alertas. |
| **Negocio** | Seguimiento remoto y protocolos de atención | Soporte a familiares y personal médico para supervisión continua y respuesta rápida ante emergencias. |

---

## 3. Estructura Sugerida para el Repositorio

```
/
├── README.md         # Visión general del proyecto, arquitectura y guía rápida
├── docs/             # Diagramas de arquitectura, esquemáticos de hardware y manuales
├── hardware/         # Modelos 3D del wearable (housing) y esquemáticos de conexiones
├── firmware/         # Código fuente para el ESP32 (Arduino / ESP-IDF)
│   ├── src/          # Lectura de sensores (MAX30102, MPU6050, MLX90614)
│   └── include/      # Librerías y configuraciones Wi-Fi/MQTT
├── backend/          # Flujos de Node-RED, scripts de base de datos MySQL
└── dashboard/        # Dashboards exportados de Grafana (archivos JSON)
```

## 4. Avances Recientes del Proyecto (Etapa 1)
* **Configuración del Repositorio y Entorno:** Inicialización del repositorio en GitHub con estructura básica y licencias.
* **Pruebas de Hardware e Integración de Sensores:** Lectura estable de los sensores MAX30102 y MLX90614 mediante el bus I2C en el ESP32.
* **Publicación y Protocolo MQTT:** Transmisión de datos hacia HiveMQ Cloud mediante mensajes JSON estandarizados con reconexión automática.
* **Servidor de Procesamiento e Histórico:** Despliegue de Node-RED vinculado a MySQL para almacenamiento estructurado con marca de tiempo.
* **Prototipado del Dashboard:** Tablero preliminar en Grafana con gráficas temporales y umbrales de alerta.

---

## 5. Siguientes Pasos
1. Finalizar el algoritmo de procesamiento de datos del MPU6050 para la detección de periodos de descanso.
2. Optimizar el consumo de energía del ESP32 mediante modos de reposo (*Deep Sleep*).
3. Diseñar e imprimir en 3D la carcasa final utilizando filamento flexible hipoalergénico.
