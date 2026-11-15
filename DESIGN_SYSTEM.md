# 🎨 Guía de Diseño, Estilo y Organización en Figma

## 🎨 1. Sistema de Diseño (Colores, Formas y Tipografía)

### Paleta de Colores
- **Azul Tajamar (Primario)**: `#003366` (Header, botones principales, énfasis institucional).
- **Azul Celeste (Secundario/Hover)**: `#0D5CAD` / `#2563EB` (Estados hover, enlaces, accesos activos).
- **Verde Eco/Disponibilidad (Éxito)**: `#10B981` (Plazas disponibles, estado confirmado, badges de movilidad limpia).
- **Naranja Eventos/Cola (Alerta)**: `#F59E0B` (Eventos puntuales, lista de espera, plazas agotándose).
- **Gris de Fondo**: `#F8FAFC` (Fondo de aplicación limpio y descanso visual).
- **Gris Neutro / Texto**: `#1E293B` (Texto principal) y `#64748B` (Subtítulos e información secundaria).

### Tipografía y Formas
- **Fuente recomendada**: `Inter` o `Montserrat` (Limpias, legibles en pantallas móviles).
- **Bordes y Sombras**:
  - `rounded-xl` (12px - 16px) en tarjetas e inputs para un aspecto moderno y amigable.
  - `shadow-sm` para tarjetas en reposo y `shadow-lg` al pasar el cursor (`hover`).

---

## 🖌️ 2. Organización del Diseño en Figma y Repositorio Git

### Estrategia de Figma
Crearemos un único archivo en Figma llamado **`Tajamar-Mobility-UI`** estructurado en las siguientes páginas:

1. **`01. Design System & Components`**:
   - Botones (Normal, Hover, Disabled, Primary, Secondary, Alert).
   - Inputs y Selectores (Origen, Destino, Horarios, Selector de días).
   - Badges (Verde = Plazas Libres, Naranja = Lista de Espera, Azul = Recurrente).
   - Tarjetas (`TripCard`, `EventCard`, `VehicleCard`).
2. **`02. Wireframes Low-Fi`**:
   - Esqueletos en blanco y negro para validar la disposición de los botones y textos antes de colorear.
3. **`03. SPRINT 2 - UI High-Fi`**:
   - Pantalla de Perfil de Conductor y Vehículos.
   - Pantalla de Publicar Viaje.
   - Pantalla de Búsqueda y Filtros de Viajes.
4. **`04. SPRINT 3 - UI High-Fi`**:
   - Pantalla de Eventos Tajamar.
   - Detalle del Evento y Trayectos Asociados.
   - Pantalla de Mis Reservas y Estado de Lista de Espera.

### Cómo guardar la parte de Diseño en el Repo Git
Para entregar la documentación de diseño junto al código:
- Crear una carpeta `/design` en la raíz del repositorio.
- Fichero `/design/FIGMA.md` con:
  - Enlace público/de lectura a Figma.
  - Capturas de pantalla (`.png` / `.svg`) de los bocetos de las pantallas principales para poder visualizarlas directamente en GitHub sin abrir Figma.

---

## 👥 3. Reparto de Tareas en el Equipo de 4 Integrantes (Sprints 2 y 3)

### 👤 Alumno 1: Lead UI/UX & Componentes Base Angular
- Diseñar el **Design System** en Figma (Colores, Botones, Tarjetas).
- Crear la biblioteca de componentes reutilizables en Angular (`Navbar`, `Footer`, `TripCardComponent`, `BadgeComponent`, `ModalComponent`).
- Aplicar Tailwind CSS / SCSS en Angular.

### 👤 Alumno 2: Angular Frontend Developer (Vistas y Formas)
- Maquetar las pantallas en Figma (Wireframes + UI).
- Implementar en Angular: `TripListComponent`, `TripCreateComponent`, `ProfileComponent` y `VehicleManagerComponent`.
- Manejar formularios reactivos (`ReactiveFormsModule`) e integración de eventos de botones.

### 👤 Alumno 3: Lead Backend (.NET / Node.js) & DB
- Modelar en SQL Server las tablas correspondientes a Vehículos, Trayectos y Eventos (siguiendo las directrices de Paco).
- Crear Endpoints API REST para: CRUD de Vehículos, Publicar Trayecto (Recurrente/Temporal) y Filtros de Búsqueda.

### 👤 Alumno 4: Backend Developer (Lógica de Reservas & Eventos)
- Crear Endpoints API REST para: CRUD de Eventos Tajamar, Asociación Evento-Trayecto y Reservas de Pasajeros.
- Diseñar la estructura de base de datos y endpoints preparados para la **Lista de Espera (FIFO)**.
