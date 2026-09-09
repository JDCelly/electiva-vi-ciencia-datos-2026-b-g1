# Caso de Estudio: Arquitectura y Analítica de Datos en Spotify

Este repositorio contiene un caso de estudio práctico sobre la gestión, clasificación y flujo de analítica de datos en la plataforma de streaming **Spotify Technology S.A.**

---

## 1. Identificación y Clasificación de Tipos de Datos

Spotify procesa diariamente más de 500 mil millones de eventos de usuarios para alimentar sus motores de recomendación y reportes de negocio. Los datos se clasifican de la siguiente manera:

| Tipo de Dato | Clasificación | Descripción y Formato |
| :--- | :--- | :--- |
| **Historial de transacciones de pago** | **Estructurado** | Registros en bases de datos relacionales (PostgreSQL/MySQL) con esquema rígido: `user_id`, `plan_type`, `amount_usd`, `billing_date`. |
| **Logs de interacción en tiempo real** | **Semiestructurado** | Eventos capturados mediante Apache Kafka en formato JSON con etiquetas clave-valor: `track_id`, `timestamp`, `device_type`, `action`. |
| **Archivos de audio de canciones** | **No Estructurado** | Archivos binarios multimedia (formato Ogg Vorbis/AAC) almacenados en repositorios de objetos sin esquema relacional. |
| **Comentarios de soporte y feedback** | **No Estructurado** | Texto libre escrito por los usuarios en formularios de atención al cliente o encuestas de satisfacción. |

---

## 2. Preguntas de Analítica

### Analítica Descriptiva (Descriptive Analytics)
> **¿Cuáles fueron las 10 canciones más escuchadas por usuarios en América Latina durante el último trimestre y cuántas horas totales de reproducción sumaron?**  
> *Objetivo:* Resumir el comportamiento histórico y el volumen de consumo real dentro de un periodo ya transcurrido.

### Analítica Predictiva (Predictive Analytics)
> **¿Qué probabilidad tiene un usuario de cuenta gratuita de cancelar la aplicación (*churn*) en los próximos 30 días basándose en la reducción de su frecuencia de escucha en las últimas 2 semanas?**  
> *Objetivo:* Utilizar modelos estadísticos y de Machine Learning sobre datos pasados para predecir comportamientos o eventos futuros.

---

## 3. Diagrama del Flujo de Datos (Data Pipeline Architecture)

```text
+-----------------------------------+
|              FUENTE               |
|  - App Móvil / Web (Eventos JSON) |
|  - Subida de Audios de Artistas   |
+-----------------------------------+
                  │
                  ▼
+-----------------------------------+
|          ALMACENAMIENTO           |
|  - Google Cloud Storage (Lake)    |
|  - Cloud Bigtable (NoSQL)         |
+-----------------------------------+
                  │
                  ▼
+-----------------------------------+
|             ANÁLISIS              |
|  - Google BigQuery (Data Wh)      |
|  - Apache Spark / Scikit-Learn    |
+-----------------------------------+
                  │
                  ▼
+-----------------------------------+
|           VISUALIZACIÓN           |
|  - Looker Studio / Tableau        |
|  - Dashboards Ejecutivos          |
+-----------------------------------+
```

---

## 4. Differences Between Descriptive and Predictive Analytics

* **Descriptive analytics** focuses on examining historical data to summarize and understand what has already occurred in the business, such as calculating total monthly active users or overall stream counts.
* **Predictive analytics** utilizes statistical models, data mining, and machine learning techniques on historical data to forecast future outcomes, such as predicting customer churn rate or recommending personalized songs based on user trends.

---

## Referencias y Fuentes Consultadas

1. **Spotify Engineering Blog.** (2020). *Event Delivery at Spotify: Adopting Cloud Pub/Sub*. Recuperado de [engineering.atspotify.com](https://engineering.atspotify.com/)
2. **Google Cloud Customer Stories.** (2021). *How Spotify leverages Google Cloud Platform for big data processing at scale*. Recuperado de [cloud.google.com](https://cloud.google.com/customers/spotify)
3. **DataCamp.** (2022). *Descriptive vs Predictive vs Prescriptive Analytics*. Data Science Resources.
