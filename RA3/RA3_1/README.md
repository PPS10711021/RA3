Server Hardening - Apache Security Practices

1. Introducción

1.1. Server Hardening

El hardening de servidores web es el proceso de mejorar la seguridad de un servidor web mediante la reducción de vulnerabilidades y la eliminación de posibles puntos de entrada que los atacantes pueden explotar. Este enfoque se basa en asegurar tanto el sistema operativo como las aplicaciones web que se ejecutan en el servidor, con el objetivo de protegerlo contra una amplia variedad de amenazas, como:

Ataques de denegación de servicio (DDoS)

Inyecciones de código

Explotación de vulnerabilidades conocidas

Acceso no autorizado

1.2. Apache Hardening

El hardening de Apache se refiere al proceso de reforzar la seguridad del servidor web Apache para reducir la superficie de ataque y protegerlo de posibles vulnerabilidades. Apache es uno de los servidores web más populares y, debido a su amplia adopción, puede ser un objetivo frecuente de ataques.

Buenas prácticas para mejorar la seguridad en Apache:

Mantener Apache actualizado

Desactivar módulos innecesarios

Deshabilitar la visualización de información del servidor

Configurar permisos estrictos

Usar HTTPS (SSL/TLS)

Limitar los métodos HTTP permitidos

Proteger contra ataques de inyección

Implementar autenticación básica

Habilitar y configurar correctamente los registros

Usar un firewall

Configurar Timeout y KeepAlive

Implementar límites de acceso por IP

2. Objetivos

Esta unidad didáctica contribuye a trabajar los siguientes criterios de evaluación:

RA4: Detecta y corrige vulnerabilidades de aplicaciones web analizando su código fuente y configurando servidores web.

CA.A: Se han validado las entradas de los usuarios.

CA.B: Se han detectado riesgos de inyección tanto en el servidor como en el cliente.

CA.E: Se ha gestionado correctamente la sesión del usuario durante el uso de la aplicación.

3. Actividades

3.1. Requisitos

Crear una cuenta de GitHub para las entregas utilizando el correo oficial @alu.edu.gva.es con el usuario PPS+NIA (sin incluir +).

Crear una cuenta en Docker HUB para subir las imágenes de los contenedores con el mismo usuario PPS+NIA.

Utilizar GIT + template para la entrega: Template en GitHub.

3.2. Apache Hardening

Referencia: Hardening Servidor

Prácticas:

Content Security Policy (CSP)

Web Application Firewall

OWASP

Evitar ataques DDoS

EXTRA: Implementación con Nginx

Las imágenes Docker tendrán que estar subidas al Docker HUB utilizando la nomenclatura pps/prX (sustituyendo X por el número de la práctica).

Se debe utilizar la mejor estrategia de capas en la creación de los contenedores, asegurando que los contenedores tengan información en cascada. Ejemplo:

El contenedor 3.1.3 contendrá la información de los contenedores 3.1.2 y 3.1.1.

Cada práctica debe incluir un README con:

Explicación detallada

Validación

Capturas de pantalla

URL para realizar docker pull de la imagen correspondiente.

3.3. Certificados SSL

Referencia: Instalación de Certificados SSL

Tarea:

Instalar un certificado digital en el servidor Apache y generar la imagen Docker correspondiente.

3.4. Apache Hardening Best Practices

Referencia: Apache Web Server Hardening

Tarea:

Implementar las mejores prácticas de securización del servidor Apache y generar la imagen Docker correspondiente.

