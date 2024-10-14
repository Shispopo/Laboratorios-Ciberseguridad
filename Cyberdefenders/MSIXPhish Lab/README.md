# MSIXPhish Lab

## Escenario
Como analista de inteligencia de amenazas en una importante empresa de seguridad, desempeña un papel en la recopilación eficiente de información sobre posibles amenazas. Durante su jornada laboral, un respondedor de incidentes le ha proporcionado un hash asociado a un instalador de software malintencionado detectado en la red de su organización. Su tarea es analizar este hash para recopilar información valiosa sobre amenazas y mejorar las defensas de su organización.

## Preguntas y procedimiento:
  * Para mitigar eficazmente la amenaza, es importante determinar el origen o la categoría de este malware. ¿Puede identificar a qué familia de malware está asociada esta muestra para comprender mejor sus comportamientos típicos y los riesgos asociados?
      * Respuesta: Batloader
      * Subir el archivo a VirusTotal:
          * Accede a la página principal de VirusTotal: https://www.virustotal.com/
          * Utiliza la opción para cargar el archivo (arrastrar y soltar o seleccionar desde tu dispositivo).
      * Esperar los resultados del análisis:
          * VirusTotal realizará un análisis completo del archivo utilizando múltiples motores antivirus.
          * Este proceso puede tomar unos minutos.
      * Revisar los resultados:
          * Una vez finalizado el análisis, se mostrará un informe detallado.
          * Busca la sección de "Detecciones". Aquí encontrarás una lista de los motores antivirus que han identificado el archivo como malicioso.
          * Identifica la etiqueta de amenaza más común o popular. Esta etiqueta te dará una buena indicación de la familia de malware a la que pertenece el archivo. En este caso, la etiqueta más común fue "Batloader".
           ![]() 
        
  * Es importante identificar la primera aparición pública del malware para realizar un seguimiento eficaz de su historial y propagación. ¿Puede proporcionar la fecha y hora de envío inicial de este malware en VirusTotal?
      * 12-12-2023 18:08:13
      * Acceder al informe de VirusTotal: Asegúrate de estar en la página del informe detallado del archivo que estás analizando.
      * Buscar la pestaña "Detalles" o "Información": Esta pestaña suele contener datos exhaustivos sobre el archivo, incluyendo su historial de detección.
      * Localizar la sección "Historia" o "Primera detección": Dentro de la pestaña "Detalles", busca una sección específica que indique el historial de detecciones del archivo. Esta sección podría estar titulada "Historia", "Primera detección" o algo similar.
      * Identificar la fecha y hora: En esta sección, encontrarás la fecha y hora en que el archivo fue detectado por primera vez en la base de datos de VirusTotal. Esta será la primera aparición pública registrada del malware.
       ![]()
            
  * El reconocimiento de una técnica MITRE específica empleada por el malware ayuda a desarrollar estrategias de defensa específicas. ¿Cuál es el ID de MITRE de la técnica utilizada por el malware para la recopilación de datos?
      * T1056
      * Acceder al informe de VirusTotal: Asegúrate de estar en la página del informe detallado del archivo que estás analizando.
      * En el informe, busca una sección que detalle el comportamiento del malware. Esta sección puede estar titulada "Comportamiento", "Técnicas" o algo similar.
      * Dentro de la sección de comportamiento, busca una subsección o tabla que se refiera a MITRE ATT&CK. MITRE ATT&CK es un marco de trabajo para describir las tácticas y técnicas utilizadas por los adversarios cibernéticos.
        ![]()
        
  * Conocer los nombres de los archivos ejecutables arrojados por el malware ayuda a detectar y aislar las máquinas infectadas. ¿Cuál es el nombre del archivo ejecutable que arroja el malware?
      * Install.exe
      * Acceder al informe de VirusTotal: Asegúrate de estar en la página del informe detallado del archivo que estás analizando.
      * En el informe, busca una sección que detalle los archivos relacionados con el malware. Esta sección puede estar titulada "Relaciones", "Archivos relacionados", "Archivos agrupados" o algo similar.
      * Dentro de esta sección, encontrarás una lista de archivos que están asociados con el malware. Busca el archivo que tenga una extensión típica de ejecutable, como .exe, .dll, o .scr. Este archivo es el que el malware utiliza para llevar a cabo sus acciones.
        ![]()
        
  * Continuando con la pregunta anterior. ¿Puede identificar el nombre del segundo padre de ejecución observado en la naturaleza para el ejecutable detectado?
      * ZoomInstaller.msix
      * Acceder al informe de VirusTotal: Asegúrate de estar en la página del informe detallado del archivo ejecutable que estás analizando (por ejemplo, Install.exe).
      * Dentro del informe, busca una sección que detalle los procesos que han iniciado o cargado el archivo ejecutable. Esta sección puede estar titulada "Relaciones", "Padres de ejecución" o algo similar.
      * En esta sección, encontrarás información sobre el proceso que inició directamente al archivo ejecutable (Install.exe). Este es el primer padre de ejecución.
      * Generalmente, al hacer clic en el nombre del primer padre, se abrirá un nuevo informe de VirusTotal para ese archivo específico.
      * En el nuevo informe del primer padre, busca nuevamente la sección de "Relaciones" o "Padres de ejecución". Aquí encontrarás información sobre el proceso que inició al primer padre. Este será el segundo padre de ejecución que estás buscando.
        ![]()
        
  * La identificación de los dominios utilizados en los ataques puede ayudar a bloquear futuras comunicaciones maliciosas y a comprender la infraestructura de los atacantes. ¿Qué dominio utiliza el actor de amenazas para alojar el instalador de aplicaciones ilegítimo?
      * scheta.site
      * Acceso a VirusTotal:
          * Asegurarse de tener una cuenta en VirusTotal y haber iniciado sesión.
          * Dirigirse a la sección "Comunidad".
      * Buscar la publicación:
          * Utilizar los filtros de búsqueda para localizar la publicación específica del blog de Microsoft que menciona el malware en cuestión.
          * Puede ser necesario utilizar palabras clave como "scheta.site", "instalador ilegítimo", el nombre del malware (si se conoce) o cualquier otra información relevante.
      * Revisar la sección de "Direcciones URL":
          * Una vez localizada la publicación, buscar la sección específica que detalla las direcciones URL asociadas al malware.
          * Esta sección podría incluir una lista de dominios, direcciones IP o enlaces a archivos.
            ![]()
        
  * Necesitamos identificar el vector de acceso del que abusa el malware para mitigarlo. ¿Qué controlador de protocolo explota el malware?
      * ms-appinstaller
      * Utilizando los mismos criterios de búsqueda que en la pregunta anterior, localizar nuevamente la publicación del blog de Microsoft que analiza el malware.
      * Buscar la sección inicial o introducción:
          * Dirigirse al inicio del artículo o a la sección introductoria.
      * Identificar el esquema URI:
          * Prestar especial atención a la mención del esquema URI. El esquema URI es la parte inicial de una dirección web que especifica el protocolo a utilizar (por ejemplo, http://, https://, mailto:, etc.).
          * En este caso, se nos indica que el malware explota el esquema "ms-appinstaller".
            ![]()   
        
  * Descubrir al actor de amenazas asociado con este malware es clave para comprender sus tácticas, técnicas y procedimientos (TTP) y reforzar las defensas contra futuros ataques. ¿Puede proporcionar el nombre del actor de amenazas?
      * Storm-0569
      * Regresar a la publicación del blog de Microsoft en VirusTotal que hemos analizado en las preguntas anteriores.
      * Buscar la sección inicial:
          * Concentrarse en la introducción o primeras secciones del artículo.
      * Identificar al actor de amenazas:
          * Los actores de amenazas suelen ser mencionados al principio del análisis, junto con una breve descripción de sus actividades y objetivos.
          * En este caso, se nos proporciona el nombre del actor de amenazas: Storm-0569.
            ![]()
    
## Análisis del Malware

### Información Básica
* **Familia de malware:** Batloader
* **Fecha de envío inicial a VirusTotal:** 12-12-2023 18:08:13
* **Técnica MITRE:** T1056 (Data from Local System)
* **Archivos ejecutables:** Install.exe
* **Padre de ejecución:** ZoomInstaller.msix
* **Dominio asociado:** scheta.site
* **Vector de acceso:** ms-appinstaller
* **Actor de amenazas:** Storm-0569

### Análisis Detallado

#### Comportamiento del Malware
* **Infección inicial:** El malware se disfraza como un instalador legítimo (ZoomInstaller.msix) y se aprovecha del protocolo ms-appinstaller para infectar los sistemas.
* **Recopilación de datos:** Utiliza la técnica T1056 para recopilar información del sistema local, lo que podría incluir credenciales, listas de archivos y datos sensibles.
* **Comunicación con el C2:** Se comunica con el servidor de comando y control (C2) ubicado en scheta.site para recibir nuevas instrucciones y enviar datos exfiltrados.

#### Implicaciones de Seguridad
* **Riesgo de pérdida de datos:** La recopilación de datos sensibles puede llevar a la exposición de información confidencial de la organización.
* **Pérdida de control del sistema:** El malware puede permitir a los atacantes tomar el control remoto de los sistemas infectados.
* **Propagación lateral:** El malware podría propagarse a otros sistemas dentro de la red.

### Recomendaciones
* **Bloquear el dominio:** Implementar medidas para bloquear el acceso al dominio scheta.site en la red.
* **Detectar y eliminar el malware:** Utilizar herramientas de detección de malware y análisis forense para identificar y eliminar las infecciones.
* **Actualizar software y sistemas:** Mantener todos los sistemas operativos, aplicaciones y software antivirus actualizados con los últimos parches de seguridad.
* **Segmentar la red:** Implementar una arquitectura de red segmentada para limitar la propagación del malware en caso de infección.
* **Educar a los usuarios:** Concientizar a los usuarios sobre los riesgos de abrir archivos adjuntos desconocidos o hacer clic en enlaces sospechosos.
* **Monitorear la actividad de la red:** Implementar sistemas de detección de intrusiones (IDS) y sistemas de prevención de intrusiones (IPS) para monitorear la actividad de la red y detectar posibles ataques.

### Herramientas Utilizadas
* **VirusTotal:** Para analizar el hash del malware y obtener información sobre su comportamiento.
* **Whois:** Para obtener información sobre el dominio scheta.site.
* **Microsoft Security Blog:** Para obtener información sobre la campaña de ataques relacionada con ms-appinstaller.

## Próximos Pasos
* **Análisis en profundidad:** Realizar un análisis más profundo del malware utilizando herramientas de ingeniería inversa para comprender mejor su funcionamiento interno.
* **Correlación con otras amenazas:** Buscar conexiones entre este malware y otras campañas de ataques.
* **Desarrollo de IOCs:** Crear indicadores de compromiso (IOCs) para detectar futuras infecciones.
* **Actualización de las reglas de detección:** Actualizar las reglas de detección de las herramientas de seguridad para identificar este tipo de amenazas.

**Nota:** Este documento es un punto de partida para el análisis de este malware. A medida que se obtenga más información, se actualizará y ampliará.
