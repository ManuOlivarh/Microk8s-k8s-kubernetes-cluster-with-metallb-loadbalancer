# Microk8s K8s - Kubernetes bare metal cluster with MetalLB loadbalancer

Esta documentación sirve para configurar un clúster de Kubernetes en Ubuntu 20.04 LTS para un entorno BARE METAL con un balanceador de carga.

## Consideraciones iniciales

A diferencia de otros tipos de instalaciones  microk8s nos provee una vía rapida y sencilla para poder crear un clúster de kubernetes, es tan fácil que se puede instalar con snap.

### Balanceadores de carga
En entornos de nube tradicionales , donde los balanceadores de carga están disponibles bajo demanda, un solo manifiesto de Kubernetes es suficiente para proporcionar un único punto de contacto para el controlador NGINX Ingress para clientes externos e indirectamente, para cualquier aplicación que se ejecute dentro del clúster. Los entornos bare-metal carecen de este producto, lo que requiere una configuración ligeramente diferente para ofrecer el mismo tipo de acceso a los consumidores externos por esta razon en esta guía utilizaremos MetalLB como balanceador de carga externo.


## Que necesitamos para esta implementación?

- Maquinas virtuales


## Primeros pasos

### 1. Instalar Microk8s vía snap

```bash
sudo snap install microk8s --classic
```
### 2. Habilitar addons de Microk8s

```bash
microk8s enable dns dashboard storage
```

### 3. Verificar que servicios y pods esten corriendo

```bash
kubectl get all --all-namespaces
```

### 4. Agregar nodos

```bash
microk8s add-node
```

Al correr el comando aparecera algo como esto:

```bash
From the node you wish to join to this cluster, run the following:
microk8s join 192.168.1.230:25000/92b2db237428470dc4fcfc4ebbd9dc81/2c0cb3284b05

Use the '--worker' flag to join a node as a worker not running the control plane, eg:
microk8s join 192.168.1.230:25000/92b2db237428470dc4fcfc4ebbd9dc81/2c0cb3284b05 --worker

If the node you are adding is not reachable through the default interface you can use one of the following:
microk8s join 192.168.1.230:25000/92b2db237428470dc4fcfc4ebbd9dc81/2c0cb3284b05
microk8s join 10.23.209.1:25000/92b2db237428470dc4fcfc4ebbd9dc81/2c0cb3284b05
microk8s join 172.17.0.1:25000/92b2db237428470dc4fcfc4ebbd9dc81/2c0cb3284b05
```

en nuestro ###nodo worker debemos correr el comando generado "microk8s join" para poder unir el worker al master, cabe destacar que hay añadir la etiqueta "--worker"


```bash
microk8s join 192.168.1.230:25000/92b2db237428470dc4fcfc4ebbd9dc81/2c0cb3284b05 --worker
```


### -Opcional-  Acceder al dashboard
```bash
microk8s dashboard-proxy
```
