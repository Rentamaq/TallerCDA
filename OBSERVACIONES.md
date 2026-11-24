# Observaciones y mejoras pendientes – Panel Taller Rentamaq CDA

## OBS-01 · Calidad del reporte y retroalimentación de cierre (24/11/2026)

**Registrada por:** René Luna, Jefe de Operaciones.
**Estado:** abierta, pendiente de definir la solución.

### Observación
El panel funciona bien en general, pero tiene un problema de origen en la información:

1. **Los reportes que llegan por WhatsApp no traen los datos necesarios.** Los usuarios escriben con formato libre. Muchas veces falta el código interno del equipo, no queda claro si el equipo está detenido o sigue operando, o la ubicación y la falla llegan en mensajes separados o como respuesta a otro mensaje. Por eso la clasificación (fuera de servicio o revisión) y la identificación del equipo dependen de interpretar el texto.
2. **Mantención no confirma que el equipo fue atendido y quedó operativo.** Muchos registros quedan abiertos sin aviso de cierre, o se cierran por deducción, por ejemplo cuando el equipo vuelve a aparecer trabajando o con una mantención programada posterior. Así, el panel no refleja con certeza qué está realmente operativo.

### Evidencia (lectura del 16/11 al 23/11)
- Reportes sin código interno: «Rodillo doble tambor», «camión petrolero arrendado».
- Registros que quedaron abiertos sin aviso de cierre de mantención: EX-14 (luces, reiterado 3 veces), EX-30 (tapa de combustible y golpe), EX-31 (flexible del picarrocas), CMT-115, REX-23, CFA-12, entre otros.
- Cierres deducidos y no confirmados: EX-31 (mantención del 15/11, cerrada porque el equipo volvió a operar).
- Operativos informados sin ingreso previo en el grupo: GG-15, REX-18, CMT-132, CA-27, BS-14, EXA-35, CAA-08.

### Ideas de mejora (por evaluar)
- **Formato estándar de reporte** (plantilla fija o formulario):
  Equipo (código interno) · Estado (DETENIDO / OPERA CON FALLA) · Falla · Ubicación · Quién reporta.
  Ejemplo: `F/S EX-14 · Sin luces · Muro oriente central · Javier Moroso`.
- **Formato estándar de cierre para mantención**, obligatorio al terminar cada atención:
  `OPERATIVO EX-14 · Trabajo realizado · Hora`.
- **Formulario web o QR por equipo** que alimente el panel directamente, en lugar del texto libre de WhatsApp.
- **Alerta de registros sin cierre**: marcar en el panel los equipos con más de X horas sin respuesta de mantención y recordarlos en el grupo o por correo.
- **Responsable de cierre**: definir quién de mantención confirma cada operativo (hoy lo hace mayoritariamente Juan Olivares).
- **Confirmación del solicitante**: que quien reportó valide que el equipo quedó bien.

### Próximo paso
Definir con mantención y operaciones el formato de reporte y de cierre, y luego adaptar el panel y el skill `tallercda` a ese formato.
