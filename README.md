# Heaven

Web app privada para que una dentista que trabaja en varias clínicas y hospitales registre en segundos los procedimientos realizados y controle cuánto debe cobrar según la configuración de cada centro. Reemplaza el uso manual de Excel/Word, priorizando velocidad, simplicidad y trazabilidad histórica.

No es un software clínico: no almacena fichas médicas ni datos de pacientes. Solo registra prestaciones y tarifas para efectos de cobro.

## Ver el prototipo

Este repo contiene un **prototipo visual interactivo** (`index.html`), un solo archivo sin dependencias ni backend. Se puede abrir directamente en el navegador o publicarlo con GitHub Pages:

**Settings → Pages → Deploy from branch → `main` → `/ (root)`**

Queda disponible en `https://TU_USUARIO.github.io/heaven-prototipo/`

Los datos que se ven (centros, procedimientos, tarifas, registros) son de ejemplo y viven en memoria del navegador — al recargar la página vuelven a su estado inicial.

## Qué incluye el prototipo

**Vista operativa (mobile, marco de teléfono)**
- Login
- Registro rápido: centro → adulto/niño → uno o varios procedimientos → guardar, con ticket de confirmación
- Historial de registros propios

**Panel administrativo (desktop)**
- Resumen: totales y facturación por centro
- Centros: alta y activación/desactivación
- Procedimientos: catálogo, con o sin diferencia adulto/niño
- Tarifas: valor por centro y procedimiento, editable
- Registros: listado completo con edición y borrado auditado
- Auditoría: historial cronológico de cambios (creado / editado / eliminado)

## Alcance del MVP

**Incluye:** login privado, registro por procedimientos, centros, tarifas por centro/procedimiento, diferenciación adulto/niño, múltiples procedimientos por atención, historial de tarifas (versionado + snapshot por registro), edición y borrado con trazabilidad, panel admin básico.

**Excluye por ahora:** agenda/calendario, pago por horas, bonos, descuentos, retenciones, estadísticas avanzadas, multiusuario complejo, integraciones externas.

## Modelo de datos

| Entidad | Descripción |
|---|---|
| `users` | Usuario operativo y admin |
| `centers` | Clínicas y hospitales |
| `procedures` | Catálogo de procedimientos |
| `center_procedures` | Procedimientos habilitados por centro |
| `procedure_rates` | Tarifas vigentes por centro y procedimiento |
| `registrations` | Cabecera de cada atención |
| `registration_items` | Procedimientos dentro de una atención, con snapshot del valor aplicado |
| `audit_log` | Historial de cambios |

El snapshot en cada `registration_item` es clave: permite modificar tarifas hacia adelante sin alterar el valor histórico de atenciones ya registradas.

## Reglas de negocio

- El sistema trabaja por procedimientos (no por horas, por ahora).
- Cada centro tiene sus propios valores por procedimiento.
- La diferenciación adulto/niño aplica solo cuando el procedimiento lo requiere.
- Un mismo paciente puede tener varios procedimientos en un mismo registro.
- La fecha es obligatoria; la hora no es relevante.
- Toda edición o borrado queda registrado — nunca se pierde información histórica.

## Stack propuesto (siguiente etapa)

- Frontend: responsive, mobile-first
- Backend: PHP / Laravel
- Base de datos: PostgreSQL o MySQL
- Autenticación por roles (operativo / admin)

## Estado actual

Este repositorio contiene únicamente el **prototipo clickeable**, pensado para validar pantallas y flujo antes de construir la aplicación real con backend y base de datos.
