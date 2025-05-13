# Sistema de Copias de Seguridad Automatizadas Multicapa

## 1. Arquitectura General del Sistema

- Nivel 1: ______________________________________
- Nivel 2: ______________________________________
- Nivel 3: ______________________________________

_(Explica brevemente la función de cada nivel. Puedes añadir un esquema o diagrama ASCII si lo deseas.)_

---

## 2. Configuración del Nivel 1: PCs Individuales

### a. Selección de software

- Windows: ______________________
- macOS: ________________________
- Linux: _________________________

_(Explica por qué has elegido cada uno.)_

### b. Programación de copias

- ¿Cómo se configuran las copias incrementales diarias?
- ¿Cómo se hacen las copias completas semanales?

### c. Destino de las copias

- ¿Dónde se almacenan?
- ¿Cómo se organizan las carpetas por PC?

---

## 3. Configuración del Nivel 2: Servidor Local Primario

### a. Tipo de hardware elegido

- Opción: *NAS*  *(Network Attached Storage)*
- Marca/modelo: *QNAP TS-473A*
- Sistema operativo: *Ubuntu*

### b. Tipo de RAID

- Elegido: *RAID 10*
- Justificación: *El RAID 10 ofrece mejoras en el rendimiento y también una tolerancia a fallos, lo malo que es mas caro que los demas raids.*

### c. Software de gestión

- Software elegido: *Veeam Backup & Replication*
- Función principal: *ayuda a las empresas de todos los tamaños a lograr una protección de datos completa para todas las cargas de trabajo, bien sean físicas, virtuales o cloud.*

---

## 4. Configuración del Nivel 3: Servidor Secundario Remoto

### a. Tipo de servidor remoto

- Opción elegida: *Nube (google)*
- Justificación: *acceso desde cualquier ubicación, alta disponibilidad, mantenimiento gestionado por el proveedor sin preocuparse del hardware, capia de datos con una protección contra fallos regionales.*

### b. Seguridad de la sincronización

- ¿Cómo se programa la sincronización?
  
  *Abres Drive, luego haces clic en configuración-preferencias, luego a la izquierda le das clic en Carpetas de tu ordenador, y por ultimo selecciona una opción: Sincronizar con Google Drive, ahora los archivos se reflejaran a la carpeta sincronizada*
- ¿Qué cifrado se usa?
  
  *Utiliza el protocolo de cifrado S/MIME se utiliza en coordinacion con las firmas digitales de S/MIME para garantizar la integridad del correo*
  
- ¿Se puede activar doble autenticación?
  
  *Para activar el 2FA en Google tienes que acceder al siguiente enlace [google.com](https://www.google.com/landing/2step/) y darle a empieza. Una vez dentro, habrá que introducir la contraseña para poder verificar así la identidad*

---

## 5. Automatización del Proceso

- Script de verificación: _(pega o enlaza un ejemplo)_
- Alerta por email: ¿Cómo se configura?
- Prueba de restauración: ¿Cada cuánto tiempo? ¿Cómo?

---

## 6. Justificación del uso de RAID

- ¿Por qué no sustituye al backup?
- ¿Qué pasa si solo tenemos RAID?

---

## 7. Resumen de Software Recomendado

| Función                        | Software Recomendado     |
|-------------------------------|--------------------------|
| Gestión centralizada          |                          |
| Sincronización entre servidores|                          |
| Monitorización                |                          |

_(Puedes añadir más si lo crees necesario)_

---

## Bibliografía / Fuentes consultadas

- Fuente 1: Reddit
- Fuente 2: [www.3digits.es](https://www.3digits.es/veeam-backup-replication#:~:text=Veeam%20Backup%26Replication%2C%20la%20herramienta%20de,sean%20f%C3%ADsicas%2C%20virtuales%20o%20cloud.)
- [Google Help](https://support.google.com/mail/answer/13317990?hl=es#:~:text=Protocolo%20de%20cifrado&text=509%20en%20los%20que%20conf%C3%ADe,garantizar%20la%20integridad%20del%20correo.)
- [Google Help](https://support.google.com/drive/answer/10838124?hl=es)
- [](https://www.ciberseguridad.eus/hogar-seguro/como/como-se-activa-el-factor-de-doble-autenticacion-2fa-en-google#:~:text=Para%20activar%20el%202FA%20en,poder%20verificar%20as%C3%AD%20la%20identidad.)
- ...

