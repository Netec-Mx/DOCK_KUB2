# Nombre del laboratorio 

## Objetivo de la práctica:
- Comprender y aplicar la creación de Pods en Kubernetes utilizando archivos de configuración YAML.
- Implementar un servicio ClusterIP para exponer un Pod dentro del clúster.

- Verificar el despliegue y la conectividad del servicio mediante comandos de Kubernetes

## Duración aproximada:
- 45 minutos.


## Instrucciones 

### Tarea 1. Crear un Servicio ClusterIP
Paso 1. Primero, crea un Pod que será expuesto por el servicio. Aquí tienes un ejemplo simple  utilizando nginx:

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: nginx-pod
  labels:
    app: nginx
spec:
  containers:
    - name: nginx
      image: nginx
```
Paso 2. Crea el Pod con el siguiente comando:
```bash
kubectl apply -f pod.yaml
```
![Cap_11_create_yaml.png](../images/Capitulo%2011/Cap_11_create_yaml.png)


Paso 3. crea un servicio ClusterIP para exponer el Pod:

```yaml
apiVersion: v1
kind: Service
metadata:
  name: nginx-service
spec:
  type: ClusterIP
  selector:
    app: nginx
  ports:
    - protocol: TCP
      port: 80
      targetPort: 80
```
![Cap11_create_service.png](../images/Capitulo%2011/Cap11_create_service.png)


Paso 4 . Crea el servicio con el siguiente comando:
```bash
kubectl apply -f nginx-service.yaml .
```
![Cap11_service_create.png](../images/Capitulo%2011/Cap11_service_create.png)


Paso 5. Verifica que el servicio se haya creado correctamente:
```bash
kubectl get service nginx-service
```

![Cap11_final.png](../images/Capitulo%2011/Cap11_final.png)

### Resultado esperado

![Cap11_final.png](../images/Capitulo%2011/Cap11_final.png)

