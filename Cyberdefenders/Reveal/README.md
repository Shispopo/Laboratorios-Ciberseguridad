## Reveal: Análisis Forense de un Volcado de Memoria

### Escenario
Como analista de ciberseguridad de una institución financiera líder, una alerta de su solución SIEM ha señalado actividad inusual en una estación de trabajo interna. Dados los datos financieros confidenciales en riesgo, se requiere una acción inmediata para prevenir posibles violaciones.
Su tarea es profundizar en el volcado de memoria proporcionado por el sistema comprometido. Es necesario identificar los indicadores básicos de compromiso (IOC) y determinar el alcance de la intrusión. Investigue los comandos o archivos maliciosos ejecutados en el entorno e informe de sus hallazgos en detalle para ayudar en la corrección y mejorar las defensas futuras.

### Objetivos
* Identificar el proceso malicioso que comprometió el sistema.
* Determinar la secuencia de acciones del atacante.
* Encontrar evidencias de exfiltración de datos.
* Correlcionar los hallazgos con las técnicas de ataque conocidas.

### Herramientas
* **Volatility 3:** Framework de volatilidad de memoria líder en la industria.

### Preguntas
  * Identificar el nombre del proceso malicioso ayuda a comprender la naturaleza del ataque. ¿Cómo se llama el proceso malicioso? powershell.exe
  * Conocer el ID de proceso principal (PPID) del proceso malicioso ayuda a rastrear la jerarquía del proceso y a comprender el flujo de ataque. ¿Cuál es el PID principal del proceso malicioso? 4120
  * Determinar el nombre de archivo utilizado por el malware para ejecutar la carga útil de la segunda etapa es crucial para identificar actividades maliciosas posteriores. ¿Cuál es el nombre de archivo que utiliza el malware para ejecutar la carga útil de la segunda etapa? 3435.dll
  * La identificación del directorio compartido en el servidor remoto ayuda a rastrear los recursos a los que se dirige el atacante. ¿Cómo se llama el directorio compartido al que se accede en el servidor remoto? davwwwroot
  * ¿Cuál es el ID de subtécnica de MITRE utilizado por el malware para ejecutar la carga útil de la segunda etapa? T1218.011
  * Identificar el nombre de usuario con el que se ejecuta el proceso malicioso ayuda a evaluar la cuenta comprometida y su posible impacto. ¿Cuál es el nombre de usuario con el que se ejecuta el proceso malicioso? Elon
  * Conocer el nombre de la familia de malware es esencial para correlacionar el ataque con amenazas conocidas y desarrollar defensas adecuadas. ¿Cómo se llama la familia de malware? StrelaStealer

### Procedimiento
1. **Preparación del Entorno:**
   * Descarga y instala Volatility 3.
   * Asegúrate de tener el volcado de memoria `192-Reveal.dmp` en tu directorio de trabajo.
2. **Identificación del Proceso Malicioso:**
   * Utiliza el comando `python3 vol.py -f 192-Reveal.dmp windows.pstree` para obtener una vista general de los procesos en ejecución.
   * Emplea `windows.malfind` para identificar procesos sospechosos.
3. **Análisis del Proceso Malicioso:**
   * Determina el proceso padre (PPID) utilizando `pstree`.
   * Encuentra el archivo ejecutado por el proceso malicioso con `windows.cmdline`.
   * Identifica la ruta del directorio compartido utilizando `strings` y buscando patrones específicos.
   * Mapea las técnicas utilizadas con la matriz MITRE ATT&CK.
4. **Investigación Adicional:**
   * Busca indicios de persistencia (registros de inicio, servicios).
   * Analiza la red para identificar comunicaciones con servidores externos.
   * Busca credenciales comprometidas.

### Resultados Esperados
Al finalizar el laboratorio, deberás ser capaz de:
* Identificar el malware utilizado.
* Describir las etapas del ataque.
* Evaluar el impacto del incidente.
* Proponer medidas de mitigación.
  
