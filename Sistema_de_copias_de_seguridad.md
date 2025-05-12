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

- Opción: NAS  (Network Attached Storage)
- Marca/modelo: QNAP TS-473A
- Sistema operativo: Ubuntu

### b. Tipo de RAID

- Elegido: RAID 10
- Justificación: El RAID 10 ofrece mejoras en el rendimiento y también una tolerancia a fallos, lo malo que es mas caro que los demas raids.

### c. Software de gestión

- Software elegido: OpenMediaVault
- Función principal: tiene un almacenamiento centralizado con redundancia, servicios de red para compartir archivos en la red, gestión avanzada de permisos y usuarios, virtualización y contenedores como por ejemplo un Docker.

---

## 4. Configuración del Nivel 3: Servidor Secundario Remoto

### a. Tipo de servidor remoto

- Opción elegida: Nube
- Justificación: acceso desde cualquier ubicación, alta disponibilidad, mantenimiento gestionado por el proveedor sin preocuparse del hardware, capia de datos con una protección contra fallos regionales.

### b. Seguridad de la sincronización

- ¿Cómo se programa la sincronización?
  
  Utiliza Backup incremental automatizado, su frecuencia es diaria para datos críticos, y semanal o mensual para archivos menos sensibles.
- ¿Qué cifrado se usa?
  
  utiliza varios tipos de cifrado como el TLS 1.2/1.2 que protege datos durante la transferencia, y el cifrado en reposo como el AES-256 aplicado antes de subir a la nube.
- ¿Se puede activar doble autenticación?

  Si, en la mayoria de proveedores como por ejemplo:
  Wasabi: que utiliza la doble autentificación de Google
  Azure: que utiliza la autentificación en dos pasos

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
- Fuente 2: ______________________
- ...

