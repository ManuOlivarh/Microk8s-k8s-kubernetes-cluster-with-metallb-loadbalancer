# Microk8s K8s - Kubernetes bare metal cluster with MetalLB loadbalancer

Esta documentación sirve para configurar un clúster de Kubernetes en Ubuntu 20.04 LTS para un entorno BARE METAL con un balanceador de carga.

## Consideraciones iniciales

A diferencia de otros tipos de instalaciones  microk8s nos provee una vía rapida y sencilla para poder crear un clúster de kubernetes, es tan fácil que se puede instalar con snap.

### Balanceadores de carga
En entornos de nube tradicionales , donde los balanceadores de carga están disponibles bajo demanda, un solo manifiesto de Kubernetes es suficiente para proporcionar un único punto de contacto para el controlador NGINX Ingress para clientes externos e indirectamente, para cualquier aplicación que se ejecute dentro del clúster. Los entornos bare-metal carecen de este producto, lo que requiere una configuración ligeramente diferente para ofrecer el mismo tipo de acceso a los consumidores externos por esta razon en esta guía utilizaremos MetalLB como balanceador de carga externo.


## Que necesitamos para esta implementación?

- Maquinas virtuales que nos sirvan como nodos


## Primeros pasos

### Instalar Microk8s vía snap

```bash
sudo snap install microk8s --classic
```
