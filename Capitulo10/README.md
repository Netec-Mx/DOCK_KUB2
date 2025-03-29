# Trabajo con Volumes (emptyDir)

## Objetivo de la práctica:
- Comprender el funcionamiento de los volúmenes emptyDir en Kubernetes, que son útiles para
  compartir datos entre contenedores en el mismo Pod.


## Duración aproximada:
- 20 minutos.

## Instrucciones 

### Tarea 1. Creacion pod con volumen emptyDir

Paso 1. crear el emptydir-pod.yaml con la siguiente informacion

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: mypod
spec:
  containers:
    - name: mycontainer1
      image: nginx
      volumeMounts:
        - name: cache-volume
          mountPath: /cache
    - name: mycontainer2
      image: alien777/mi-aplicacion-node:v1
      volumeMounts:
        - name: cache-volume
          mountPath: /cache
  volumes:
    - name: cache-volume
      emptyDir: {}
```
![emptydir-pod-file.png](../images/Capitulo%2010/emptydir-pod-file.png)

Paso 2. Crear el pod con el siguiente comando

```bash
kubectl apply -f emptydir-pod.yaml
```
![cap10_file_at_k8s.png](../images/Capitulo%2010/cap10_file_at_k8s.png)

Paso 3. Acceder al contenedor para poder interactuar con el volumen

```bash
kubectl exec -it mypod -c mycontainer1 -- /bin/sh
```
![cap10_exec_entry_info.png](../images/Capitulo%2010/cap10_exec_entry_info.png)


Paso 4. Una vez dentro del contenedor, crea un archivo en el directorio /cache . Por ejemplo:

```bash
echo "Hola Kubernetes" > /cache/saludo.txt
exit
```

Paso 5. Acceder al Segundo Contenedor y ver el archivo que se guardo en el primer pod

```bash
kubectl exec -it mypod -c mycontainer2 -- /bin/sh
cat /cache/saludo.txt
```

![cap10_archive_tex.png](../images/Capitulo%2010/cap10_archive_tex.png)


Paso 6. Eliminar el pod

```bash
kubectl delete pod mypod
```
![cap10_final_delete.png](../images/Capitulo%2010/cap10_final_delete.png)

### Resultado esperado


![cap10_archive_tex.png](../images/Capitulo%2010/cap10_archive_tex.png)
