# 🛡️ Análisis Forense de Memoria RAM (DFIR-01)

Este proyecto documenta el proceso y los resultados del análisis forense de una imagen de memoria RAM capturada de un servidor con comportamiento anómalo. El objetivo principal fue identificar la actividad maliciosa, los comandos ejecutados por el atacante y los indicios de persistencia y acceso remoto.

## ⚙️ Caso Práctico y Metodología

El análisis se centra en la evidencia volátil de un servidor comprometido. Un compañero capturó la memoria RAM (`memdump.mem`) justo antes de que se apagara la máquina, lo cual fue clave, ya que si se hubiera apagado, la información volátil se habría perdido en gran parte.

| Contexto | Detalle |
| :--- | :--- |
| **Evidencia** | Imagen de memoria RAM (`memdump.mem`) de un servidor con Windows Vista SP1 x86. |
| **Herramienta principal** | Volatility Foundation Framework 2.6.1. |
| **Plataforma de Ejecución** | Windows CMD con Python 2.7.18. |
| **Fecha de la Imagen** | 2015-09-03 10:04:05 UTC+0000. |

## 🔑 Conclusiones Clave del Análisis

El análisis de la consola y los procesos reveló un ataque persistente y dirigido con una clara intención de establecer acceso remoto permanente:

* **Persistencia y Elevación de Privilegios:** El cibercriminal creó el usuario sospechoso `user1` y lo añadió al grupo "Remote Desktop Users".
* **Preparación de la Red:** Se modificó la configuración del Firewall de Windows (mediante `netsh firewall`) para habilitar y permitir conexiones entrantes de Escritorio Remoto (RDP).
* **Ejecución de Código Malicioso:** Se identificó la ejecución de archivos sospechosos como **`et.exe`** y **`httpd.exe`**.
* **Identificación del Malware:** El archivo `httpd.exe` está vinculado al entorno **XAMPP** (Apache HTTP Server). Se considera un archivo potencialmente malicioso (un posible *backdoor* o *webshell*) que buscaba explotar puertos abiertos (80, 443, 3306) para el control y la transferencia de datos.
* **IP Sospechosa:** Se identificó la IP **`192.168.56.1`** con una conexión activa a `svchost.exe`, que se considera la fuente del ataque.

## 📚 Estructura del Repositorio

* **`Moreno_Aranda_Jose_Antonio_AFI01_Tarea.pdf`**: Documento completo con el análisis y las respuestas a todas las preguntas del coordinador.
* **`README.md`**: Resumen del proyecto, herramientas y conclusiones (este archivo).
* **`Comandos.txt`**: Listado de todos los comandos de Volatility ejecutados durante el análisis para obtener la evidencia.
