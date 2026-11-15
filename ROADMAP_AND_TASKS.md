# 📅 Planificación de Tareas y Roadmap por Sprints

Organización propuesta del desarrollo en 4 Sprints / Fases de trabajo:

---

## 🚀 Fase 1: Configuración Inicial, Autenticación y Modelado (Sprint 1)

### 🗄️ Base de Datos & Configuración
- [ ] Analizar el script/diagrama de SQL Server proporcionado por Paco.
- [ ] Configurar el proyecto Backend y la cadena de conexión a SQL Server.
- [ ] Configurar el repositorio Git con ramas `main` y `develop`.

### 🔑 Backend
- [ ] Crear estructura base de capas (Controllers, Services, Repositories).
- [ ] Implementar registro y login de usuarios con hash de contraseña.
- [ ] Configurar Middleware de JWT para proteger endpoints.

### 💻 Frontend
- [ ] Inicializar proyecto React + Vite + Tailwind CSS.
- [ ] Diseñar layout base (Navbar, Footer, Sidebar de navegación).
- [ ] Crear páginas de Registro, Login y gestión de Tokens en `LocalStorage`/`Cookies`.

---

## 🚗 Fase 2: Gestor de Trayectos y Perfiles de Usuario (Sprint 2)

### 🔑 Backend
- [ ] CRUD de Vehículos asociados al usuario conductor.
- [ ] CRUD de Trayectos Recurrentes (Lunes a Viernes, Ida/Vuelta) y Puntuales.
- [ ] Endpoints de búsqueda con filtros (Origen, Destino Tajamar, Fecha).

### 💻 Frontend
- [ ] Perfil de Usuario (Vista Conductor / Vista Pasajero).
- [ ] Formulario de creación de trayectos (modo recurrente y puntual).
- [ ] Pantalla de catálogo/búsqueda de trayectos disponibles con tarjetas informativas (*TripCards*).

---

## 🎓 Fase 3: Gestión Académica, Eventos y Reservas (Sprint 3)

### 🔑 Backend
- [ ] CRUD de Eventos Tajamar (Creación por admin/profesor).
- [ ] Endpoint para asociar trayectos temporales a eventos académicos.
- [ ] Lógica de Reserva de Plazas con control de aforo (decrementar plazas disponibles).

### 💻 Frontend
- [ ] Vista de Eventos Tajamar (*Hackathons*, *Jornadas*, etc.).
- [ ] Integración de botón "Reservar Plaza" con feedback visual.
- [ ] Vista de mis reservas activas (como pasajero) y mis viajes ofertados (como conductor).

---

## ⏳ Fase 4: Lista de Espera, Notificaciones y Pulido Final (Sprint 4)

### 🔑 Backend
- [ ] Implementación de la **Cola de Espera (FIFO)** en trayectos temporales llenos.
- [ ] Lógica de reasignación de plazas al cancelar una reserva (notificación / asignación al 1º de la lista).
- [ ] Validación general de errores y logs.

### 💻 Frontend
- [ ] Interfaz para unirse/cancelar inscripción en la Lista de Espera.
- [ ] Notificaciones en pantalla (Toasts/Alertas) para cambios de estado en reservas.
- [ ] Pulido visual, responsive design en dispositivos móviles y documentación final.

---

## 📋 Matriz de Reparto de Tareas Recomendado

| Alumno / Integrante | Enfoque Principal | Responsabilidades |
| :--- | :--- | :--- |
| **Integrante 1** | Lead Backend / DB | SQL Server, EF Core / ORM, Lógica de Lista de Espera FIFO |
| **Integrante 2** | Backend & API | Autenticación JWT, Endpoints de Trayectos y Reservas |
| **Integrante 3** | Lead Frontend / UI | Diseño Tailwind, Navbar, Vistas de Trayectos y Eventos |
| **Integrante 4** | Frontend & UX | Formularios, Integración API (Axios/Fetch), Lista de Espera UI |
