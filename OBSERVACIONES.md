# Observaciones y mejoras pendientes – Panel Taller Rentamaq CDA

## OBS-01 · Calidad del reporte y retroalimentación de cierre (24/11/2026)

**Registrada por:** René Luna, Jefe de Operaciones.
**Estado:** en curso. Formatos de solicitud y de cierre definidos por René el 24/11/2026 (ver abajo). Falta difundirlos y medir su cumplimiento.

### Observación
El panel funciona bien en general, pero tiene un problema de origen en la información:

1. **Los reportes que llegan por WhatsApp no traen los datos necesarios.** Los usuarios escriben con formato libre. Muchas veces falta el código interno del equipo, no queda claro si el equipo está detenido o sigue operando, o la ubicación y la falla llegan en mensajes separados o como respuesta a otro mensaje. Por eso la clasificación (fuera de servicio o revisión) y la identificación del equipo dependen de interpretar el texto.
2. **Mantención no confirma que el equipo fue atendido y quedó operativo.** Muchos registros quedan abiertos sin aviso de cierre, o se cierran por deducción, por ejemplo cuando el equipo vuelve a aparecer trabajando o con una mantención programada posterior. Así, el panel no refleja con certeza qué está realmente operativo.

### Evidencia (lectura del 16/11 al 23/11)
- Reportes sin código interno: «Rodillo doble tambor», «camión petrolero arrendado».
- Registros que quedaron abiertos sin aviso de cierre de mantención: EX-14 (luces, reiterado 3 veces), EX-30 (tapa de combustible y golpe), EX-31 (flexible del picarrocas), CMT-115, REX-23, CFA-12, entre otros.
- Cierres deducidos y no confirmados: EX-31 (mantención del 15/11, cerrada porque el equipo volvió a operar).
- Operativos informados sin ingreso previo en el grupo: GG-15, REX-18, CMT-132, CA-27, BS-14, EXA-35, CAA-08.

### Formato estándar de solicitud de atención (definido 24/11/2026)
Desde el 24/11/2026, todo pedido de atención en el grupo debe enviarse así:

```
Identificación del equipo: Excavadora Komatsu PC200
Código del equipo: EX-06
Ubicación:
Horómetro:
Operador:
Observación: (detalle del problema presentado)
Supervisor a cargo:
```

- El panel guarda y muestra cada campo (identificación, ubicación, horómetro, operador, supervisor) junto a la falla.
- Los reportes recibidos desde el 24/11 13:00 que no traigan estos datos se marcan en el panel como «Reporte sin formato estándar», para hacer seguimiento al cumplimiento.
- El formulario de ingreso manual del panel pide los mismos campos.

### Formato estándar de cierre de mantención (definido 24/11/2026)
Cuando un equipo queda reparado, mantención debe responder en el mismo grupo de WhatsApp, idealmente citando la solicitud original, así:

```
Equipo: Excavadora PC200
Código: EX-06
Estado: Operativa
```

- Con este mensaje el panel cierra el registro abierto de ese código y lo pasa a «Operativos».
- Estados posibles: Operativo/Operativa (cierra el registro). Si se informa «Operativo con observación», también cierra, y la observación queda en el detalle. «Fuera de servicio» o «En taller» no cierra: mantiene o crea el registro F/S.
- Si se agrega una línea «Trabajo realizado:», se guarda en el detalle del operativo (opcional, recomendado).
- Los cierres desde el 24/11 13:00 que no usen este formato igual se registran, pero en la pestaña «Operativos» se marcan como «Cierre sin formato estándar».

### Ideas de mejora (por evaluar)
- ~~Formato estándar de reporte~~ → definido (ver arriba). Pendiente evaluar si se agrega un campo «Estado: DETENIDO / OPERA CON FALLA» para distinguir F/S de revisión sin interpretar.
- ~~Formato estándar de cierre para mantención~~ → definido (ver arriba).
- **Formulario web o QR por equipo** que alimente el panel directamente, en lugar del texto libre de WhatsApp.
- **Alerta de registros sin cierre**: marcar en el panel los equipos con más de X horas sin respuesta de mantención y recordarlos en el grupo o por correo.
- **Responsable de cierre**: definir quién de mantención confirma cada operativo (hoy lo hace mayoritariamente Juan Olivares).
- **Confirmación del solicitante**: que quien reportó valide que el equipo quedó bien.

### Próximo paso
1. Difundir en el grupo «Taller Rentamaq CDA» el formato de solicitud (usuarios) y el de cierre (mantención).
2. Revisar en cada lectura cuántas solicitudes y cierres cumplen el formato, y reforzar con quienes no lo usen.
