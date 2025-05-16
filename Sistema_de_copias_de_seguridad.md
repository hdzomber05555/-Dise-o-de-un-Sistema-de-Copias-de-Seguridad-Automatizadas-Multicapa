# Sistema de Copias de Seguridad Automatizadas Multicapa

## 1. Arquitectura General del Sistema

- Nivel 1:
- [Excalidraw](https://excalidraw.com/#json=sExitgzTmohY4HilrJ1S_,_CiUXweu6SSm5nLjBF0iSQ)
  La arquitectura de backups de tres niveles sigue la estrategia 3-2-1 para garantizar la seguridad de los datos. El Nivel 1 son los datos primarios en producción, almacenados en dispositivos de acceso rápido como discos SSD, HDD o servidores activos. Estos no son backups, sino la fuente original de información.
- Nivel 2:
  El Nivel 2 es la primera capa de backup, ubicada localmente, y su función es permitir recuperaciones rápidas ante fallos técnicos. Aquí se usan dispositivos como HDD adicionales, NAS o sistemas RAID, que ofrecen redundancia dentro del mismo entorno físico.
- Nivel 3:
  el Nivel 3 es la copia remota, diseñada para proteger los datos en casos de desastres como incendios o robos. Se almacena fuera del sitio principal, usando medios como cintas magnéticas, la nube (AWS, Backblaze) o discos externos en ubicaciones seguras. La regla 3-2-1 resumen esta estructura: 3 copias totales (original + 2 backups), en 2 tipos de medios distintos (ej. disco y cinta), con al menos 1 copia fuera del sitio.

---

## 2. Configuración del Nivel 1: PCs Individuales

### a. Selección de software

- Windows: Veeam Agent for Microsoft
  He elegido este software ya que se pueden hacer copias de seguridad y restauraciones completamente gratis, la interfaz es muy sencilla de usar, además de poder hacer copias incrementales y completas de manera diaria programandolo.
- macOS: Carbon Copy Cloner
  He elegido este ya que se pueden hacer copias de seguridad completas e incrementales totalmente gratis, a diferencia de la nativa de apple que solo permite hacer incrementales, también permite hacer clonaciones
- Linux: TimeShift
  He elegido este ya que es bastante completo, aparte de ser muy simple, osea, hace lo justo y necesario, es totalmente gratuito de una persona de github.

### b. Programación de copias

- ¿Cómo se configuran las copias incrementales diarias?
  Windows: Veeam Agent for Microsoft Windows realizará una copia de seguridad incremental utilizando la configuración del trabajo de copia de seguridad programado y agregará un nuevo punto de restauración a la cadena de copia de seguridad en la ubicación de destino.
  ![Imagen1](https://helpcenter.veeam.com/docs/agentforwindows/userguide/images/ep_incremental_backup_launch_free.png)
  
  MacOs: Una vez abras la aplicación tendremos que darle a new task para empezar a crear la backup, tendremos que seleccionar el origen de los datos, luego el destino, luego en la seccion cloning options, tendremos que marcar la opción incremental backup, para programarla para que se haga diariamente tendremos que hacer click en schedule y elegir la frecuencia daily, ponemos la hora que queramos, lo mejor seria en la madrugada y guardar la configuracion
  ![Imagen3](https://images.macrumors.com/article-new/2021/05/carbon-copy-cloner-6.jpg)
  
  Linux: Nada mas se abra el software recomiendo darle a la opción rsync ya que con eso podremos hacer copias incrementales, pero ojo, solo podemos hacer copias incrementales, pero si es la primera copia que hacemos se hace una copia completa aunque no te lo indique, bueno una vez elegido rsync elegiremos donde guardar las copias de seguridad, tal como digo abajo, habria que usar esa distribución de carpetas, una vez hecho eso podremos elegir con que frecuencia se harán las copias, se pueden hacer mensualmente, semanalmente, diariamente, cada hora, e incluso con cada arranque, en este caso seleccionaremos diariamente, luego de eso tendremos que ir a configuración para indicar el origen de la copia, en la pestaña filtros podremos selccionar las carpetas que quermeos que haga backup, luego de todo eso simplemente le daremos a crear y se nos hara la primera, la cual es la completa, a partir de ahí, serán incrementales
  ![Imagen4](https://atareao.es/wp-content/uploads/2018/02/Captura-de-pantalla-de-2018-02-17-07-15-46.png)
- ¿Cómo se hacen las copias completas semanales?
  Windows: Para hacer una copia de seguridad completa semanal, cuando le demos a active full backup, se nos abrira un software de ayuda para hacer la backup, primero tendremos que elegir el nombre, luego el tipo de copia y seleccionamos el pc entero, o las carpetas que queramos, luego seleccionamos si queremos que se haga de forma local o en la nube y cuando seleccionemos el directorio donde se hara la copia, abajo veremos que pone avanzado, el daremos y ahí podremos elegir que se haga de manera automática los dias que queramos.
  ![Imagen2](https://helpcenter.veeam.com/docs/agentforwindows/userguide/images/ep_backup_job_settings_backup.png)
  
  MacOs: Para hacer una copia de seguridad completa semanal, tendremos que hacer exactamente lo mismo que con la incremental, solamente cambiando el tipo de backup a completa, luego de eso simplemente tenemos que decirle que se haga semanalmente y ya esta.
  
  Linux: Con linux, como he dicho anteriormente, las copias completas se hacen haciendo la primera copia, para ello simplemente tendremos que usar el sistema de organización de carpetas que comento abajo, dentro de las backups completas, como es un origen totalmente distinto, se estarán haciendo copias completas constantemente, y las incrementales se seguiran haciendo en su sitio.

### c. Destino de las copias

- ¿Dónde se almacenan?
  Tanto en Windows como en MacOs y en Linux, se almacenaran donde le indiquemos en el gestor de backups
- ¿Cómo se organizan las carpetas por PC?
  Tanto en Windows como en MacOs y en Linux, las carpetas habria que organizarlas de esta manera, en una carpeta llamada backups, tener otras 2 carpetas, una llamada completas y la otra incrementales, dentro de cada una deberia haber otras carpetas las cuales se llamen backup_completa/incremental con su respectiva fecha en la cual se hizo.

---

## 3. Configuración del Nivel 2: Servidor Local Primario

### a. Tipo de hardware elegido

- Opción: NAS  (Network Attached Storage)
- Marca/modelo: QNAP TS-473A
- Sistema operativo: Ubuntu

### b. Tipo de RAID

- Elegido: RAID 10
- Justificación: El RAID 10 ofrece mejoras en el rendimiento y también una tolerancia a fallos, lo malo que es mas caro que los demas raids.

### c. Software de gestión

- Software elegido: Veeam Backup & Replication
- Función principal: ayuda a las empresas de todos los tamaños a lograr una protección de datos completa para todas las cargas de trabajo, bien sean físicas, virtuales o cloud.

---

## 4. Configuración del Nivel 3: Servidor Secundario Remoto

### a. Tipo de servidor remoto

- Opción elegida: Nube (google)
- Justificación: acceso desde cualquier ubicación, alta disponibilidad, mantenimiento gestionado por el proveedor sin preocuparse del hardware, capia de datos con una protección contra fallos regionales.

### b. Seguridad de la sincronización

- ¿Cómo se programa la sincronización?
  
  Abres Drive, luego haces clic en configuración-preferencias, luego a la izquierda le das clic en Carpetas de tu ordenador, y por ultimo selecciona una opción: Sincronizar con Google Drive, ahora los archivos se reflejaran a la carpeta sincronizada
- ¿Qué cifrado se usa?
  
  Utiliza el protocolo de cifrado S/MIME se utiliza en coordinacion con las firmas digitales de S/MIME para garantizar la integridad del correo
- ¿Se puede activar doble autenticación?
  
  Para activar el 2FA en Google tienes que acceder al siguiente enlace [google.com](https://www.google.com/landing/2step/) y darle a empieza. Una vez dentro, habrá que introducir la contraseña para poder verificar así la identidad

---

## 5. Automatización del Proceso

- Script de verificación:

@echo off
dsmc q vm sql01_SQL -detail -asnode=datacenter01 | find /c
“database-level recovery” > c:\temp.txt
SET /p VAR=<c:\temp.txt

if %VAR% == “1” (
tdpsqlc back * log
) ELSE (
echo “There is no full backup”
set ERRORLEVEL=1
)

- Alerta por email: ¿Cómo se configura?
  (imagen1)https://static.vecteezy.com/system/resources/previews/055/637/733/non_2x/holographic-email-alert-with-warning-signal-being-handled-by-a-professional-vector.jpg

Crear una alerta
Ve a Alertas de Google.
En el cuadro de la parte superior, introduce el tema que quieras seguir.
Para cambiar la configuración, haz clic en Mostrar opciones. Puedes cambiar:
La frecuencia con la que recibes notificaciones
Los tipos de sitio web que verás
El idioma
La zona del mundo de la que quieres recibir información
El número de resultados que quieres ver
Las cuentas que reciben la alerta
Haz clic en Crear alerta. Recibirás correos electrónicos cada vez que encontremos resultados de búsqueda que coincidan con tu selección.

(imagen2)https://i.blogs.es/7d8edb/crear-punto-de-restauracion-windows-11/840_560.jpg

- Prueba de restauración: ¿Cada cuánto tiempo? ¿Cómo?

Lo primero que hay que hacer es tener una politica de contraseñas que dicte las frecuencias y los procedimientos de respaldo para cada sistema. Es importante también revisar las copias para asegurarse de que son correctas y precisas y no van a dar problema a la hora de restaurarse. Para las pruebas de restauración es recomendable programar las pruebas en un entorno separado del de la producción para evitar cualquier impacto en aplicaciones y servicios en uso. Es importante también utilizar una solución de copia de seguridad fiable para asegurarse de que los datos puedan recuperarse de forma rapida y faci.

---

## 6. Justificación del uso de RAID

![imagen8](https://media.kingston.com/kingston/articles/windows10backup-diy5-ep94.jpg)

- ¿Por qué no sustituye al backup?

Porque pueden seguirse produciendo perdidas de datos ya que aunque tengamos un RAID algunos archivos pueden quedar inutilizables y los que son borrados accidentalmente no podrían ser recuperados sin más.

![imagen9](https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcSoSu_LBVcCtZBHcoBfJTd-fM3I85P7p1NvlA&s)

- ¿Qué pasa si solo tenemos RAID?

Pues que podriamos continuar el trabajo sin interrupciones si alguno de los discos fallan pero si hay algun error no podremos volver a un estado anterior o si falla el raid en si.
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

## 7. Resumen de Software Recomendado

| Función                        | Software Recomendado     |
|-------------------------------|--------------------------|
| Gestión centralizada          | Scalefusion, SuperOps, Desktop Central, LogMeIn                        |
| Sincronización entre servidores| AOMEI Backupper Server, Replidacion DFS,                          |
| Monitorización                | Pandora FMS, Nagios, Centreon, Netdata, Zabbix, Asana                         |

---

## Bibliografía / Fuentes consultadas

- Fuente 1: Reddit
- Fuente 2: [www.3digits.es](https://www.3digits.es/veeam-backup-replication#:~:text=Veeam%20Backup%26Replication%2C%20la%20herramienta%20de,sean%20f%C3%ADsicas%2C%20virtuales%20o%20cloud.)
- [Google Help](https://support.google.com/mail/answer/13317990?hl=es#:~:text=Protocolo%20de%20cifrado&text=509%20en%20los%20que%20conf%C3%ADe,garantizar%20la%20integridad%20del%20correo.)
- [Google Help](https://support.google.com/drive/answer/10838124?hl=es)
- [ciberseguridad](https://www.ciberseguridad.eus/hogar-seguro/como/como-se-activa-el-factor-de-doble-autenticacion-2fa-en-google#:~:text=Para%20activar%20el%202FA%20en,poder%20verificar%20as%C3%AD%20la%20identidad.)
- Fuente 3: [atareao](https://atareao.es/software/seguridad/backups-con-timeshift/)
- Fuente 4: [Carbon Copy](https://forums.macrumors.com/threads/bombich-software-announces-carbon-copy-cloner-6-featuring-faster-backups-quick-updates-snapshot-navigator-and-more.2296895/)
- Fuente 5: [Veeam Microsoft](https://helpcenter.veeam.com/docs/agentforwindows/userguide/backup_active_full.html?ver=60)
- Fuente 6: [IBM](https://www.ibm.com/docs/es/spfve/8.1.25?topic=pmssdihve-sample-script-validating-full-virtual-machine-backups) [Google](https://support.google.com/websearch/answer/4815696?hl=es) [Linkedin](https://es.linkedin.com/pulse/el-poder-de-las-pruebas-restauraci%C3%B3n-c%C3%B3mo-puede-la-los-consultor-it)
- Fuente 7: [Langmeier](https://www.langmeier-software.com/es/seiten/news/was-ist-der-unterschied-zwischen-raid-und-backup)
- Fuente 8: [LeyProteccion](https://ayudaleyprotecciondatos.es/2021/05/13/software-monitorizacion/) [Ubackup](https://www.ubackup.com/es/windows-server/sincronizar-archivos-entre-servidores-de-windows.html) [Geekflare](https://geekflare.com/es/best-desktop-management-software/)

