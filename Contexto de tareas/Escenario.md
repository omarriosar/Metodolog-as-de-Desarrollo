## Contexto
En la División de Ciencias, Ingeniería y Tecnología (DCIT) de la Universidad de Quintana Roo, Campus Chetumal Bahía, el Laboratorio Múltiple de Telemática opera como un espacio de formación práctica para los estudiantes de la carrera de Ingeniería en Redes. Actualmente, el control de las prácticas y el préstamo de los equipos se realiza de manera manual mediante formatos de digitales y bitácoras en Excel, lo que genera cuellos de botella al inicio de las sesiones, descontrol en el inventario y discrepancias al momento de verificar qué materiales fueron devueltos en buen estado.

En la reunión más reciente con el cliente se han obtenido los siguientes requisitos funcionales:
| Requisito funcional	| Descripción operativa |
|-----|-----|
| Reservación de Estaciones por equipos |	El estudiante agenda una estación disponible para su práctica, registrando de 1 a 4 integrantes dentro del periodo habilitado por el responsable. |
| Control de Asistencia y Tolerancia | El sistema valida la llegada del equipo en los primeros 15 minutos; de no presentarse, libera automáticamente la estación reservada. |
| Registro y Dictamen de Prácticas | El equipo registra el Check-in al inicio de la sesión y el responsable del laboratorio concluye con el Check-out, marcando el estatus como "Aprobada", "No Aprobada" o "Parcial" con las anotaciones correspondientes. |
| Inventario Agrupado por área de trabajo | El responsable registra activos institucionales y los asocia o desvincula físicamente de cada espacio de trabajo según se requiera. |
| Bitácora de fallas y mantenimiento | El responsable o los estudiantes pueden reportar incidencias en el equipamiento tras una práctica y el responsable tendrá acceso al historial de fallos y mantenimientos realizados al equipo. |
| Bloqueo de Calendario para Docentes | El docente registra horarios exclusivos de laboratorio para demostraciones de clase, inhabilitando las reservas de alumnos en ese bloque. |
| Personalización de calendario de disponibilidad de áreas | El responsable registrará los espacios disponibles para el trabajo por bloques de horas, permitiendo la libre solicitud de parte de los estudiantes. |

Adicionalmente, tras la última reunión con el equipo de trabajo, se han determinado los siguientes requisitos no funcionales:
| Categoría | Requisito No Funcional | Restricción o Criterio de Calidad |
| ----- | ----- | ----- |
| **Seguridad** | Cifrado y gestión de credenciales | Las contraseñas de los usuarios deben almacenarse cifradas en la base de datos mediante algoritmos robustos (ej. bcrypt) y la identificación del usuario autenticado debe gestionarse mediante tokens de acceso seguros. |
| **Seguridad** | Control de acceso y autorización granular | El sistema debe implementar control de acceso por roles (Administrador, Responsable, Docente y Alumno) impidiendo accesos o modificaciones no autorizadas; la validación de permisos debe resolverse en un tiempo $\le 1.0$ segundo. |
| **Rendimiento** | Tiempo de respuesta en autenticación | El proceso completo de validación de credenciales y generación del token de sesión debe completarse en un tiempo no mayor a 2.0 segundos. |
| **Rendimiento** | Tiempo de procesamiento transaccional en BD | El proceso de validación y persistencia transaccional de citas, Check-in/Check-out o inventario debe ejecutarse en un tiempo $\le 2.0$ segundos bajo condiciones normales de concurrencia. |
| **Fiabilidad** | Validación de esquemas y consistencia relacional | El motor del sistema debe garantizar que el 100% de las transacciones rechacen entradas nulas, duplicadas o con inconsistencias de formato antes de confirmar la escritura en la base de datos. |
| **Disponibilidad / Fiabilidad** | Respaldo periódico y automatizado de la base de datos | El servicio de persistencia debe ejecutar respaldos automáticos e íntegros del esquema y datos de la base de datos cada 24 horas sin requerir intervención manual ni interrumpir la operación del sistema. |
| **Disponibilidad** | Nivel de servicio y continuidad operativa (SLA) | El entorno de despliegue principal del sistema debe garantizar una disponibilidad de servicio del 99.0% mensual durante el periodo del ciclo académico. |
| **Usabilidad** | Adaptabilidad responsiva de la interfaz | La interfaz de usuario debe contar con diseño responsivo operable sin desbordamientos visuales en pantallas desde 360px hasta 1080px. |
| **Rendimiento** | Capacidad de concurrencia en apertura de citas y registro de asistencias | El sistema debe gestionar peticiones simultáneas de al menos 30 usuarios concurrentes sin degradación del servicio ni bloqueo de transacciones al habilitar el calendario de prácticas. |
| **Fiabilidad / Automatización** | Precisión temporal en liberación por tolerancia | El servicio temporizador del sistema debe validar y liberar automáticamente las estaciones reservadas con un desfase técnico no mayor a 60 segundos tras cumplirse los 15 minutos de tolerancia establecidos. |

