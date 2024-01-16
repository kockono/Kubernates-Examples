Problematica como podemos correr 10 o 20 instanceas con docker compose es complicado, las instanceas serían como ganado

## Documentación
```embed
title: "kubectl Cheat Sheet"
image: "https://kubernetes.io/images/kubernetes-horizontal-color.png"
description: "This page contains a list of commonly used kubectl commands and flags. Note: These instructions are for Kubernetes v1.29. To check the version, use the kubectl version command. Kubectl autocomplete BASH source <(kubectl completion bash) # set up autocomplete in bash into the current shell, bash-completion package should be installed first. echo “source <(kubectl completion bash)” >> ~/.bashrc # add autocomplete permanently to your bash shell. You can also use a shorthand alias for kubectl that also works with completion:"
url: "https://kubernetes.io/docs/reference/kubectl/cheatsheet/"
```


### Kubelet
  **Función**: Es un agente que se ejecuta en cada nodo del clúster y se encarga de asegurarse de que los contenedores estén ejecutándose en un pod.
  **Acciones**:
      Recibe las especificaciones del pod a través de la API del servidor Kubernetes.
      Se asegura de que los contenedores estén en ejecución en el nodo.
      Informa sobre el estado del nodo y los contenedores al API Server.
### Control Plane 
  **Función**: Es el componente central que coordina todas las operaciones en el clúster. Está compuesto por varios componentes, incluidos el API Server, el Controlador de Almacenamiento, el Controlador de Nodo y el Administrador de Recursos.
  **Acciones**:
      Toma decisiones globales sobre el clúster (por ejemplo, programación de pods).
      Detecta y responde a eventos del clúster (por ejemplo, iniciar o detener un contenedor).
### Cloud Controller Manager 
  **Función**: Interactúa con la infraestructura de la nube subyacente. Puede ser responsable de integrar características específicas de la nube con Kubernetes.
  **Acciones**:
      Proporciona integración con recursos específicos de la nube (por ejemplo, nodos y volúmenes de almacenamiento).
### Kuroxy 
  **Función**: Mantiene las reglas de red en los nodos. Puede realizar redirección de red para exponer servicios en el clúster.
  **Acciones**:
      Implementa las reglas de red para permitir la comunicación con los pods desde fuera del clúster.
### Scheduler 
  **Función**: Asigna los pods recién creados a nodos en el clúster.
  **Acciones**:
      Considera factores como los recursos del nodo, restricciones de afinidad y anfinidad, y requisitos de hardware y software al programar pods.
### API Server 
  **Función**: Expone la API del clúster Kubernetes. Es la interfaz principal para interactuar con el clúster.
  **Acciones**:
      Valida y configura los datos para la API del clúster.
      Sirve como punto de entrada para las solicitudes de los usuarios y componentes del clúster.
### etcd 
  **Función**: Es una base de datos distribuida y consistente que almacena la configuración del clúster y su estado.
  **Acciones**:
      Almacena la configuración del clúster, como la información del nodo, los límites de recursos y el estado de los pods.

### Pod
Is the basic building block of Kubern­­et­e­s–the smallest and simplest unit in the Kubernetes object model that you create or deploy,is also a group of containers (1 or more).Only containers of same pod can share shared storage.

### Componentes
![[Pasted image 20231220160040.png]]

![[deleted-44122_kubectl.pdf]]

### Comandos Mas Usados
---
```bash
kubectl run name --image name : Crear 1 solo y unico pod
kubectl scale deploy/name   2 : Puede crear multiples pods
kubectl create                : Crea cualquier recurso por Cli o Yaml
kubectl apply                 : Crea/Actualiza cualquier cosa via Yaml
kubectl get pods              : Ver pods
kubectl get all               : Obtener todo lo relacionado a developer
kubectl describe deploy name  : Mejor describción
```

### Pods
```
kubectl run myngx --image nginx
```
Mismo contenedor con mismo Ip, puedes tener varios, solo crea pods no contenedores

### Deployment
```bash
kubectl create deployment name-deploy --image nginx
```
Creación de despliegue

### Scaling ReplicasSets
```bash
kubectl scale deploy/my-apache --replicas 2
```
Deployment -> ReplicaSet(s) -> Pod(s)

### Clean Eliminar 
```bash
kubectl delete pod name-pod
kubectl delete deployment name-deploy
```

### Get Information
```bash
kubectl get pods
kubectl get deploy/pod-name
kubectl get deploy/pod-name -o wide
kubectl describe deploy my-apache   : Best single page information
kubectl get deploy/pod-name -o yaml : All yaml information, api, labels
kubectl get events                  : Ver todos los eventos
```

### Watch In Real Time
```bash
kubectl get pods -w               : Estara escuchando los pods
kubectl get events --watch-only   : Escuchara los pod con mas información
```

### Logs
```bash
kubectl logs pod/pod-name                    : logs del container first only
kubectl logs pod/my-apache -- all containers=true : Ver todos los containers
kubectl logs pod/my-apache-xxx-yyy -c httpd       : Especific container pod
kubectl logs -l app=my-apache                     : Ver multiples logs 
kubectl logs deploy/my-apache --follow --tail 1   : Last entires and firsts
```

## Stern
