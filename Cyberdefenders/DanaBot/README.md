# DanaBot - Análisis de Tráfico de Red con Wireshark

**Escenario:**

Se ha detectado una intrusión en la red de la empresa. El objetivo de este laboratorio es analizar un archivo PCAP capturado durante el incidente para identificar el malware utilizado, el método de ataque y los datos exfiltrados.

**Objetivos del Laboratorio:**

* Identificar el malware DanaBot en el tráfico de red.
* Analizar el comportamiento del malware.
* Determinar los datos exfiltrados.
* Comprender las técnicas utilizadas por el atacante.

**Herramienta:**
* **Wireshark:** Analizador de protocolos de red.
* **VirusTotal:** Plataforma de análisis de archivos maliciosos.

**Preguntas y prodecimiento:**
   * **Pregunta 1:** ¿Cuál es el nombre del archivo inicial malicioso?
     * Buscar paquetes relacionados con descargas y analizar el nombre del archivo.
     * **Respuesta:** allegato_708.js
       ![Pregunta1](https://github.com/Shispopo/Laboratorios-Ciberseguridad/blob/main/Cyberdefenders/DanaBot/Imagenes/1.png)
      
   * **Pregunta 2:** ¿Cuál es el hash SHA256 del archivo inicial malicioso?
     * Buscar el hash en las cabeceras HTTP o en el contenido del paquete.
     * **Respuesta:** 847b4ad90b1daba2d9117a8e05776f3f902dda593fb1252289538acf476c4268
       ![Pregunta2](https://github.com/Shispopo/Laboratorios-Ciberseguridad/blob/main/Cyberdefenders/DanaBot/Imagenes/2.1.png)
       ![Pregunta2.2](https://github.com/Shispopo/Laboratorios-Ciberseguridad/blob/main/Cyberdefenders/DanaBot/Imagenes/2.2.png)
       
   * **Pregunta 3:** ¿Qué proceso se utilizó para ejecutar el archivo inicial malicioso?
     * Buscar eventos relacionados con la creación de procesos.
     * **Respuesta:** wscript.exe
       
       ![Pregunta3](https://github.com/Shispopo/Laboratorios-Ciberseguridad/blob/main/Cyberdefenders/DanaBot/Imagenes/3.png)
       
   * **Pregunta 4:** ¿Cuál es la extensión del segundo archivo malicioso?
     * Buscar descargas adicionales y analizar la extensión del archivo.
     * **Respuesta:** .dll
       ![Pregunta4](https://github.com/Shispopo/Laboratorios-Ciberseguridad/blob/main/Cyberdefenders/DanaBot/Imagenes/4.png)
       
   * **Pregunta 5:** ¿Cuál es el hash MD5 del segundo archivo malicioso?
     * Buscar el hash MD5 en las cabeceras HTTP.
     * **Respuesta:** e758e07113016aca55d9eda2b0ffeebe
       ![Pregunta 5](https://github.com/Shispopo/Laboratorios-Ciberseguridad/blob/main/Cyberdefenders/DanaBot/Imagenes/5.1.png)
       ![Pregunta5.2](https://github.com/Shispopo/Laboratorios-Ciberseguridad/blob/main/Cyberdefenders/DanaBot/Imagenes/5.2.png)
       
   * **Pregunta 6:** ¿Cuál es la IP del atacante en el acceso inicial?
     * Identificar la dirección IP de origen de los paquetes iniciales.
     * **Respuesta:** 62.173.146.41
       ![Pregunta 6](https://github.com/Shispopo/Laboratorios-Ciberseguridad/blob/main/Cyberdefenders/DanaBot/Imagenes/6.png)
       
   * **Pregunta 7:** ¿Cuál es la última IP C2 de DanaBot?
     * Buscar conexiones a servidores conocidos por ser utilizados por DanaBot.
     * **Respuesta:** 91.201.67.85
       ![Pregunta7](https://github.com/Shispopo/Laboratorios-Ciberseguridad/blob/main/Cyberdefenders/DanaBot/Imagenes/7.png)

**Recomendaciones:**

* **Documentar todos los pasos:** Mantener un registro detallado de tu análisis.
* **Compartir tus hallazgos:** Contribuir a la comunidad de seguridad.
* **Practicar con diferentes escenarios:** Aumentar tu experiencia en análisis de tráfico de red.

**Nota:** Este laboratorio es solo un ejemplo. Puedes adaptar el procedimiento y agregar más detalles según tus necesidades y los resultados obtenidos.
