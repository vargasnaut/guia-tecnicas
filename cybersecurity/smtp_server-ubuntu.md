Aquí tienes el código completo y corregido, listo para que lo copies y lo pegues en tu archivo `servidor-smtp-propio.md` dentro de la carpeta `01-Linux-Admin`.

```markdown
# 📧 Configuración de Servidor SMTP Propio (Postfix) en Ubuntu
> **Categoría:** Infraestructura de Servidores
> **Servidor:** Postfix (MTA)
> **Entorno:** Ubuntu 22.04 / 24.04

## 🎯 Objetivo
Instalar y configurar un servidor de correo autónomo que permita el envío de emails directamente desde el host local hacia internet, sin depender de proveedores externos como Gmail.

## ⚠️ Prerrequisitos
* Un servidor Ubuntu con acceso root/sudo.
* **Hostname FQDN:** El servidor debe tener un nombre definido (ej: `mail.tudominio.com`).
* **Puertos abiertos:** Asegurar que el puerto `25` (SMTP) no esté bloqueado por el ISP o Firewall.

---

## 📥 1. Instalación de Postfix
Durante la instalación, aparecerá un menú azul. Elige la opción **"Internet Site"**.

```bash
sudo apt update
sudo apt install postfix mailutils -y

```

## ⚙️ 2. Configuración del Hostname y Dominio

Es vital que el servidor se identifique correctamente para evitar ser marcado como SPAM.

**Paso A: Cambiar el nombre del sistema**

```bash
sudo hostnamectl set-hostname mail.tudominio.com

```

**Paso B: Editar el archivo principal de Postfix**
Edita el archivo con `sudo nano /etc/postfix/main.cf` y asegúrate de configurar estas líneas:

```text
myhostname = mail.tudominio.com
mydomain = tudominio.com
myorigin = /etc/mailname
inet_interfaces = all
inet_protocols = ipv4
mydestination = $myhostname, localhost.$mydomain, localhost, $mydomain

```

## 🔐 3. Seguridad Básica (Evitar Open Relay)

Para evitar que atacantes usen tu servidor para enviar SPAM, añade estas restricciones en el mismo archivo `main.cf`:

```text
smtpd_relay_restrictions = permit_mynetworks permit_sasl_authenticated defer_unauth_destination
mynetworks = 127.0.0.0/8 [::ffff:127.0.0.0]/104 [::1]/128

```

Reinicia el servicio para aplicar los cambios:

```bash
sudo systemctl restart postfix

```

## ✅ 4. Verificación y Pruebas

### Prueba de envío desde consola:

```bash
echo "Cuerpo del mensaje: Servidor SMTP Propio funcionando" | mail -s "Prueba SMTP Local" tu-correo@personal.com

```

### Verificación de puertos activos:

```bash
netstat -ltnp | grep 25

```

## 🛠️ Diagnóstico de Errores (Troubleshooting)

Si el correo no llega a su destino, revisa los siguientes puntos:

1. **Logs en tiempo real:** Es la herramienta más importante para saber qué falló.
```bash
sudo tail -f /var/log/mail.log

```


2. **Bloqueo del Puerto 25:** Muchos proveedores de internet bloquean el puerto 25 por defecto para evitar spam.
3. **Falta de registros DNS:** En producción, necesitas configurar registros **MX** y **SPF** en tu dominio para que otros servidores acepten tus correos.

---

*Mantenido por Naut Vargas | Ingeniería de Sistemas UNAC*

```

---

### ¿Qué acabas de documentar?
Acabas de registrar un proceso de **infraestructura pura**. A diferencia de usar Gmail, aquí tú eres el administrador del correo. Esto demuestra que entiendes cómo funciona el protocolo SMTP a bajo nivel.

**¿Te gustaría que ahora preparemos la guía de instalación y configuración de MongoDB para tu carpeta de Bases de Datos?** Es una excelente forma de seguir llenando tu portafolio.

```