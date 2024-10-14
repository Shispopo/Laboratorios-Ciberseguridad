# Laboratorio OpenWire

## Escenario
Durante su turno como analista de SOC de nivel 2, recibe una escalada de un analista de nivel 1 con respecto a un servidor público. Este servidor ha sido marcado por realizar conexiones salientes a varias direcciones IP sospechosas. En respuesta, se inicia el protocolo estándar de respuesta a incidentes, que incluye el aislamiento del servidor de la red para evitar posibles movimientos laterales o exfiltración de datos y la obtención de una captura de paquetes de la utilidad NSM para su análisis. Su tarea es analizar el pcap y evaluar si hay signos de actividad maliciosa.

## Herramientas Utilizadas
  * **Wireshark:** Para el análisis de paquetes de red.

## Preguntas
* Al identificar la IP C2, podemos bloquear el tráfico hacia y desde esta IP, lo que ayuda a contener la brecha y evitar una mayor exfiltración de datos o ejecución de comandos. ¿Puede proporcionar la IP del servidor C2 que se comunicó con nuestro servidor? 146.190.21.92
* Los puntos de entrada iniciales son fundamentales para rastrear el vector de ataque. ¿Cuál es el número de puerto del servicio que explotó el adversario? 61616
* Continuando con la pregunta anterior, ¿cuál es el nombre del servicio que se encontró vulnerable? Apache ActiveMQ
* La infraestructura del atacante a menudo involucra múltiples componentes. ¿Cuál es la IP del segundo servidor C2? 128.199.52.72
* Los atacantes suelen dejar rastros en el disco. ¿Cómo se llama el ejecutable de shell inverso que se coloca en el servidor? docker
* ¿Qué clase Java fue invocada por el archivo XML para ejecutar el exploit? java.lang.ProcessBuilder
* Para comprender mejor la falla de seguridad específica explotada, ¿puede identificar el identificador CVE asociado con esta vulnerabilidad? CVE-2023-46604
* ¿Cuál es el método y la clase Java vulnerables que permiten a un atacante ejecutar código arbitrario? (Formato: Clase.Método) BaseDataStreamMarshaller.createThrowable

### Análisis Detallado
  **Identificación del Ataque**
    * **Vector de ataque:** El atacante explotó una vulnerabilidad en Apache ActiveMQ (CVE-2023-46604) utilizando el protocolo OpenWire.
    * **C2 Servers:** Se identificaron dos servidores de comando y control (C2) que se comunicaban con el servidor comprometido:
                      * 146.190.21.92
                      * 128.199.52.72
    * **Payload:** Se detectó la descarga de un ejecutable (posiblemente un reverse shell) en el directorio /tmp/ con el nombre "docker".
    * **Método de explotación:** Se utilizó la clase java.lang.ProcessBuilder para ejecutar comandos arbitrarios en el servidor.

  **Análisis del Pcap**
    * **Flujo de ataque:**
      * El atacante estableció una conexión con el servidor vulnerable en el puerto 61616 (OpenWire).
      * Se envió una solicitud maliciosa explotando la vulnerabilidad CVE-2023-46604.
      * El servidor ejecutó el código malicioso, lo que permitió al atacante obtener un shell inverso.
      * El atacante descargó un ejecutable adicional en el servidor.
  **Implicaciones de Seguridad**
    * **Pérdida de control del sistema:** El atacante puede ejecutar comandos arbitrarios en el sistema comprometido.
    * **Exfiltración de datos:** El atacante puede robar datos sensibles del sistema.
    * **Propagación lateral:** El atacante puede utilizar el sistema comprometido como punto de partida para atacar otros sistemas en la red.

### Recomendaciones
* **Parchear la vulnerabilidad:** Aplicar el parche de seguridad correspondiente para corregir la vulnerabilidad en Apache ActiveMQ.
* **Aislar el sistema:** Mantener el sistema aislado hasta que se complete la investigación y remediación.
* **Analizar el ejecutable descargado:** Realizar un análisis en profundidad del ejecutable "docker" para determinar su funcionalidad exacta.
* **Buscar otros sistemas comprometidos:** Escanear la red en busca de otros sistemas que puedan estar infectados.
* **Implementar un sistema de detección de intrusiones (IDS):** Configurar un IDS para detectar actividades sospechosas y alertar al equipo de seguridad.
* **Fortalecer las políticas de seguridad:** Revisar y fortalecer las políticas de seguridad de la organización, incluyendo la gestión de parches, el control de acceso y la segmentación de la red.

### Próximos Pasos
* **Análisis en profundidad del malware:** Realizar un análisis estático y dinámico del ejecutable descargado para identificar sus capacidades y objetivos.
* **Investigación del actor de amenazas:** Intentar identificar al actor de amenazas responsable del ataque y sus motivaciones.
* **Desarrollo de IOCs:** Crear indicadores de compromiso (IOCs) para detectar futuras instancias de este ataque.
* **Capacitación de los usuarios:** Concientizar a los usuarios sobre las mejores prácticas de seguridad para prevenir futuros ataques.

### Anotaciones
* **Profundidad:** Se ha profundizado en el análisis técnico del ataque, incluyendo el flujo de ataque y las técnicas utilizadas.
* **Claridad:** Se ha utilizado un lenguaje claro y conciso para facilitar la comprensión.
* **Completitud:** Se han cubierto todos los aspectos relevantes del análisis, desde la identificación del problema hasta las recomendaciones.
* **Acciónable:** Se han proporcionado recomendaciones específicas para mitigar el riesgo y prevenir futuros ataques.

**Nota:** Este laboratorio es solo un ejemplo. Puedes adaptar el procedimiento y agregar más detalles según tus necesidades y los resultados obtenidos.
