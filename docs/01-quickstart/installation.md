# Instalación Quickstart de Wazuh

En esta sección realizaremos una instalación All-in-One utilizando el **Wazuh Installation Assistant**.

Este método automatiza gran parte del proceso de instalación y configuración de los componentes principales de Wazuh.

---

# 1. Preparar el servidor

Primero verificamos que nuestro servidor tenga conectividad.

```bash
ping -c 4 google.com
```

Comprobamos también que podemos resolver el dominio de los paquetes de Wazuh:

```bash
getent hosts packages.wazuh.com
```

Si ambas pruebas funcionan correctamente podemos continuar.

---

# 2. Descargar Wazuh Installation Assistant

Wazuh proporciona un script denominado:

```text
wazuh-install.sh
```

Este script automatiza el despliegue y configuración de los principales componentes.

La estructura general del comando de descarga es:

```bash
curl -sO https://packages.wazuh.com/<VERSION>/wazuh-install.sh
```

Donde `<VERSION>` debe reemplazarse por la rama correspondiente a la versión de Wazuh que se desea instalar.

Por ejemplo:

```bash
curl -sO https://packages.wazuh.com/4.x/wazuh-install.sh
```

> Antes de ejecutar este comando verifica en la documentación oficial de Wazuh cuál es la versión actual del asistente de instalación.

Podemos comprobar que el archivo fue descargado:

```bash
ls -lh wazuh-install.sh
```

---

# 3. Ejecutar el asistente

Ejecutamos:

```bash
sudo bash wazuh-install.sh -a
```

La opción:

```text
-a
```

corresponde al despliegue **All-in-One**.

El asistente se encargará de instalar y configurar automáticamente los componentes necesarios.

El proceso puede tardar varios minutos dependiendo de los recursos del servidor y de la conexión a Internet.

---

# 4. ¿Qué está instalando el script?

Durante el proceso se desplegarán los principales componentes:

```text
wazuh-install.sh
       │
       ├── Wazuh Indexer
       │
       ├── Wazuh Server
       │
       └── Wazuh Dashboard
```

Una vez finalizado el proceso tendremos una instancia funcional de Wazuh ejecutándose sobre el servidor.

---

# 5. Guardar las credenciales

Al finalizar, el asistente mostrará información para acceder al Wazuh Dashboard.

Guarda estas credenciales en un lugar seguro.

> No almacenes contraseñas reales, API keys, certificados privados ni otras credenciales dentro de este repositorio.

---

# 6. Verificar los servicios

Podemos comprobar el estado del Wazuh Manager:

```bash
sudo systemctl status wazuh-manager
```

Wazuh Indexer:

```bash
sudo systemctl status wazuh-indexer
```

Wazuh Dashboard:

```bash
sudo systemctl status wazuh-dashboard
```

Los servicios deberían aparecer como:

```text
active (running)
```

También podemos realizar una comprobación rápida:

```bash
sudo systemctl is-active wazuh-manager
sudo systemctl is-active wazuh-indexer
sudo systemctl is-active wazuh-dashboard
```

Si todo funciona correctamente deberíamos obtener:

```text
active
active
active
```

---

# 7. Obtener la dirección IP

Podemos consultar las interfaces y direcciones IP del servidor utilizando:

```bash
ip addr
```

O de forma resumida:

```bash
hostname -I
```

Por ejemplo:

```text
192.168.1.50
```

---

# 8. Acceder al Dashboard

Desde un navegador ingresamos:

```text
https://IP_DEL_SERVIDOR
```

Ejemplo:

```text
https://192.168.1.50
```

Utilizamos las credenciales generadas durante la instalación.

---

## Certificado HTTPS

Durante el primer acceso es posible que el navegador muestre una advertencia relacionada con el certificado HTTPS.

En un entorno de laboratorio esto puede ocurrir debido al certificado utilizado por el despliegue.

Para una implementación expuesta o utilizada en producción se recomienda configurar correctamente certificados y controles de acceso adecuados.

---

# 9. Verificación final

Una vez dentro del Dashboard debemos comprobar que la plataforma carga correctamente.

Nuestra arquitectura en este punto será:

```text
                 Browser
                    │
                  HTTPS
                    │
                    ▼
          ┌───────────────────┐
          │  Wazuh Dashboard  │
          └─────────┬─────────┘
                    │
          ┌─────────▼─────────┐
          │   Wazuh Indexer   │
          └─────────▲─────────┘
                    │
          ┌─────────┴─────────┐
          │   Wazuh Server    │
          └───────────────────┘
```

Con esto hemos completado nuestro primer despliegue de Wazuh.

---

# Siguiente paso

Una vez instalado Wazuh podemos comenzar a agregar endpoints utilizando **Wazuh Agent**.

Más adelante también veremos cómo recibir información proveniente de otras fuentes como firewalls, IDS y plataformas de Threat Intelligence.

Si tu instalación presentó algún problema:

➡️ [Consultar Troubleshooting](troubleshooting.md)