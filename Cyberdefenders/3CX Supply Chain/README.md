## Análisis del Ataque a la Cadena de Suministro de 3CX

### Escenario
Una gran corporación multinacional depende en gran medida del software 3CX para la comunicación telefónica, lo que lo convierte en un componente crítico de sus operaciones comerciales. Después de una actualización reciente de la aplicación de escritorio 3CX, las alertas antivirus señalan instancias esporádicas de que el software se borra de algunas estaciones de trabajo, mientras que otras no se ven afectadas. Al descartar esto como un falso positivo, el equipo de TI pasa por alto las alertas, solo para notar un rendimiento degradado y un tráfico de red extraño a servidores desconocidos. Los empleados informan problemas con la aplicación 3CX y el equipo de seguridad de TI identifica patrones de comunicación inusuales relacionados con actualizaciones de software recientes.
Como analista de inteligencia de amenazas, es su responsabilidad examinar este posible ataque a la cadena de suministro. Sus objetivos son descubrir cómo los atacantes comprometieron la aplicación 3CX, identificar al posible actor de amenazas involucrado y evaluar el alcance general del incidente.

## Objetivos
* Identificar los archivos maliciosos introducidos en las versiones comprometidas de 3CX.
* Analizar el comportamiento del malware y determinar su funcionalidad.
* Identificar los indicadores de compromiso (IOCs) asociados con el ataque.
* Determinar la familia del malware y el actor de la amenaza potencialmente involucrado.
* Evaluar el impacto del ataque en los sistemas comprometidos.

## Herramientas
* **VirusTotal:** Plataforma de análisis de archivos maliciosos.

## Preguntas y procedimiento:
* **Pregunta 1**
  Comprender el alcance del ataque e identificar qué versiones presentan El comportamiento malicioso es crucial para tomar decisiones informadas si estas versiones comprometidas están presentes en la organización. ¿Cuántas versiones de 3CX que se ejecutan en Windows han sido marcadas como malware?
  Respuesta: 2
  * Según un hilo de discusión en la comunidad 3CX (https://www.3cx.com/community/threads/3cx-desktop-marked-as-malware-by-sentinelone.123877/), al menos dos versiones de 3CX DesktopApp para Windows han sido identificadas como maliciosas por soluciones de seguridad. Sin embargo, es posible que existan más versiones comprometidas que aún no hayan sido detectadas.
    ![Cantidad de Versiones](https://github.com/Shispopo/Laboratorios-Ciberseguridad/blob/main/Cyberdefenders/3CX%20Supply%20Chain/Imagenes/1.png)

* **Pregunta 2**
  Determinar la antigüedad del malware puede ayudar a evaluar el alcance del compromiso y realizar un seguimiento de la evolución de las familias y variantes de malware. ¿Cuál es la hora UTC de creación del malware .msi?
  Respuesta: 2023-03-13 06:33:26 UTC
  * El análisis de la muestra del malware .msi en VirusTotal indica que fue creado el 13 de marzo de 2023 a las 06:33:26 UTC. Esta información se encuentra en la sección "Detalles" del informe de VirusTotal.
    ![Hora de creacion del malware](https://github.com/Shispopo/Laboratorios-Ciberseguridad/blob/main/Cyberdefenders/3CX%20Supply%20Chain/Imagenes/2.png)

* **Pregunta 3**
  Los archivos ejecutables (.exe) se utilizan con frecuencia como cargas útiles de malware primarias o secundarias, mientras que las bibliotecas de enlaces dinámicos (.dll) A menudo cargan código malicioso o mejoran la funcionalidad del malware. El análisis de los archivos depositados por el El instalador de software de Microsoft (.msi) es crucial para identificar archivos maliciosos e investigar todo su potencial. ¿Qué archivos DLL malintencionados quitó el archivo .msi?
  Respuesta: ffmpeg.dll d3dcompiler_47.dll
  * Para identificar los archivos DLL maliciosos ffmpeg.dll y d3dcompiler_47.dll, se realizó un análisis en VirusTotal y nos dirigimos al apartado Detecciones. Se examinaron los nombres de los archivos, comparándolos con sus funciones legítimas y observando si su presencia en un contexto malicioso era inusual. Además, se utilizó el análisis de comportamiento para observar cómo estos archivos interactuaban con el sistema, buscando acciones sospechosas como el acceso no autorizado a recursos del sistema o la comunicación con servidores externos. También se compararon los hashes de los archivos con bases de datos de firmas de malware conocidas para verificar si habían sido identificados previamente como maliciosos. Finalmente, se consideraron las funciones legítimas de estos archivos para entender cómo podrían ser explotadas con fines malintencionados. Al combinar toda esta información, se pudo concluir con alta certeza que estos archivos eran parte de una infección maliciosa y representaban una amenaza para el sistema..
    ![Archivos malintencionados](https://github.com/Shispopo/Laboratorios-Ciberseguridad/blob/main/Cyberdefenders/3CX%20Supply%20Chain/Imagenes/3.png)

* **Pregunta 4**
  Reconocer las técnicas de persistencia utilizadas en este incidente es esencial para las estrategias de mitigación actuales y futuras. Mejoras en la defensa. ¿Cuál es el ID de subtécnica de MITRE empleado por los archivos .msi para cargar la DLL maliciosa?
  Respuesta: T1574.002
  * La subtécnica de MITRE T1574.002, "DLL Side-Loading", es la más probable para describir la técnica empleada por los archivos .msi para cargar la DLL maliciosa. Esta técnica consiste en aprovechar vulnerabilidades en la forma en que Windows carga bibliotecas dinámicas (DLLs) para cargar una DLL maliciosa en un proceso legítimo. Al analizar el informe de Qualys sobre el ataque a 3CX DesktopApp, se puede observar cómo los atacantes explotaron esta técnica para lograr persistencia en los sistemas comprometidos.
    ![ID MITRE](https://github.com/Shispopo/Laboratorios-Ciberseguridad/blob/main/Cyberdefenders/3CX%20Supply%20Chain/Imagenes/4.png)
  
* **Pregunta 5**
  Reconocer el tipo de malware (categoría de amenaza) es esencial para su investigación, ya que puede ofrecer información valiosa sobre el malware. posibles acciones maliciosas que examinará. ¿Cuál es la familia de malware de las dos DLL maliciosas?
  Respuesta: Trojan
  * En la sesión principal de VirusTotal se puede encontrar la familia de malware.
    ![Familia Malware](https://github.com/Shispopo/Laboratorios-Ciberseguridad/blob/main/Cyberdefenders/3CX%20Supply%20Chain/Imagenes/5.png)
    
* **Pregunta 6**
  Como analista de inteligencia de amenazas que realiza análisis dinámicos, es vital comprender cómo el malware puede evadir la detección en entornos virtualizados o sistemas de análisis. Este conocimiento le ayudará a mitigar o abordar eficazmente estas evasivas táctica. ¿Cuál es el identificador de MITRE para las técnicas de evasión de virtualización/espacio aislado que usan los dos archivos DLL malintencionados?
  Respuesta: T1497
  * Dirigirse a la sesion de Comportamiento, Evasion de defensa. La técnica T1497 de MITRE ATT&CK se refiere a las técnicas utilizadas por los atacantes para detectar si el malware está siendo ejecutado en un entorno virtualizado o aislado, como un sandbox. Al identificar esta técnica, podemos inferir que los atacantes están intentando evadir el análisis de seguridad y ejecutar su código malicioso sin ser detectados
    ![Identificador Mitre](https://github.com/Shispopo/Laboratorios-Ciberseguridad/blob/main/Cyberdefenders/3CX%20Supply%20Chain/Imagenes/6.png)

* **Pregunta 7**
  Al realizar análisis de malware e ingeniería inversa, es vital comprender las técnicas de antianálisis perdiendo el tiempo. ¿A qué hipervisor se dirigen las técnicas de antianálisis del archivo ffmpeg.dll?
  Respuesta: VMware
  * Nos diriguimos al archivo ffmpeg.dll y lo abrimos en VirusTotal.
  * En la sesión de comportamiento desplegamos evasion de defensa. La técnica de antianálisis específica del archivo ffmpeg.dll está dirigida al hipervisor VMware. Esto sugiere que los atacantes han desarrollado técnicas para detectar y evadir los mecanismos de seguridad implementados en entornos virtualizados utilizando VMware.
  * Hacer click en el ffmpeg.dll para abrir otra página de VirusTotal.
    ![Hipervisor](https://github.com/Shispopo/Laboratorios-Ciberseguridad/blob/main/Cyberdefenders/3CX%20Supply%20Chain/Imagenes/7.1.png)
  * Ver el comportamiento.
    
    ![Hipervisor](https://github.com/Shispopo/Laboratorios-Ciberseguridad/blob/main/Cyberdefenders/3CX%20Supply%20Chain/Imagenes/7.2.png)
    
* **Pregunta 8**
  Identificar el método criptográfico utilizado en el malware es crucial para comprender las técnicas empleadas para eludir los mecanismos de defensa y ejecutar sus funciones en su totalidad. ¿Qué algoritmo de cifrado utiliza el archivo ffmpeg.dll?
  Respuesta: RC4
  * En la sesión de comportamiento desplegamos evasión de defensa. El archivo ffmpeg.dll utiliza el algoritmo de cifrado RC4 para proteger sus comunicaciones y datos. RC4 es un algoritmo de cifrado de flujo que ha sido ampliamente utilizado, pero también ha sido objeto de numerosas críticas debido a sus vulnerabilidades.
    ![Cifrado](https://github.com/Shispopo/Laboratorios-Ciberseguridad/blob/main/Cyberdefenders/3CX%20Supply%20Chain/Imagenes/8.png)
    
* **Pregunta 9**
  Como analista, ha reconocido algunos TTP involucrados en el incidente, pero identificar al grupo de APT responsable le ayudará busca sus TTP habituales y descubre otras posibles actividades maliciosas. ¿Qué grupo es responsable de esto? ¿atacar?
  Respuesta: Lazarus
  * Basándose en el informe de Qualys, se ha determinado que el grupo de hackers Lazarus es el principal sospechoso detrás de este ataque. Lazarus es un grupo de hackers patrocinado por el estado, conocido por sus sofisticadas campañas de ciberespionaje y ciberataques.(https://blog.qualys.com/vulnerabilities-threat-research/2023/04/03/3cxdesktopapp-backdoored-in-a-suspected-lazarus-campaign).
  ![Grupo](https://github.com/Shispopo/Laboratorios-Ciberseguridad/blob/main/Cyberdefenders/3CX%20Supply%20Chain/Imagenes/9.png)

## Recomendaciones
* **Aislar los sistemas comprometidos:** Evitar la propagación del malware.
* **Cambiar contraseñas:** Cambiar todas las contraseñas de las cuentas afectadas.
* **Escanear todos los sistemas:** Realizar un escaneo completo de todos los sistemas en busca de malware.
* **ctualizar software:** Mantener todos los sistemas y software actualizados con los últimos parches de seguridad.
* **Implementar una solución EDR:** Utilizar una solución de detección y respuesta a endpoints para detectar y responder a amenazas en tiempo real.

## Conclusión
El ataque a la cadena de suministro de 3CX destaca la importancia de mantener una buena higiene de seguridad y estar atentos a las amenazas emergentes. Al realizar un análisis forense exhaustivo, podemos comprender mejor las tácticas utilizadas por los atacantes y tomar medidas para proteger nuestros sistemas.

**Recomendaciones:**

* **Documentar todos los pasos:** Mantener un registro detallado del proceso de análisis.
* **Compartir los resultados:** Contribuir a la comunidad de seguridad compartiendo tus hallazgos.
* **Mantenerse actualizado:** Estar al tanto de las últimas amenazas y herramientas de análisis.

**Nota:** Este laboratorio es solo un ejemplo. Puedes adaptar el procedimiento y agregar más detalles según tus necesidades y los resultados obtenidos.
