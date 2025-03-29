# Nombre del laboratorio 

## Objetivo de la práctica:
Al finalizar la práctica, serás capaz de:
- Crear una aplicación Node.js con Express y ejecutarla localmente.
- Construir y subir una imagen Docker de la aplicación a Docker Hub.
- Desplegar la aplicación en Kubernetes utilizando Deployment, Service e Ingress.

## Duración aproximada:
- 60  minutos.


## Instrucciones 

### Tarea 1. Crear una Aplicación Node.js


Paso 1. crear una carpeta llamada lab12 y dentro de esta parpeta crear un proyecto de express

```bash
npm init -y
npm install express
```

Paso 2. Crear un archivo index.js y agregar el siguiente código

```javascript
const express = require('express');
const app = express();
const port = 3000;

app.get('/', (req, res) => {
  res.send('Practica 12!');
});

app.listen(port, () => {
  console.log(`Aplicación escuchando en el puerto ${port}`);
});
```

Paso 3. Crear un archivo Dockerfile y agregar el siguiente código

```Dockerfile
# Usa la última versión de Node.js como base
FROM node:latest  

# Establece el directorio de trabajo dentro del contenedor
WORKDIR /usr/src/app  

# Copia solo los archivos de dependencias para aprovechar la caché de Docker
COPY package*.json ./  

# Instala las dependencias
RUN npm install  

# Copia el resto de los archivos del proyecto
COPY . .  

# Expone el puerto 3000 para acceder al contenedor
EXPOSE 3000  

# Comando de inicio de la aplicación
CMD ["node", "server.js"]

```

Paso 4. Crear una imagen de Docker con el siguiente comando

```bash
docker build -t daniel0223/netec_docker_repo:v12 .
```
![Cao12_star_img.png](../images/Capitulo%2012/Cao12_star_img.png)
Paso 5. Subir la imagen a Docker Hub

```bash
docker push daniel0223/netec_docker_repo:v12 
```
![Cap12_push_docker_hub.png](../images/Capitulo%2012/Cap12_push_docker_hub.png)


### Tarea 2. Crear los objetos Deployment y Service
Paso 1. Crear un archivo deployment.yaml y agregar el siguiente código

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: practica12-deployment
spec:
  replicas: 3
  selector:
    matchLabels:
      app: practica12
  template:
    metadata:
      labels:
        app: practica12
    spec:
      containers:
        - name: practica12
          image: daniel0223/netec_docker_repo:v12
          ports:
            - containerPort: 3000
```
![Screenshot 2025-03-22 at 11.57.21 PM.png](../images/Capitulo%2012/Screenshot%202025-03-22%20at%2011.57.21%E2%80%AFPM.png)

Paso 2 Crear el deploy 

```bash
kubectl apply -f deployment.yaml
```
![cap12_server__impl.png](../images/Capitulo%2012/cap12_server__impl.png)
Paso 3 . Crear el archivo service.yaml

```yaml
apiVersion: v1
kind: Service
metadata:
  name: practica12
spec:
  type: LoadBalancer
  selector:
    app: practica12
  ports:
    - protocol: TCP
      port: 8081
      targetPort: 3000
```
![Cap12_push_docker_hub.png](../images/Capitulo%2012/Cap12_push_docker_hub.png)


Paso 4. Crear el servicio

```bash
kubectl apply -f service.yaml
```
![cap12_service.png](../images/Capitulo%2012/cap12_service.png)


Paso 5. crear el ingress con Nginx

```yaml
kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/main/deploy/static/provider/cloud/deploy.yaml
```
![cap12_dowload.png](../images/Capitulo%2012/cap12_dowload.png)



Paso 6. Crear el archivo ingress-rules.yaml

```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: practica12-ingress
  annotations:
    kubernetes.io/ingress.class: nginx
spec:
  ingressClassName: nginx
  rules:
    - host: practica12.example.com
      http:
        paths:
          - path: /
            pathType: ImplementationSpecific
            backend:
              service:
                name: practica12
                port:
                  number: 8081
```
![cap12_ingress.png](../images/Capitulo%2012/cap12_ingress.png)



### Resultado esperado
![cap12_final.png](../images/Capitulo%2012/cap12_final.png)