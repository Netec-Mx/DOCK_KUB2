# Nombre del laboratorio 

## Objetivo de la práctica:
Al finalizar la práctica, serás capaz de:
- Configurar el entorno
- de trabajo asegurándose de que Docker esté instalado y funcionando correctamente.
- Ejecutar un contenedor NGINX, mapeando los puertos entre el contenedor y el host para garantizar la accesibilidad del servicio.
- Identificar y analizar los puertos utilizados por los contenedores, facilitando la resolución de conflictos de red y la configuración de firewalls y enrutamientos.

## Instrucciones 

### Tarea 1. Create aplicacion de node js
Paso 1. crea el una carpeta que se llame "mi-aplicacion" y inicializa el proyecto e instala express
```bash
npm init -y
npm install express
```
![cap7_create_project.png](../images/Capitulo%207/cap7_create_project.png)

Paso 2. Crea un archivo llamado "index.js" y agrega el siguiente código
```javascript
const express = require('express');
const app = express();
const port = 3000;
app.get('/', (req, res) => {
res.send('Hola Mundo desde Node.js!');
});
app.listen(port, () => {
console.log(`Aplicación escuchando en el puerto ${port}`);
});
```

Paso 3. Crear Dockerfile para contenerizar el servicio
```bash
FROM node:14
WORKDIR /usr/src/app
COPY package*.json ./
RUN npm install
COPY . .
EXPOSE 3000
CMD ["node", "index.js"]
```
![cap7_create_docker.png](../images/Capitulo%207/cap7_create_docker.png)

### Tarea 2. Subir imagen a docker hub
Paso 1. para crear una cuenta en docker hub, visita [Docker Hub](https://hub.docker.com/)

![cap7_login_docker_hub.png](../images/Capitulo%207/cap7_login_docker_hub.png)


Paso 2. Crear un repositorio en docker hub

![cap7_create_repo.png](../images/Capitulo%207/cap7_create_repo.png)


Paso 3. agrgar nombre de usuario y nombre de repositorio <netec_docker_repo>

![cap7_create_repo2.png](../images/Capitulo%207/cap7_create_repo2.png)

![Screenshot 2025-03-21 at 11.32.43 PM.png](../images/Capitulo%207/Screenshot%202025-03-21%20at%2011.32.43%E2%80%AFPM.png)

Paso 4. Crear imagen de docker
```bash
docker build -t daniel0223/netec_docker_repo .
```
![cap7_create_img.png](../images/Capitulo%207/cap7_create_img.png)

Paso 5. Subir imagen a docker hub
```bash
docker push daniel0223/netec_docker_repo
```

![cap7_push_img.png](../images/Capitulo%207/cap7_push_img.png)

Paso 6. Verificar que la imagen se haya subido correctamente

![cap7_img_docker_hub.png](../images/Capitulo%207/cap7_img_docker_hub.png)

Paso 7. Crear contenedor con la imagen de docker
```bash
docker run -d -p 3000:3000 daniel0223/netec_docker_repo
```
![cap7_create_container.png](../images/Capitulo%207/cap7_create_container.png)

Paso 8. Verificar que el contenedor se haya creado correctamente

![cap7_container.png](../images/Capitulo%207/cap7_container.png)

### Tarea 3. Desplegar en Kubernetes

Paso 1. Crear un archivo de despliegue de kubernetes
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: mi-aplicacion-node
spec:
  replicas: 2
  selector:
    matchLabels:
      app: mi-aplicacion-node
  template:
    metadata:
      labels:
        app: mi-aplicacion-node
    spec:
      containers:
        - name: mi-aplicacion-node
          image: daniel0223/netec_docker_repo
          ports:
            - containerPort: 3000
```

Paso 2. Desplegar la aplicación:
```bash
kubectl apply -f deployment.yaml
```
![cap7_execue_k8s.png](../images/Capitulo%207/cap7_execue_k8s.png)

Paso 3. exponer aplicacion
```yaml
kubectl expose deployment mi-aplicacion-node --type=LoadBalancer --port=3000
```
![cap7_expo_app.png](../images/Capitulo%207/cap7_expo_app.png)

Paso 4. Verificar que el servicio se haya creado correctamente
```bash
kubectl get svc
```

### Resultado esperado


![cap7_refact.png](../images/Capitulo%207/cap7_refact.png)
