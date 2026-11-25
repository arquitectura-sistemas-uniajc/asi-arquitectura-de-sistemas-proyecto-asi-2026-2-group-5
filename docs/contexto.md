## Análisis y Requisitos: Sistema de Gestion de Citas Medicas


# ¿Qué duele hoy?
- El agendamiento se hace por teléfono, eso produce citas duplicadas: dos pacientes con el mismo médico en el mismo horario. A partir de ahí vienen la reprogramación manual, las llamadas para avisar del cruce, los cupos desperdiciados y la falta de un historial confiable. Además, nadie tiene visibilidad en tiempo real de qué horarios están libres.

# ¿Quién sufre ese dolor?
- Pacientes: llegan y descubren que su cita choca con la de otro, pierden tiempo y desplazamiento, y no pueden consultar ni cancelar fuera del horario de atención telefónica.
- Médicos: su agenda se desordena, tienen tiempos muertos o sobrecupo, y atienden con retrasos en cadena.
- Personal administrativo: el más afectado en carga operativa. Atiende las llamadas, lleva la agenda a mano, resuelve conflictos y da la cara ante pacientes molestos.
- La red de consultorios: pierde ingresos por cupos mal usados e inasistencias sin recordatorio, y daña su reputación.

# ¿Qué pasa si el sistema se cae una hora?

- Si el sistema cae, no se pueden tomar citas, y si el personal vuelve al teléfono o a una hoja de cálculo, reaparece el problema original. Y peor aún, al restablecerse hay que reconciliar las citas hechas por fuera con las del sistema, con riesgo de duplicados. Por eso.

- Si el servicio de mensajería falla, las citas no se pierden, pero hay que reenviar los recordatorios pendientes al recuperarse, para no aumentar las inasistencias.

# ¿Bloqueo optimista o pesimista? ¿Qué pasa con el que pierde la carrera?
- Optimista, respaldado por una restricción de unicidad en la base de datos. La razón es el patrón de uso: hay muchísimas consultas de disponibilidad y muy pocos intentos reales de reservar el mismo cupo al mismo tiempo. El flujo es: intentar insertar la cita, si la base de datos acepta, el cupo es tuyo, si no, viola la restricción por lo tanto no se podria agendar.
- El que pierde la carrera recibe un mensaje claro e inmediato ("Ese horario acaba de ser reservado") junto con alguna alternativa como pueder ser el mismo médico en otros horarios del día u otros médicos disponibles a esa hora.

# ¿Qué se cachea y qué jamás se cachea?

Se cachea:
- Catálogo de médicos, especialidades y consultorios (cambia poco).
- Plantillas de horarios de atención de cada médico.
- La vista de disponibilidad para navegación.
- Contenido estático y configuración.

No se cachea:
- La verificación de disponibilidad dentro de la transacción de reserva. Esto siempre se va a decidir contra la base de datos.
- El resultado de reservar o cancelar.
- Datos clínicos o personales del paciente y menos aún su historial de citas.
- Permisos y roles: cachearlos mucho tiempo significa que alguien con acceso revocado sigue viendo datos.

# Los datos de salud son sensibles. ¿Quién puede ver qué, y cómo se audita quién consultó qué?

Quien puede ver qué: 
- Paciente: solo sus propias citas e historial.
- Médico: las citas de su propia agenda y los datos del paciente necesarios para atenderlo.
- Personal administrativo: ve y gestiona agendas, pero solo con datos mínimos del paciente (nombre, contacto, documento para identificarlo), sin motivo de consulta ni información clínica. Si necesita ver más, se hace por una acción explícita y registrada.
- Administrador del sistema: gestiona configuración y usuarios, pero no tiene acceso por defecto a datos de pacientes.

Como se audita:
- Se registra todo en un log con los datos del usuario, la hora de la ejecución, acción que ejecuto, hora en que lo hizo y respuesta.
