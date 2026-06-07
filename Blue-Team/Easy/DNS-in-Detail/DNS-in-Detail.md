# TryHackMe: DNS in Detail

## Descripción del Laboratorio
Este laboratorio práctico aborda en profundidad el funcionamiento del Sistema de Nombres de Dominio (DNS), su estructura jerárquica, los tipos de registros fundamentales utilizados en la infraestructura de red y el flujo secuencial de una solicitud de resolución de nombres. Adicionalmente, se incluye una sección práctica de auditoría mediante simulación de consultas de comandos.

---

## Tarea 1: Introducción a DNS
El Sistema de Nombres de Dominio (DNS) es el encargado de traducir nombres de dominio legibles para seres humanos (por ejemplo, `tryhackme.com`) en direcciones IP numéricas (por ejemplo, `104.26.10.229`) para permitir la comunicación entre dispositivos en la red.

*   **Estructura de IP analizada:** Direcciones IPv4 compuestas por 4 octetos (valores numéricos que oscilan entre 0 y 255) separados por puntos.
*   **Significado de las siglas:** Domain Name System.

---

## Tarea 2: Jerarquía de Dominios
La resolución y lectura de un nombre de dominio calificado (FQDN) se procesa de derecha a izquierda siguiendo una estructura jerárquica estricta:

| Capa Jerárquica | Nombre Técnico | Descripción y Reglas de Ingeniería |
| :--- | :--- | :--- |
| **Derecha (Final)** | TLD (Top-Level Domain) | Extensión final del dominio. Se divide en **gTLD** (genéricos por propósito, ej: `.com`, `.org`) y **ccTLD** (códigos geográficos por país, ej: `.co.uk`, `.ar`). |
| **Centro** | SLD (Second-Level Domain) | El nombre principal o de la organización (ej: `tryhackme`). Limitado a un máximo de 63 caracteres. Solo permite caracteres `a-z`, `0-9` y guiones medios (no consecutivos, ni al inicio o final). |
| **Izquierda (Inicio)** | Subdominio | Prefijo utilizado para segmentar servicios o servidores específicos (ej: `admin`). Posee las mismas restricciones de caracteres que el SLD. |

*   **Límite total de longitud:** El nombre de dominio completo no puede superar los 253 caracteres.

---

## Tarea 3: Tipos de Registros DNS (DNS Record Types)
Los servidores DNS utilizan diferentes tipos de registros para almacenar información específica de un dominio. Los más comunes son:

*   **A (Address):** Mapea un nombre de dominio directamente a una dirección IPv4.
*   **AAAA (Quad-A):** Mapea un nombre de dominio a una dirección IPv6 (128 bits).
*   **CNAME (Canonical Name):** Funciona como un alias. Apunta un subdominio hacia otro nombre de dominio en lugar de a una dirección IP directa.
*   **MX (Mail Exchange):** Especifica los servidores encargados de gestionar el correo electrónico del dominio. Incluye un valor numérico de prioridad (a menor número, mayor prioridad de entrega).
*   **TXT (Text):** Campo de texto libre. Utilizado en ciberseguridad para validación de propiedad de dominios y para implementar políticas de seguridad frente a suplantación de identidad (reglas anti-phishing como SPF, DKIM y DMARC).

---

## Tarea 4: Flujo de una Solicitud DNS (Making a Request)
Cuando un cliente realiza una petición de conexión, el proceso de resolución sigue un orden jerárquico y secuencial de consultas:

```text
[Cliente] ──> 1. Caché Local ──> 2. Servidor Recursivo (ISP) ──> 3. Servidor Raíz (Root) ──> 4. Servidor TLD ──> 5. Servidor Autoritativo
