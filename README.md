
# BDFI - Proyecto Base

Este proyecto implementa un sistema para manejar datos y flujos utilizando contenedores Docker, Kafka, Spark, Flask, MongoDB, y otras herramientas relacionadas.

---

## **Requisitos**

Asegúrate de que los siguientes programas estén instalados:

- [Docker](https://docs.docker.com/get-docker/)
- [Docker Compose](https://docs.docker.com/compose/install/)
- Git

---

## **Instrucciones para Desplegar**

Sigue estos pasos para levantar todos los servicios del proyecto.

### **1. Clona el repositorio**

```bash
git clone https://github.com/luciaacs/bdfi.git
cd bdfi
```

### **2. Construye las imágenes de Docker**

```bash
docker-compose build
```

### **3. Inicia los contenedores**

```bash
docker-compose up -d
```

> Esto levantará los servicios de Kafka, Spark, Flask, MongoDB, y cualquier otro definido en el archivo `docker-compose.yml`.

---

## **Servicios Disponibles**

### Flask API
La API Flask estará disponible en:
```bash
http://<IP_DEL_SERVIDOR>:5001
```

Prueba la funcionalidad de predicción:
```bash
curl http://<IP_DEL_SERVIDOR>:5001/flights/delays/predict_kafka
```

### Kafka
Kafka estará escuchando en el puerto `9092`.

### MongoDB
MongoDB estará disponible en el puerto `27017`.

---

## **Comandos Útiles**

### Ver los contenedores en ejecución:
```bash
docker ps
```

### Detener todos los contenedores:
```bash
docker-compose down
```

### Ver logs de un contenedor específico:
```bash
docker logs <nombre_o_id_del_contenedor>
```

### Acceder a un contenedor:
```bash
docker exec -it <nombre_o_id_del_contenedor> bash
```

---

## **Estructura del Proyecto**

- `docker-compose.yml`: Configuración de los servicios Docker.
- `web/`: Código fuente de la API Flask.
- `kafka/`: Configuración para Kafka.
- `spark/`: Configuración para Spark.
- `mongo/`: Configuración para MongoDB.

---
