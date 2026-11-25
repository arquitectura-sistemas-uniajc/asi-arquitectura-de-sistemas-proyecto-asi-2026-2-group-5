SaludCita Agendamiento de citas médicas

El problema. Una red de consultorios necesita agendar citas evitando que dos
pacientes reserven el mismo horario con el mismo médico. Hoy lo hacen por
teléfono y hay duplicados constantes.

Usuarios. Pacientes, médicos, personal administrativo.
Funcionalidad mínima. Consultar disponibilidad. Reservar una cita. Cancelar. Ver historial de citas. Enviar recordatorio.
Sistemas externos probables. Servicio de mensajería o correo para recordatorios.

El reto arquitectónico. La condición de carrera en la reserva: dos pacientes
pidiendo el mismo cupo en el mismo instante. Es el mejor caso del semestre para
entender consistencia y por qué la caché es peligrosa en escrituras.

Preguntas que deberán responder.
¿Bloqueo optimista o pesimista? ¿Qué pasa con el que pierde la carrera?
¿Qué se cachea y qué jamás se cachea en este sistema?
Los datos de salud son sensibles. ¿Quién puede ver qué, y cómo se audita quién consultó qué?