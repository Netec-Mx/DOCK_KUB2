# Ejericios de práctica

## Objetivo de la práctica:
- El estudiante entendera desde una manera practica como interactuar con kubernetes
- El estudiante podra realizar operaciones basicas en kubernetes

## Duración aproximada:
- 20 minutos.


## Instrucciones 
Comprender cómo utilizar labels y selectors para organizar y seleccionar recursos en Kubernetes.

### Tarea 1. Creacion de un pod con labels y selectors.
Paso 1. Crearemos un yaml con el nombre de pod1.yaml
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: pod1
  labels:
    app: myapp
    env: development
spec:
  containers:
    - name: nginx
      image: nginx
```
![cap9_labels_yaml.png](../images/Capitulo%209/cap9_labels_yaml.png)
Paso 2. Crearemos el pod con el siguiente comando
```bash
kubectl apply -f pod1.yaml
```
![cap9_labels_yaml_create.png](../images/Capitulo%209/cap9_labels_yaml_create.png)

### Tarea 2. Listar los pods con labels y selectors.
Paso 1. Listaremos los pods con el siguiente comando
```bash
kubectl get pods --show-labels
```
![cap9_list_all_labels_pod.png](../images/Capitulo%209/cap9_list_all_labels_pod.png)

Paso 2. Listaremos los pods con el selector app=myapp
```bash
kubectl get pods -l app=myapp
```
![cap9_list_spesifict_label.png](../images/Capitulo%209/cap9_list_spesifict_label.png)

### Tarea 3. Actualizar los labels de un pod.
Paso 3. Actualizaremos los labels del pod1 con el siguiente comando
```bash
kubectl get pods -l app=myapp,env=development --show-labels
```

### Resultado esperado
- El estudiante podra visualizar los labels de los pods
![Screenshot 2025-03-22 at 2.35.13 PM.png](../images/Capitulo%209/Screenshot%202025-03-22%20at%202.35.13%E2%80%AFPM.png)