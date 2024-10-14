# Laboratorio OpenWire

## Escenario
Durante su turno como analista de SOC de nivel 2, recibe una escalada de un analista de nivel 1 con respecto a un servidor público. Este servidor ha sido marcado por realizar conexiones salientes a varias direcciones IP sospechosas. En respuesta, se inicia el protocolo estándar de respuesta a incidentes, que incluye el aislamiento del servidor de la red para evitar posibles movimientos laterales o exfiltración de datos y la obtención de una captura de paquetes de la utilidad NSM para su análisis. Su tarea es analizar el pcap y evaluar si hay signos de actividad maliciosa.

## Herramientas Utilizadas
  * **Wireshark:** Para el análisis de paquetes de red.

## Preguntas y procedimiento
* Al identificar la IP C2, podemos bloquear el tráfico hacia y desde esta IP, lo que ayuda a contener la brecha y evitar una mayor exfiltración de datos o ejecución de comandos. ¿Puede proporcionar la IP del servidor C2 que se comunicó con nuestro servidor?
  * Respuesta: 146.190.21.9
  * Al analizar las estadísticas de conversaciones IPv4, se identificaron tres conexiones con la dirección IP 134.209.197.3, correspondiente a nuestro servidor.
    
    ![]()
    
* Los puntos de entrada iniciales son fundamentales para rastrear el vector de ataque. ¿Cuál es el número de puerto del servicio que explotó el adversario? 61616
  * Respuesta: 61616
  * El análisis del paquete 5 revela que el atacante explotó el servicio en el puerto 61616, lo que sugiere el uso del protocolo OpenWire, comúnmente asociado con Apache ActiveMQ.
    
    ![]()
    
* Continuando con la pregunta anterior, ¿cuál es el nombre del servicio que se encontró vulnerable?
  * Respuesta: Apache ActiveMQ
  * La combinación del puerto 61616 y el análisis del tráfico indica que el servicio vulnerable es Apache ActiveMQ, específicamente el protocolo OpenWire.
    
    ![]()
    
* La infraestructura del atacante a menudo involucra múltiples componentes. ¿Cuál es la IP del segundo servidor C2?
  * Respuesta: 128.199.52.72
  * Al analizar el paquete 34 utilizando la herramienta de análisis de protocolos Wireshark, se identificaron bytes mágicos ELF, característicos de archivos ejecutables. Esto, junto con el hecho de que nuestro servidor estaba solicitando un recurso de esta dirección IP y el tipo de tráfico observado (predominantemente comandos y control), confirma que 128.199.52.72 es un segundo servidor de comando y control (C2) utilizado por el atacante.
    
    ![]()
    
* Los atacantes suelen dejar rastros en el disco. ¿Cómo se llama el ejecutable de shell inverso que se coloca en el servidor?
  * Respuesta: docker
  * El análisis del paquete 11 revela un comando de descarga que incluye la cadena '/tmp/docker', lo que sugiere que el atacante está intentando descargar un shell inverso basado en Docker en el directorio /tmp/ del servidor comprometido. La presencia de comandos típicos de un shell inverso (como 'cd', 'ls', 'whoami') en el tráfico posterior confirma esta hipótesis.
    
    ![]()
    
* ¿Qué clase Java fue invocada por el archivo XML para ejecutar el exploit?
  * Respuesta: java.lang.ProcessBuilder
  * La clase java.lang.ProcessBuilder se utiliza normalmente para crear nuevos procesos y ejecutar comandos externos desde una aplicación Java. En este caso, el atacante ha explotado esta clase para ejecutar el payload malicioso, que probablemente consistía en un comando de shell inverso, con el objetivo de obtener acceso persistente al sistema.
    
    ![]()
    
* Para comprender mejor la falla de seguridad específica explotada, ¿puede identificar el identificador CVE asociado con esta vulnerabilidad?
  * Respuesta: CVE-2023-46604
  * Ingresar a la pagina (https://blog.sonicwall.com/en-us/2023/11/apache-activemq-remote-code-execution-cve_2023_46604/)
  * La vulnerabilidad CVE-2023-46604 en Apache ActiveMQ permite a atacantes remotos ejecutar código arbitrario al manipular tipos de clases serializadas en el protocolo OpenWire.
    
    ![]()
    
* ¿Cuál es el método y la clase Java vulnerables que permiten a un atacante ejecutar código arbitrario? (Formato: Clase.Método)
  * Respuesta: BaseDataStreamMarshaller.createThrowable
  * Ingresar a la pagina (https://blog.sonicwall.com/en-us/2023/11/apache-activemq-remote-code-execution-cve_2023_46604/)
  * El método vulnerable, BaseDataStreamMarshaller.createThrowable, permite a los atacantes inyectar código malicioso en el servidor.

    ![]()

## Recomendaciones
* **Parchear la vulnerabilidad:** Aplicar el parche de seguridad correspondiente para corregir la vulnerabilidad en Apache ActiveMQ.
* **Aislar el sistema:** Mantener el sistema aislado hasta que se complete la investigación y remediación.
* **Analizar el ejecutable descargado:** Realizar un análisis en profundidad del ejecutable "docker" para determinar su funcionalidad exacta.
* **Buscar otros sistemas comprometidos:** Escanear la red en busca de otros sistemas que puedan estar infectados.
* **Implementar un sistema de detección de intrusiones (IDS):** Configurar un IDS para detectar actividades sospechosas y alertar al equipo de seguridad.
* **Fortalecer las políticas de seguridad:** Revisar y fortalecer las políticas de seguridad de la organización, incluyendo la gestión de parches, el control de acceso y la segmentación de la red.

## Próximos Pasos
* **Análisis en profundidad del malware:** Realizar un análisis estático y dinámico del ejecutable descargado para identificar sus capacidades y objetivos.
* **Investigación del actor de amenazas:** Intentar identificar al actor de amenazas responsable del ataque y sus motivaciones.
* **Desarrollo de IOCs:** Crear indicadores de compromiso (IOCs) para detectar futuras instancias de este ataque.
* **Capacitación de los usuarios:** Concientizar a los usuarios sobre las mejores prácticas de seguridad para prevenir futuros ataques.

**Nota:** Este laboratorio es solo un ejemplo. Puedes adaptar el procedimiento y agregar más detalles según tus necesidades y los resultados obtenidos.
