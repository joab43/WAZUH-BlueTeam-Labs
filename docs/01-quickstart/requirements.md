# Requisitos para Wazuh Quickstart

Antes de realizar la instalación debemos verificar que el servidor cumpla con los requisitos necesarios para ejecutar los componentes de Wazuh.

En una instalación Quickstart los principales componentes se ejecutarán sobre el **mismo servidor**:

```text
Server
├── Wazuh Manager
├── Wazuh Indexer
└── Wazuh Dashboard
```

Por esta razón, los recursos necesarios dependerán principalmente de la cantidad de endpoints que serán monitoreados y de la cantidad de eventos generados.

---

## Sistema operativo

Se recomienda utilizar una distribución Linux compatible con la versión de Wazuh que se desea instalar.

Algunos sistemas utilizados habitualmente incluyen:

- Ubuntu
- Debian
- Red Hat Enterprise Linux
- Rocky Linux
- AlmaLinux
- Amazon Linux

> **Importante:** Los sistemas operativos y versiones soportadas pueden cambiar entre versiones de Wazuh. Antes de realizar una instalación en producción se recomienda verificar la documentación oficial correspondiente a la versión utilizada.

---

## Hardware

Para un laboratorio pequeño se recomienda disponer como mínimo de recursos suficientes para ejecutar simultáneamente el Manager, Indexer y Dashboard.

Como referencia para un entorno de laboratorio:

```text
CPU:        4 vCPU
RAM:        8 GB
Storage:    50 GB+
```

El almacenamiento necesario puede aumentar considerablemente dependiendo de:

- Número de agentes.
- Cantidad de eventos recibidos.
- Periodo de retención.
- Integraciones configuradas.
- Logs provenientes de dispositivos externos.

Para entornos de producción se debe realizar un dimensionamiento acorde a la infraestructura que será monitoreada.

---

## Conectividad

El servidor debe contar con:

- Conectividad de red.
- Resolución DNS funcional.
- Acceso a Internet para descargar los paquetes necesarios.
- Comunicación con los endpoints que utilizarán Wazuh Agent.

Podemos comprobar la conectividad utilizando:

```bash
ping -c 4 google.com
```

También podemos verificar resolución DNS:

```bash
getent hosts packages.wazuh.com
```

---

## Privilegios

La instalación requiere privilegios administrativos.

Podemos ejecutar los comandos utilizando:

```bash
sudo <command>
```

o acceder temporalmente como `root`:

```bash
sudo -i
```

---

## Actualizar el sistema

Antes de comenzar es recomendable actualizar los paquetes disponibles.

En sistemas basados en Debian/Ubuntu:

```bash
sudo apt update
sudo apt upgrade -y
```

En sistemas basados en RHEL:

```bash
sudo dnf update -y
```

Una vez comprobados los requisitos podemos continuar con la instalación.

➡️ [Continuar con la instalación](installation.md)