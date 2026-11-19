Servicios de Red para el Despliegue Web: DNS y LDAP
Proyecto de configuración de servicios de red esenciales para el despliegue de aplicaciones web. Incluye la configuración de un servidor DNS (Bind9) y un servidor de directorio (OpenLDAP), ambos desplegados sobre contenedores Docker.

Tecnologías y Herramientas
Contenedores: Docker
Servidor DNS: Bind9 (ubuntu/bind9)
Servidor de Directorio: OpenLDAP (slapd), LDAP utilities
Entorno: Ubuntu (WSL)

🎯 Funcionalidades y Conceptos Aplicados
1. Servidor DNS con Bind9
Configuración de red: Modificación del archivo /etc/resolv.conf dentro del contenedor para que resuelva a sí mismo (127.0.0.1).
Zonas DNS: Creación de una zona directa (fpv.db) y una zona inversa (fpv.rev) para el dominio fpv.com.
Registros DNS: Configuración de registros de tipo A (para www, ftp, mail), CNAME (alias alumno -> www), MX (servidor de correo) y NS (servidor de nombres).
Verificación: Uso de herramientas como nslookup, host y dig para comprobar la resolución directa e inversa.

2. Servidor LDAP (OpenLDAP)
Despliegue: Creación de un contenedor Docker con la imagen oficial de OpenLDAP, configurando el dominio base (dc=distancia26,dc=com) y la contraseña de administrador.
Estructura del directorio: Creación de ficheros .ldif para añadir una unidad organizativa (ou=despliegue), un grupo y un usuario.
Modificación y consulta: Uso de comandos como ldapadd (para añadir entradas), ldapmodify (para modificar grupos) y ldapsearch (para consultar la información).

Cómo ejecutar el proyecto
1.DNS:
Arranca el contenedor: docker run -d --name dns-server -p 53:53/udp ubuntu/bind9
Accede a él: docker exec -it dns-server /bin/bash
Instala utilidades: apt update && apt install nano dnsutils -y
Aplica las configuraciones en /etc/bind/ y reinicia el servicio.

2.LDAP:
Arranca el servidor (ejemplo con docker-compose o docker run).
Usa los archivos .ldif del repositorio para añadir datos con ldapadd y consultar con ldapsearch.
