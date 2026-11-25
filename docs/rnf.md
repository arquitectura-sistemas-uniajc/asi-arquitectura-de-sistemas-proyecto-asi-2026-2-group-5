# Requerimientos no funcionales — SaludCita

| ID | Categoría | Requerimiento |
|---|---|---|
| RNF-01 | Rendimiento | El sistema soporta 25 usuarios concurrentes en la franja pico, con el 95 % de las respuestas en 0,5 s o menos. |
| RNF-02 | Disponibilidad | 99,5 % mensual en horario de atención (6 a. m. a 8 p. m.). La capa de aplicación no tiene punto único de falla. La base de datos tiene respaldo diario y recuperación en 4 h o menos. |
| RNF-03 | Consistencia | Cero citas duplicadas para el mismo médico y horario; lo garantiza la base de datos con una restricción única. |
| RNF-04 | Seguridad y privacidad | TLS en tránsito, cifrado en reposo, acceso por rol y relación médico-paciente, conforme a la Ley 1581 de 2012. |
| RNF-05 | Auditoría | Registro inmutable de cada lectura y escritura de datos de pacientes, con retención de 12 meses. |
| RNF-06 | Costo | La infraestructura no supera 100 USD al mes en operación. |
| RNF-07 | Mensajería | Los recordatorios son asíncronos y reintentables; su falla no bloquea reservar ni cancelar. |
