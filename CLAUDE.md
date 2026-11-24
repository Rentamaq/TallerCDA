# Panel Taller Rentamaq CDA

Panel web (GitHub Pages) con el estado de los equipos informados en el grupo de WhatsApp «Taller Rentamaq CDA».
Publicado en https://rentamaq.github.io/TallerCDA/ desde la rama `main` (raíz). Responsable: René Luna (rluna@rentamaq.cl). Responder en español.

## Archivos
- `index.html` – todo el panel (HTML + CSS + JS, sin dependencias externas).
- `data.js` – `window.TALLER_DATA = { actualizado, ultima_lectura, periodo, registros: [...] }`. `ultima_lectura` marca hasta dónde se leyó el grupo (lo usa el skill `tallercda`). Es lo único que cambia en cada lectura del grupo.
- `logo-rentamaq.png` – logo corporativo (encabezado y favicon).
- `OBSERVACIONES.md` – observaciones de René y mejoras pendientes del sistema. Leerlo antes de proponer cambios. OBS-01: los reportes por WhatsApp no traen la información necesaria y mantención no confirma los cierres.

## Botones del encabezado
- «⟳ Actualizar»: solo recarga la página (data.js se carga sin caché). No ejecuta el skill; la lectura de WhatsApp se hace con /tallercda.
- «Exportar CSV». (René pidió quitar «Recargar» y «Descargar data.js»; se recarga con F5.)

## Pestañas
En las tablas de las pestañas 1 y 2 los encabezados ordenan al hacer clic (▲ ascendente / ▼ descendente).
1. **Fuera de servicio y revisiones**: arriba los mismos KPIs del Dashboard; registros con `estado: "ABIERTO"`. Columnas: Estado (desplegable editable solo entre Fuera de servicio y Solicita revisión; muestra «Cambiado …» si se modificó), Reportado por, Código interno, Hora de reporte, Horas F/S (en vivo), Falla/motivo, botón «Declarar operativo» (confirmación en la misma fila). Formulario de ingreso abajo.
2. **Operativos**: registros con `estado: "OP"`. Columnas: Código interno, Hora de reporte, Declarado operativo, Tiempo desde operativo, Tiempo detenido, Declarado por, Detalle (+ «Reabrir» si se cerró en el navegador). Formulario de ingreso abajo.
3. **Dashboard**: KPIs, torta 3D grande de «Averías por sistema» (clasificación por palabras clave en `SISTEMAS`) y 5 tortas 3D con tabla de leyenda, total y conclusión.

Decisiones ya tomadas por René: sin columnas Patente ni N° Teck; tortas en 3D; colores corporativos (gris #2b2b2b / #636363, naranjo #e88305); estados en rojo/amarillo/verde; sin el gráfico «Quién declara los equipos operativos».

Los ingresos manuales, cierres y reaperturas se guardan en `localStorage` (`tallercda_local_v1`) del navegador; no hay botón para exportarlos (René lo pidió quitar), así que los cambios que deben ver todos se cargan en data.js vía WhatsApp/skill.

## Formato de un registro (data.js)
```js
{ id:"W001", tipo:"FS"|"REV", equipo:"EX-11", patente:"", teck:"", clase:"Excavadora",
  reportado_por:"Tel. ••1941" | "Nombre", fecha_reporte:"2026-11-13T07:55:00-03:00",
  condicion:"falla o motivo", estado:"ABIERTO"|"OP", fecha_op:"", declarado_por:"",
  nota:"", fuente:"WhatsApp"|"Manual",
  // campos del formato estándar de solicitud (desde 24/11/2026; opcionales en registros antiguos)
  descripcion:"Excavadora Komatsu PC200", ubicacion:"", horometro:"", operador:"", supervisor:"" }
```
Clases válidas: Excavadora, Mini excavadora, Retroexcavadora, Cargador frontal, Camión aljibe, Camión pluma, Camión, Rodillo, Otro.
Fechas ISO con -03:00 (hora de Chile). Ids nuevos: siguiente correlativo `W0NN`.

## Actualizar desde WhatsApp (cuando René lo pida)
1. Abrir WhatsApp Web en el Chrome de René (el navegador integrado no es compatible), grupo «Taller Rentamaq CDA». Solo lectura: nunca enviar ni responder mensajes.
2. Leer los mensajes desde la última `actualizado` de data.js, con la hora de `data-pre-plain-text` de cada mensaje, recorriendo el chat de arriba hacia abajo.
3. Clasificar:
   - **FS**: equipo detenido, «fuera de servicio», no arranca, fuga que impide moverlo, baja/ingresa a taller, mantención programada en taller.
   - **REV**: el equipo opera pero piden revisión (luces, códigos, pértiga, vidrios, pasadores, niveles de aceite…). **También son REV (indicado por René)**: falta de fluidos sin detención («falta refrigerante», «falta aceite») y alertas o alarmas en tablero informadas por el conductor («alerta de batería baja», «arroja código…»). Ejemplos: «Rodillo doble tambor falta refrigerante»; «CAA-04 conductor indica que en tablero arroja alerta de batería baja de contacto, se encuentra en PTOI». La ubicación informada («muro oriente central», «PTOI») va en `nota`.
   - Si el reporte no trae código interno pero identifica el equipo (p. ej. «Rodillo doble tambor»), registrarlo igual usando esa descripción como `equipo` y anotar «Sin código interno en el reporte».
   - **Formato estándar de solicitud (desde 24/11/2026, ver OBSERVACIONES.md)**: los mensajes traen las líneas «Identificación del equipo / Código del equipo / Ubicación / Horómetro / Operador / Observación / Supervisor a cargo». Mapear: Identificación → `descripcion` (y deducir `clase`), Código → `equipo`, Ubicación → `ubicacion`, Horómetro → `horometro` (solo el número), Operador → `operador`, Observación → `condicion`, Supervisor a cargo → `supervisor`. Aceptar variaciones de mayúsculas, tildes, «:» o «-». Si faltan campos, registrar igual con lo que venga; el panel marca como «Reporte sin formato estándar» lo recibido desde el 24/11 13:00 sin ubicación, horómetro, operador ni supervisor. En reportes sin formato, si el texto libre trae ubicación, ponerla en `ubicacion` (no en `nota`).
   - **Operativo**: «operativo», «quedó operativa», «se despacha operativo», «se realizó lo solicitado», «funcionando bien», «listo» → cerrar el registro abierto de ese equipo (`estado:"OP"`, `fecha_op`, `declarado_por`, nota con el trabajo).
   - No registrar: engrase, relleno de AdBlue, porta número u otros servicios menores; mencionarlos en el resumen.
   - Sin duplicados: reenvíos y recordatorios del mismo problema no son registros nuevos (agregar «reiterado» en la condición). Si un equipo operativo vuelve a fallar, crear un registro nuevo.
4. Quien reporta: nombre si el remitente está guardado o tiene nombre visible (Christian, Pedro Orrego, Operaciones Rentamaq, Manuel Navarro, Francisco Alvarado, Javier Moroso [••6082], Andrea Ximena [••3794]…). El nombre visible aparece en la cabecera del mensaje con «~»; si no, `Tel. ••` + 4 últimos dígitos. El repo es público: nunca publicar teléfonos completos.
5. Actualizar `actualizado` y `periodo`, validar con `node -e "global.window={};eval(require('fs').readFileSync('data.js','utf8'));console.log(window.TALLER_DATA.registros.length)"`, commit con autor «René Luna <rluna@rentamaq.cl>» y push a `main`. Pages publica en ~1 minuto.
6. Resumen breve a René: nuevos F/S, nuevas revisiones, nuevos operativos, totales vigentes y lo que no se registró.
