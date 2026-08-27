# Wazuh Deployment Guide

Guía práctica para la instalación, configuración y despliegue de **Wazuh**, desde una instalación rápida utilizando el asistente oficial hasta despliegues más avanzados e integraciones orientadas a entornos de Blue Team.

El objetivo de este repositorio es documentar el proceso **paso a paso**, explicando no solamente los comandos utilizados, sino también la función de los principales componentes involucrados en una infraestructura Wazuh.

> **Nota:** Este repositorio tiene fines educativos y de laboratorio. Las configuraciones deberán adaptarse antes de utilizarlas en un entorno de producción.

---

## ¿Qué es Wazuh?

Wazuh es una plataforma de seguridad de código abierto que proporciona capacidades de **XDR (Extended Detection and Response)** y **SIEM (Security Information and Event Management)**.

Permite centralizar y analizar información de seguridad proveniente de servidores, estaciones de trabajo, firewalls, aplicaciones y otros dispositivos.

Entre sus principales capacidades se encuentran:

- Monitoreo de eventos de seguridad.
- Análisis y correlación de logs.
- File Integrity Monitoring (FIM).
- Detección de vulnerabilidades.
- Security Configuration Assessment (SCA).
- Detección de amenazas.
- Monitoreo de endpoints.
- Respuesta activa ante determinados eventos.
- Integración con herramientas y plataformas externas.


## Arquitectura de Wazuh

Una implementación de Wazuh está compuesta principalmente por tres componentes centrales:

### Wazuh Server

Es responsable de analizar la información recibida desde los agentes y otras fuentes de datos.

Aquí se encuentran componentes como el **Wazuh Manager**, encargado del análisis de eventos, aplicación de reglas, decoders y generación de alertas.

### Wazuh Indexer

Es el componente encargado de almacenar e indexar las alertas generadas por Wazuh, permitiendo realizar búsquedas y análisis sobre los datos almacenados.

### Wazuh Dashboard

Proporciona la interfaz web desde la cual se pueden visualizar y analizar alertas, administrar agentes y consultar diferentes módulos de seguridad.

De forma simplificada:

```text
                    ┌─────────────────┐
                    │ Wazuh Dashboard │
                    └────────┬────────┘
                             │
                    ┌────────▼────────┐
                    │  Wazuh Indexer  │
                    └────────▲────────┘
                             │
                    ┌────────┴────────┐
                    │  Wazuh Server   │
                    └────────▲────────┘
                             │
              ┌──────────────┼──────────────┐
              │              │              │
         Linux Agent    Windows Agent    Other Sources
```

Durante esta guía iremos viendo con mayor detalle la función y configuración de cada componente.



# Contenido del repositorio

La documentación se encuentra organizada de forma progresiva.

```text
wazuh-deployment-guide/
│
├── README.md
│
├── docs/
│   ├── 01-quickstart/
│   │   ├── README.md
│   │   ├── requirements.md
│   │   ├── installation.md
│   │   └── troubleshooting.md
│   │
│   ├── 02-all-in-one/
│   │
│   ├── 03-distributed-deployment/
│   │
│   ├── 04-agents/
│   │
│   └── 05-integrations/
│
├── configs/
│
├── scripts/
│
└── images/
```

---
## 01 — Quickstart

Instalación rápida de Wazuh utilizando el **Wazuh Installation Assistant**.

Esta sección está pensada para crear rápidamente un entorno funcional con:

- Wazuh Server
- Wazuh Indexer
- Wazuh Dashboard

Ideal para:

- Laboratorios.
- Homelabs.
- Aprendizaje.
- Pruebas de concepto.

[Ir a Quickstart](docs/01-quickstart/README.md)



## 02 — All-in-One

Instalación y explicación de los componentes principales de Wazuh con mayor detalle.

Se abordarán individualmente:

- Wazuh Indexer.
- Wazuh Server.
- Wazuh Dashboard.
- Certificados.
- Comunicación entre componentes.
- Verificación de servicios.



## 03 — Distributed Deployment

Implementación de una arquitectura distribuida donde los componentes de Wazuh se encuentran separados en diferentes servidores.

Ejemplo:

```text
┌──────────────────┐
│ Wazuh Dashboard  │
│    Server 01     │
└────────┬─────────┘
         │
┌────────▼─────────┐
│  Wazuh Indexer   │
│    Server 02     │
└────────▲─────────┘
         │
┌────────┴─────────┐
│  Wazuh Manager   │
│    Server 03     │
└──────────────────┘
```

Este tipo de arquitectura permite comprender mejor cómo interactúan los diferentes componentes de la plataforma.



## 04 — Agents

Instalación y administración de Wazuh Agent en diferentes sistemas operativos.

Inicialmente se cubrirán:

- Linux.
- Windows.
- Administración y verificación de agentes.


## 05 — Integrations

Esta sección estará dedicada a integrar Wazuh con diferentes tecnologías utilizadas en infraestructura y Blue Team.

Algunas de las integraciones previstas son:

```text
pfSense ────────┐
Suricata ───────┤
Linux ──────────┤
Windows/Sysmon ─┼──► Wazuh ──► Detection & Analysis
Threat Intel ───┤
Other Sources ──┘
```

Entre las futuras integraciones:

- pfSense
- Suricata
- Sysmon
- VirusTotal
- MISP
- AlienVault OTX
- Discord / Slack
- Otras herramientas de seguridad

Cada integración buscará incluir:

1. Arquitectura.
2. Requisitos.
3. Configuración.
4. Archivos utilizados.
5. Generación de eventos de prueba.
6. Verificación de alertas.
7. Troubleshooting.



# Objetivo del proyecto

Este repositorio busca funcionar tanto como **documentación de aprendizaje** como una referencia práctica para construir laboratorios de seguridad utilizando Wazuh.

La documentación continuará creciendo a medida que se implementen nuevas configuraciones, reglas, decoders e integraciones.



## Referencias

La documentación de este repositorio se basa principalmente en la documentación oficial de Wazuh y en pruebas realizadas en entornos de laboratorio.

Para información oficial y actualizada, consulta la documentación de Wazuh.



## Contribuciones

Las sugerencias, correcciones y contribuciones son bienvenidas.

Si encuentras algún error en la documentación o deseas proponer una mejora, puedes abrir un **Issue** o enviar un **Pull Request**.

---

## Licencia

Este proyecto tiene fines educativos. Consulta el archivo `LICENSE` para obtener información sobre los términos de uso.