# Wazuh Quickstart

Esta sección explica cómo realizar una instalación rápida de Wazuh utilizando el **Wazuh Installation Assistant**.

El método Quickstart permite desplegar los componentes centrales de Wazuh en un único servidor utilizando el asistente proporcionado oficialmente por Wazuh.

Al finalizar tendremos:

```text
                WAZUH SERVER
┌───────────────────────────────────────┐
│                                       │
│          Wazuh Dashboard              │
│                 │                     │
│          Wazuh Indexer                │
│                 │                     │
│          Wazuh Manager                │
│                                       │
└───────────────────────────────────────┘
                    ▲
                    │
              Wazuh Agents
```

Este tipo de instalación es especialmente útil para:

- Laboratorios.
- Homelabs.
- Entornos educativos.
- Pruebas de concepto.
- Aprender el funcionamiento básico de Wazuh.



## Contenido

La guía está dividida en las siguientes secciones:

### 1. Requisitos

Antes de comenzar comprobaremos que nuestro servidor dispone de los recursos y sistema operativo necesarios.

→ [Ver requisitos](requirements.md)

### 2. Instalación

Descargaremos y ejecutaremos el asistente de instalación de Wazuh y verificaremos los componentes desplegados.

→ [Comenzar instalación](installation.md)

### 3. Troubleshooting

Problemas comunes encontrados durante la instalación y posibles soluciones.

→ [Troubleshooting](troubleshooting.md)

---

## Componentes instalados

El método Quickstart instala automáticamente los principales componentes de Wazuh:

**Wazuh Server**

Recibe y analiza los eventos provenientes de los agentes y otras fuentes de información.

**Wazuh Indexer**

Almacena e indexa las alertas generadas.

**Wazuh Dashboard**

Proporciona la interfaz web utilizada para visualizar alertas y administrar la plataforma.

---

## ¿Qué aprenderemos?

Al finalizar esta sección deberías ser capaz de:

- Preparar un servidor para Wazuh.
- Utilizar el Wazuh Installation Assistant.
- Identificar los componentes instalados.
- Verificar el estado de los servicios.
- Acceder al Wazuh Dashboard.
- Identificar problemas básicos durante la instalación.

Una vez comprendido este proceso podremos avanzar hacia instalaciones más detalladas y arquitecturas distribuidas.