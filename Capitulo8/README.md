# Nombre del laboratorio 

## Objetivo de la práctica:

- Comprender el concepto de namespaces en Kubernetes y su importancia en la organización y gestión de recursos dentro de un clúster.
- Aprender a crear y utilizar namespaces para desplegar y administrar diferentes tipos de objetos en Kubernetes.
- Implementar recursos clave de Kubernetes, incluyendo ReplicaSets, Jobs, DaemonSets y Deployments, dentro de namespaces específicos.

## Duración aproximada:
- 60 minutos.


## Instrucciones 

- Crear un nuevo namespace en Kubernetes, aprendiendo a segmentar el clúster en espacios lógicos para una mejor organización y seguridad.
- Desplegar un objeto de tipo ReplicaSet en el namespace recién creado, aprendiendo a gestionar y escalar aplicaciones en Kubernetes.
- Crear un nuevo namespace en Kubernetes, aprendiendo a segmentar el clúster en espacios lógicos para una mejor organización y seguridad.
### Tarea 1. Crear proyecto Node JS 

Paso 1. Crear un una carpeta con el nombre "mi-proyecto-nodejs" inicializar el proyecto 

```bash
mkdir mi-proyecto-nodejs
cd mi-proyecto-nodejs
npm init -y
```
![cap8_start_node.png](../images/Capitulo%208/cap8_start_node.png)

Paso 2. Crear el archjivo index.js y agregar el siguiente código

```javascript
const express = require('express');
const app = express();
const PORT = process.env.PORT || 3000;
app.get('/', (req, res) => {
res.send('Hola Mundo desde Node.js!');
});
app.listen(PORT, () => {
console.log(`Servidor corriendo en puerto ${PORT}`);
});
```

Paso 3. Instalar express

```bash
npm install express
```
![cap8_start_express.png](../images/Capitulo%208/cap8_start_express.png)

Paso 4. Crear archivo Dockerfile

```Dockerfile
FROM node:14
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
EXPOSE 3000
CMD ["node", "index.js"]
```
![cap8_docker_file.png](../images/Capitulo%208/cap8_docker_file.png)

Paso 5. subir imagen a docker hub

```bash
docker build -t daniel0223/netec_docker_repo:v1 .
docker push daniel0223/netec_docker_repo:v1
```
![cap8_up_docker_hub.png](../images/Capitulo%208/cap8_up_docker_hub.png)


### Tarea 2. Desplegar en Kubernetes
Paso 1. crear el namespace con el nombre namespace.yaml

```yaml
apiVersion: v1
kind: Namespace
metadata:
  name: mi-namespace
```
![cap8_namespace.png](../images/Capitulo%208/cap8_namespace.png)

Paso 2. aplicar y crear el namespace

```bash
kubectl apply -f namespace.yaml
```
![cap8_comand_namespace.png](../images/Capitulo%208/cap8_comand_namespace.png)

Paso 3. Crear el archivo deployment.yaml

```yaml
# deployment.yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: mi-deployment
  namespace: mi-namespace
spec:
  replicas: 3
  selector:
    matchLabels:
      app: mi-app-nodejs
  template:
    metadata:
      labels:
        app: mi-app-nodejs
    spec:
      containers:
        - name: mi-app-nodejs
          image: daniel0223/netec_docker_repo:v1
          ports:
            - containerPort: 3000
```
![cap8_deployment_yml.png](../images/Capitulo%208/cap8_deployment_yml.png)

Paso 4. Aplicar el deployment

```bash
kubectl apply -f deployment.yaml
```
![cap8_deployment_yml_exec.png](../images/Capitulo%208/cap8_deployment_yml_exec.png)

Paso 5.  Creacion de ReplicaSet y ejecicion 

```yaml
# replicaset.yaml
apiVersion: apps/v1
kind: ReplicaSet
metadata:
  name: mi-replicaset
  namespace: mi-namespace
spec:
  replicas: 3
  selector:
    matchLabels:
      app: mi-app-nodejs
  template:
    metadata:
      labels:
        app: mi-app-nodejs
    spec:
      containers:
        - name: mi-app-nodejs
          image: daniel0223/netec_docker_repo:v1
          ports:
            - containerPort: 3000

```

```bash
kubectl -f replicaset.yaml apply
```

![cap8_k8s_k8s.png](../images/Capitulo%208/cap8_k8s_k8s.png)



Paso 6. Creacion StatefulSet y ejecicion

```yaml
# statefulset.yaml
apiVersion: apps/v1
kind: ReplicaSet
metadata:
  name: mi-replicaset
  namespace: mi-namespace
spec:
  replicas: 3
  selector:
    matchLabels:
      app: mi-app-nodejs
  template:
    metadata:
      labels:
        app: mi-app-nodejs
    spec:
      containers:
        - name: mi-app-nodejs
          image: daniel0223/netec_docker_repo:v1
          ports:
            - containerPort: 3000

```

```bash
kubectl -f statefulset.yaml apply
```

Paso 7. Creacion DaemonSet, y ejecicion 
```yaml
# daemonset.yaml
apiVersion: apps/v1
kind: DaemonSet
metadata:
  name: mi-daemonset
  namespace: mi-namespace
spec:
  selector:
    matchLabels:
      app: mi-app-nodejs
  template:
    metadata:
      labels:
        app: mi-app-nodejs
    spec:
      containers:
        - name: mi-app-nodejs
          image: daniel0223/netec_docker_repo:v1
          ports:
            - containerPort: 3000
```

```bash
kubectl -f statefulset.yaml apply
```
![cap8_deamonSet.png](../images/Capitulo%208/cap8_deamonSet.png)


Paso 8. verificar configuracion completa
```yaml
kubectl get all -n mi-namespace
```
![cap8_final.png](../images/Capitulo%208/cap8_final.png)
### Resultado esperado


![cap8_final.png](../images/Capitulo%208/cap8_final.png)
