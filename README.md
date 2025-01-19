
# Base de Datos Fundamentos y Infraestructuras

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

## **Aplicación Disponible en Google Cloud**

La aplicación está desplegada en Google Cloud y puedes acceder a la API Flask directamente desde la siguiente URL:

### **URL de la API Flask**
```bash
http://34.55.124.237:5001/flights/delays/predict_kafka
```
![image](https://github.com/user-attachments/assets/e3b9a291-991a-4810-8b1b-e066e90d6aed)
![image](https://github.com/user-attachments/assets/8dc1dc67-9ecb-4c49-919b-baddd72e318b)


Prueba la funcionalidad de predicción directamente con el siguiente comando `curl` desde tu terminal:
```bash
curl http://34.55.124.237:5001/flights/delays/predict_kafka
```

---

## **Servicios Disponibles Localmente**

Si decides ejecutar el proyecto localmente, estos serán los servicios disponibles:

### Flask API
La API Flask estará disponible en:
```bash
http://<IP_DEL_SERVIDOR>:5001
```

Prueba la funcionalidad de predicción localmente con:
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

# **Instrucciones para Desplegar la Práctica en Kubernetes**

### Acceder al directorio donde se encuentran los archivos YAML 
```bash
cd /k8
```
### Iniciar Minikube con Docker como driver
```bash
minikube start --driver=docker
```
### Verificar el estado de Minikube
```bash
minikube status
```
### Aplicar los archivos YAML desde el directorio actual
Es recomendable aplicar los recursos YAML de uno en uno y en un orden específico para evitar errores relacionados con dependencias entre servicios. Sigue el siguiente orden recomendado: **zookeeper**, **kafka**, **flask**, **mongo**, **spark-master**, y finalmente **spark-worker**.

```bash
# Aplicar el Deployment y Service de Zookeeper
kubectl apply -f zookeeper-deployment.yaml
kubectl apply -f zookeeper-service.yaml

# Aplicar el Deployment y Service de Kafka
kubectl apply -f kafka-deployment.yaml
kubectl apply -f kafka-service.yaml

# Aplicar el Deployment y Service de Flask
kubectl apply -f flask-deployment.yaml
kubectl apply -f flask-service.yaml

# Aplicar el Deployment y Service de MongoDB
kubectl apply -f mongo-deployment.yaml
kubectl apply -f mongo-service.yaml

# Aplicar el Deployment de mongo-seed para importar datos en la base de datos MongoDB.
kubectl apply -f mongo-seed-deployment.yaml

# Aplicar el Deployment y Service de Spark Master
kubectl apply -f spark-master-deployment.yaml
kubectl apply -f spark-master-service.yaml

# Aplicar el Deployment y Service de Spark Worker
kubectl apply -f spark-worker-deployment.yaml
kubectl apply -f spark-worker-service.yaml

```
### Exponer un Servicio Localmente con Port Forward

Este comando permite redirigir el tráfico desde un puerto local hacia un servicio en Kubernetes. Es útil para acceder a un servicio dentro del clúster sin necesidad de exponerlo públicamente.

```bash
kubectl port-forward svc/flask 5001:5001

```

### Verificar los recursos desplegados (Pods, Deployments, Services)
```bash
kubectl get pods,deployments,services
```
### Ver los logs de un Pod específico
```bash
kubectl logs <NOMBRE_DEL_POD>
```
### Eliminar todos los recursos desplegados
```bash
kubectl delete all --all
```
### Detener Minikube una vez finalizado
```bash
minikube stop
```




