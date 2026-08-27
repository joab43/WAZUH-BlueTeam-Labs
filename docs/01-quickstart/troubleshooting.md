# Troubleshooting — Wazuh Quickstart

Esta sección recopila algunos problemas que pueden aparecer durante la instalación o utilización inicial de Wazuh.

Antes de realizar cambios en la configuración, es recomendable identificar primero cuál de los componentes presenta el problema.

---

# Verificar servicios

Comenzamos verificando los tres servicios principales.

### Wazuh Manager

```bash
sudo systemctl status wazuh-manager
```

### Wazuh Indexer

```bash
sudo systemctl status wazuh-indexer
```

### Wazuh Dashboard

```bash
sudo systemctl status wazuh-dashboard
```

También podemos comprobarlos rápidamente:

```bash
sudo systemctl is-active wazuh-manager
sudo systemctl is-active wazuh-indexer
sudo systemctl is-active wazuh-dashboard
```

---

# Consultar logs con journalctl

Cuando un servicio no inicia correctamente podemos consultar sus registros.

Por ejemplo:

```bash
sudo journalctl -u wazuh-manager
```

Para mostrar los eventos más recientes:

```bash
sudo journalctl -u wazuh-manager -n 50
```

Para seguir los logs en tiempo real:

```bash
sudo journalctl -u wazuh-manager -f
```

El mismo procedimiento puede utilizarse con otros servicios:

```bash
sudo journalctl -u wazuh-indexer -n 50
```

```bash
sudo journalctl -u wazuh-dashboard -n 50
```

---

# No puedo acceder al Dashboard

Primero verifica que el servicio se encuentre funcionando:

```bash
sudo systemctl status wazuh-dashboard
```

Después verifica los puertos abiertos en el servidor:

```bash
sudo ss -tulpn
```

También puedes filtrar específicamente conexiones HTTPS:

```bash
sudo ss -tulpn | grep :443
```

Comprueba además:

- Dirección IP correcta.
- Firewall del servidor.
- Firewall de la red.
- Reglas de seguridad del proveedor cloud, si aplica.
- Conectividad entre tu equipo y el servidor.

---

# Comprobar conectividad

Desde otro equipo podemos comprobar si el servidor responde:

```bash
ping IP_DEL_SERVIDOR
```

Ejemplo:

```bash
ping 192.168.1.50
```

También podemos probar HTTPS:

```bash
curl -k https://IP_DEL_SERVIDOR
```

La opción `-k` permite realizar la prueba ignorando temporalmente errores de validación del certificado.

> Utiliza `-k` únicamente para pruebas controladas. No es una solución para problemas de certificados.

---

# Problemas de DNS durante la instalación

Comprueba primero la resolución:

```bash
getent hosts packages.wazuh.com
```

También puedes utilizar:

```bash
ping -c 4 packages.wazuh.com
```

Si una dirección IP funciona pero los dominios no pueden resolverse, probablemente existe un problema relacionado con DNS.

Revisa la configuración DNS del servidor antes de volver a ejecutar la instalación.

---

# Problemas de recursos

Wazuh Indexer puede consumir una cantidad considerable de memoria.

Podemos comprobar los recursos disponibles con:

```bash
free -h
```

CPU y procesos:

```bash
top
```

Espacio disponible:

```bash
df -h
```

Si el servidor tiene pocos recursos, alguno de los componentes puede presentar problemas al iniciar o funcionar de forma inestable.

---

# Reiniciar servicios

Después de realizar un cambio podemos reiniciar individualmente el componente afectado.

Manager:

```bash
sudo systemctl restart wazuh-manager
```

Indexer:

```bash
sudo systemctl restart wazuh-indexer
```

Dashboard:

```bash
sudo systemctl restart wazuh-dashboard
```

Después comprobamos nuevamente:

```bash
sudo systemctl status <servicio>
```

---

# Revisar logs del Wazuh Manager

Uno de los archivos más importantes para diagnosticar problemas del Manager es:

```text
/var/ossec/logs/ossec.log
```

Podemos visualizar los últimos eventos con:

```bash
sudo tail -n 50 /var/ossec/logs/ossec.log
```

O seguirlos en tiempo real:

```bash
sudo tail -f /var/ossec/logs/ossec.log
```

Este archivo será especialmente importante más adelante cuando trabajemos con:

- Agentes.
- Decoders.
- Reglas.
- Syslog.
- Integraciones.
- Active Response.

---

# Información útil al reportar un problema

Si necesitas investigar o reportar un error, intenta recopilar:

```text
Versión de Wazuh:
Sistema operativo:
Versión del sistema operativo:
CPU:
RAM:
Almacenamiento:
Componente afectado:
Estado del servicio:
Mensaje de error:
Logs relevantes:
```

También puede ser útil obtener:

```bash
uname -a
```

```bash
cat /etc/os-release
```

```bash
free -h
```

```bash
df -h
```

---

## Volver

⬅️ [Volver a Quickstart](README.md)