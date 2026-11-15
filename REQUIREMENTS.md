# 📄 Documento de Requisitos y Análisis del Sistema

## 1. 👥 Gestión de Usuarios, Perfiles y Roles

### RF-01: Registro e Inicio de Sesión
- **RF-01.1**: Los usuarios deben registrarse usando su correo institucional o personal y contraseña encriptada.
- **RF-01.2**: Autenticación basada en JWT (JSON Web Tokens).

### RF-02: Perfil Único / Rol Dual (Conductor y Pasajero)
Un usuario no tiene un rol fijo exclusivo; puede actuar como **Conductor** o **Pasajero** según el trayecto:
- **Perfil General**: Nombre, apellidos, teléfono, foto, curso asignado.
- **Modo Conductor**:
  - Registro de vehículos (Marca, Modelo, Color, Matrícula, Número de plazas totales).
  - Publicación y gestión de trayectos.
  - Aceptación o rechazo de solicitudes de reserva.
- **Modo Pasajero**:
  - Búsqueda y filtrado de trayectos.
  - Reserva de plazas y cancelación.
  - Inscripción en lista de espera si la capacidad está llena.

---

## 🎓 2. Gestión Académica (Cursos y Eventos)

### RF-03: Vinculación Académica
- **RF-03.1**: Cada usuario debe estar asociado a uno o varios cursos académicos de Tajamar (ej: 1º DAM, 2º DAW, ASIR, Bachillerato, etc.).
- **RF-03.2**: Posibilidad de filtrar conductores/pasajeros que pertenezcan al mismo curso o departamento para mayor confianza.

### RF-04: Gestión de Eventos de Tajamar
- **RF-04.1**: Los administradores o profesores pueden crear **Eventos Oficiales** (ej: *Hackathon Tajamar*, *Feria de Empleo*, *Torneo Deportivo*, *Jornada de Puertas Abiertas*).
- **RF-04.2**: Los conductores pueden asociar un trayecto puntual a un evento específico.

---

## 🚗 3. Gestión de Trayectos y Reservas

### RF-05: Tipos de Trayectos
1. **Trayectos Recurrentes (Diarios)**:
   - Configuración de días de la semana (Lunes a Viernes).
   - Horarios de ida (ej: 07:30 AM hacia Tajamar) y/o vuelta (ej: 14:30 PM desde Tajamar).
   - Modalidad: *Solo Ida*, *Solo Vuelta*, *Ida y Vuelta*.
2. **Trayectos Puntuales / Temporales (Eventos)**:
   - Asociados a un evento de Tajamar con fecha y hora específicas.
   - Puntos de recogida intermedios o punto de encuentro.

### RF-06: Búsqueda y Filtrado
- Búsqueda por: Origen, Destino (por defecto Tajamar), Fecha/Hora, Plazas disponibles, Curso o Evento asociado.

### RF-07: Reservas de Plaza
- Solicitud de reserva por parte del pasajero.
- Confirmación automática o manual según preferencia del conductor.
- Restricción: Un pasajero no puede reservar más de 1 plaza en el mismo trayecto a la misma hora.

---

## ⏳ 4. Sistema de Cola de Espera (Eventos y Trayectos Temporales)

### RF-08: Funcionamiento de la Lista de Espera
Cuando un trayecto puntual/temporal asociado a un evento alcanza **0 plazas disponibles**:
1. **Suscripción a la Cola**:
   - El botón de "Reservar" cambia a "Unirse a la Cola de Espera".
   - El sistema registra al usuario con marca de tiempo (timestamp) manteniendo orden **FIFO** (First-In, First-Out).
2. **Gestión de Cancelaciones**:
   - Si un pasajero con reserva confirmada cancela su plaza:
     - **Opción A (Asignación Automática)**: La plaza libre se asigna automáticamente al primer usuario en la cola de espera y se le notifica.
     - **Opción B (Ventana de Tiempo)**: Se envía una notificación al primer usuario de la cola dándole X horas/minutos para confirmar la reserva antes de pasar al siguiente.
3. **Cancelación de Cola**:
   - Un usuario en lista de espera puede abandonar la cola en cualquier momento sin penalización.

---

## ⚙️ 5. Requisitos No Funcionales (RNF)

- **RNF-01 (Seguridad)**: Las contraseñas deben estar cifradas mediante algoritmos seguros (BCrypt / Argon2).
- **RNF-02 (Rendimiento)**: Respuestas de la API en menos de 300ms para consultas de búsqueda.
- **RNF-03 (Compatibilidad DB)**: Compatibilidad total con Microsoft SQL Server mediante ORM o Stored Procedures.
- **RNF-04 (Diseño Responsive)**: Interfaz adaptada a dispositivos móviles (Mobile First) y escritorio.
