#  TryHackMe: Junior Security Analyst Intro

##  Descripción del Laboratorio
Este laboratorio práctico simula el día a día de un **Analista de Seguridad de Nivel 1 (L1)** dentro de un **SOC (Security Operations Center)**. El objetivo principal fue interactuar con las herramientas centrales de monitoreo y defensa perimetral para identificar, validar, escalar y mitigar un intento de explotación real en los servidores de la organización.

---

##  Estructura y Roles de un SOC
Durante la sesión se analizaron las interacciones y jerarquías clave dentro del equipo defensivo:

*   **Junior Security Analyst (L1):** Primera línea de defensa encargada del monitoreo constante de alertas las 24 horas, los 7 días de la semana (**24/7 team**).
*   **Senior Analyst (L2/L3 - Will Griffin):** Encargado de manejar alertas complejas y recibir los escalados de incidentes validados por el nivel 1.
*   **SOC Engineer (Corey Stevens):** Responsable del mantenimiento de la infraestructura, optimización del SIEM y creación de reglas de detección.
*   **SOC Manager (Emily Conway):** Gestión general del área y reportes ejecutivos a la alta dirección.
*   **Incident Responder (Daniel Herrera):** Especialista activado bajo demanda únicamente ante incidentes críticos o de gran escala.

---

##  Resolución del Incidente: Paso a Paso

El ejercicio práctico presentó un escenario de ataque activo que requería seguir el flujo metodológico de un analista defensivo:

### 1. Detección en el SIEM
Al monitorear el **SIEM Dashboard**, se detectó un volumen inusual y crítico de eventos que alertaban sobre un intento de explotación del fallo **Log4j** dirigido contra la infraestructura de nuestros servidores web corporativos.

### 2. Identificación de los Vectores
Se procedió a aislar los registros de auditoría de la alerta, logrando extraer la dirección de origen del tráfico hostil:
*   **IP del Atacante (Simulada):** `268.23.235.1`

### 3. Ciberinteligencia y Validación (Threat Intel)
Para descartar un posible falso positivo, se ingresó la dirección identificada en la herramienta **IP Hunter**. La plataforma de inteligencia de amenazas confirmó que la IP poseía un score de reputación malicioso extremadamente alto debido a reportes previos de actividad maliciosa.

### 4. Escalado de la Alerta
Con la certeza de estar ante un incidente verídico, se utilizó el módulo de **Escalation** para formalizar el ticket de seguridad. Siguiendo los protocolos de la cadena de mando establecidos, el caso fue derivado al analista Senior (*Will Griffin*) para su respectiva aprobación técnica.

### 5. Mitigación en Cortafuegos
Tras recibir la autorización del escalado, se tomó control del **Firewall** perimetral de la empresa. Se introdujo una regla restrictiva de bloqueo directo (**Block**) para la IP hostil, interrumpiendo inmediatamente su comunicación con la red interna.

### 6. Cierre y Flag de Éxito
Una vez que el perímetro fue securizado y el ataque neutralizado, el sistema validó el procedimiento arrojando la confirmación del éxito:

>  **Flag Obtenida:** `THM{SOC_AGENT_ACTIVATED}`

---

##  Conceptos Clave Aprendidos

1.  **Centralización de Logs:** El **SIEM** es indispensable en el SOC, ya que sin un panel centralizado sería imposible correlacionar alertas provenientes de distintas fuentes en tiempo real.
2.  **Importancia del Triage:** Jamás se deben tomar medidas drásticas de bloqueo perimetral basándose únicamente en la primera alerta del sistema. El uso de herramientas de reputación (**Threat Intelligence**) es mandatorio para proteger la disponibilidad del negocio y evitar bloquear tráfico legítimo (falsos positivos).
3.  **Seguimiento de Protocolos:** El analista L1 tiene roles estrictos de investigación, clasificación y contención inicial. Las modificaciones en las políticas de seguridad perimetral críticas (como el Firewall) deben seguir una estructura formal de escalado técnico.
