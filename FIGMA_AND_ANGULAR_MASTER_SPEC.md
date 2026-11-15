# 📐 ESPECIFICACIÓN MAESTRA: FIGMA UI/UX Y COMPONENTES ANGULAR

Este documento es la guía definitiva para el **diseño de pantallas en Figma** y la **implementación de componentes en Angular** para el proyecto **Tajamar Mobility**.

---

## 🗺️ 1. Mapa de Navegación y Flujo de Pantallas (Figma User Flow)

```text
                               ┌─────────────────────────┐
                               │  1. LANDING / INICIO    │
                               │        (/home)          │
                               └───────────┬─────────────┘
                                           │
                        ┌──────────────────┴──────────────────┐
                        ▼                                     ▼
             ┌─────────────────────┐               ┌─────────────────────┐
             │  2. LOGIN / REGISTRO│               │ 3. BÚSQUEDA TRAYECTOS│
             │   (/login, /register)               │      (/trips)       │
             └──────────┬──────────┘               └──────────┬──────────┘
                        │ (Autenticado)                       │
                        └──────────────────┬──────────────────┘
                                           │
         ┌─────────────────────────────────┼─────────────────────────────────┐
         ▼                                 ▼                                 ▼
┌──────────────────┐             ┌──────────────────┐             ┌──────────────────┐
│ 4. PUBLICAR VIAJE│             │ 5. EVENTOS TAJAMAR│             │  6. MI PERFIL Y  │
│  (/trips/create) │             │    (/events)     │             │    VEHÍCULOS     │
└────────┬─────────┘             └────────┬─────────┘             │   (/profile)     │
         │                                │                       └────────┬─────────┘
         ▼                                ▼                                │
┌──────────────────┐             ┌──────────────────┐                      │
│ 7. DETALLE VIAJE │             │8. DETALLE EVENTO │                      │
│   (/trips/:id)   │             │   (/events/:id)  │                      │
└────────┬─────────┘             └────────┬─────────┘                      │
         │ (Reservar / Cola)              │ (Ver viajes de evento)         │
         └──────────────────┬─────────────┘                                │
                            ▼                                              ▼
                 ┌────────────────────┐                        ┌────────────────────┐
                 │ 9. MIS RESERVAS Y  │                        │10. GESTIÓN COCHES  │
                 │   LISTA DE ESPERA  │                        │(/profile/vehicles) │
                 │   (/my-bookings)   │                        └────────────────────┘
                 └────────────────────┘
```

---

## 🧩 2. Desglose Detallado de Pantallas y Componentes Angular

### 🖥️ PANTALLA 1: Landing Page / Inicio (`/home`)
* **Propósito**: Presentar la plataforma a la comunidad de Tajamar y permitir una búsqueda rápida.
* **Componentes en Angular**:
  1. `NavbarComponent` *(Shared)*:
     * **Muestra**: Logo Tajamar Mobility, Enlaces ("Buscar Viajes", "Eventos", "Publicar"), Botones "Iniciar Sesión" y "Registrarse" (o Avatar del usuario si está logueado).
     * **Funciones**: Navegación de rutas (`routerLink`), Cierre de sesión (`logout()`).
  2. `HeroSearchComponent`:
     * **Muestra**: Título atractivo, selector rápido de Origen, Destino (Tajamar por defecto), Fecha y tipo (Recurrente / Evento).
     * **Funciones**: Captura los parámetros de búsqueda y navega a `/trips?origen=...&fecha=...`.
  3. `FeatureCardsComponent`:
     * **Muestra**: 3 tarjetas explicativas (1. Ahorra y comparte gastos; 2. Conecta con tus compañeros de curso; 3. Asiste a eventos con la lista de espera).
  4. `UpcomingEventsSliderComponent`:
     * **Muestra**: Carrusel con los 3 próximos eventos de Tajamar.
     * **Funciones**: Clic en evento navega a `/events/:id`.

---

### 🔑 PANTALLA 2: Registro y Autenticación (`/login`, `/register`)
* **Propósito**: Autenticar usuarios vinculándolos a su curso académico.
* **Componentes en Angular**:
  1. `LoginFormComponent`:
     * **Muestra**: Formulario con Email (institucional/personal), Contraseña, opción "Recordarme".
     * **Funciones**: `onSubmit()` invoca `AuthService.login()`, almacena JWT en LocalStorage y redirige al Dashboard/Búsqueda.
  2. `RegisterFormComponent`:
     * **Muestra**: Nombre, Apellidos, Email, Contraseña, Selector de Curso Académico (`SelectComponent` cargado dinámicamente: ej: *1º DAM, 2º DAW, ASIR*), Teléfono.
     * **Funciones**: `onSubmit()` registra al usuario y le asigna el rol inicial dual.

---

### 🔍 PANTALLA 3: Catálogo y Búsqueda de Trayectos (`/trips`)
* **Propósito**: Permitir al pasajero encontrar trayectos recurrentes o de eventos.
* **Componentes en Angular**:
  1. `TripFilterBarComponent`:
     * **Muestra**: Filtros avanzados: Origen, Horario de Entrada/Salida, Modalidad (*Solo Ida*, *Solo Vuelta*, *Ida y Vuelta*), Tipo (*Recurrente* vs *Evento*), Filtro por Curso de origen.
     * **Funciones**: Emite evento `(onFilterChange)` para refrescar el listado.
  2. `TripGridComponent`:
     * **Muestra**: Contenedor responsive con las tarjetas de viaje. Muestra estado de carga (*Spinner*) o mensaje de "No hay viajes".
  3. `TripCardComponent` *(Shared - CORE)*:
     * **Muestra**:
       * Avatar y Nombre del Conductor + Badge del Curso (ej: *2º DAW*).
       * Etiqueta de Tipo: `[Recurrente]` (Azul) o `[Evento: Hackathon]` (Naranja).
       * Ruta: Origen ➔ Destino (Tajamar).
       * Horario y Días (ej: *L-V a las 07:45*).
       * Badge de Plazas:
         * 🟢 `X plazas disponibles` (si Plazas > 0).
         * 🟠 `COMPLETO - Lista de espera abierta` (si Plazas == 0).
     * **Funciones**: Clic en la tarjeta abre el detalle del viaje (`/trips/:id`).

---

### 📝 PANTALLA 4: Creación de Trayectos (`/trips/create`)
* **Propósito**: Permitir al conductor publicar un viaje (Recurrente o de Evento).
* **Componentes en Angular**:
  1. `TripCreateFormComponent`:
     * **Muestra**:
       * **Paso 1: Tipo de Trayecto**: Toggle entre `[Recurrente Diario]` y `[Puntual de Evento Tajamar]`.
       * **Paso 2: Datos de Ruta**: Origen (dirección/barrio), Destino (por defecto Tajamar o editable para eventos fuera).
       * **Paso 3: Modalidad y Horarios**:
         * Selector: *Solo Ida*, *Solo Vuelta*, *Ida y Vuelta*.
         * Hora de Ida / Hora de Vuelta.
         * Para Recurrentes: Checkboxes con Días de la semana (L, M, X, J, V).
         * Para Eventos: Select con el Evento oficial de Tajamar y Fecha exacta.
       * **Paso 4: Vehículo y Plazas**: Select de sus vehículos registrados, número de plazas ofertadas, notas/comentarios (ej: *"No se fuma"*).
     * **Funciones**: Validaciones reactivas (`ReactiveFormsModule`), envía `POST /api/trips`, muestra notificación de éxito y redirige a `/my-bookings`.

---

### ℹ️ PANTALLA 5: Detalle del Trayecto y Reserva (`/trips/:id`)
* **Propósito**: Ver toda la información del viaje y solicitar plaza o lista de espera.
* **Componentes en Angular**:
  1. `TripHeaderComponent`:
     * **Muestra**: Banner de la ruta, badge de modalidad (*Ida y Vuelta*), días/fecha.
  2. `DriverProfileCardComponent`:
     * **Muestra**: Foto del conductor, Nombre, Curso académico, Valoraciones/Opiniones, Vehículo (Marca, Modelo, Color).
  3. `TripItineraryComponent`:
     * **Muestra**: Línea de tiempo visual (Punto A de recogida ➔ Hora ➔ Tajamar).
  4. `PassengersListComponent`:
     * **Muestra**: Lista de pasajeros ya confirmados en el coche.
  5. `BookingActionPanelComponent` *(SHARED KEY COMPONENT)*:
     * **ESTADO A (Hay Plazas Libres > 0)**:
       * **Muestra**: Contador de plazas restantes (ej: *2 plazas libres*).
       * **Acción**: Botón Verde `[Reservar Plaza]` ➔ Llama a `BookingService.bookTrip(tripId)`.
     * **ESTADO B (Plazas Llenas == 0 & Es Evento)**:
       * **Muestra**: Badge Alerta *"Vehículo completo"*, número de personas en la cola actualmente (ej: *3 usuarios en espera*).
       * **Acción**: Botón Naranja `[Unirse a la Cola de Espera]` ➔ Llama a `WaitlistService.joinWaitlist(tripId)`.
     * **ESTADO C (El usuario YA está en la Lista de Espera)**:
       * **Muestra**: Banner Informativo: *"Estás en la posición #2 de la cola de espera"*.
       * **Acción**: Botón Rojo/Gris `[Abandonar Cola de Espera]`.

---

### 🎓 PANTALLA 6: Eventos de Tajamar (`/events` y `/events/:id`)
* **Propósito**: Gestión y visualización de eventos del centro y sus viajes enlazados.
* **Componentes en Angular**:
  1. `EventCardComponent`:
     * **Muestra**: Imagen/Banner del evento, Nombre (ej: *Hackathon Tajamar 2026*), Fecha, Hora, Lugar, número de trayectos ofertados por conductores.
  2. `EventDetailComponent`:
     * **Muestra**: Descripción oficial del evento + Mapa + Botón `[+ Ofrecer mi coche para este evento]`.
  3. `EventTripsListComponent`:
     * **Muestra**: Muestra únicamente los trayectos puntuales asociados a este evento concreto.

---

### 👤 PANTALLA 7: Mi Perfil y Gestión de Vehículos (`/profile`)
* **Propósito**: Administrar datos personales, cursos y coches.
* **Componentes en Angular**:
  1. `UserProfileCardComponent`:
     * **Muestra**: Foto, Nombre, Email, Curso asignado, Rol activo (Conductor / Pasajero).
  2. `VehicleListComponent`:
     * **Muestra**: Tarjetas con los vehículos del usuario (Marca, Modelo, Color, Matrícula, Plazas).
  3. `VehicleFormComponent` *(Modal / Component)*:
     * **Muestra**: Formulario para registrar/editar un vehículo.

---

### 📋 PANTALLA 8: Mis Reservas y Gestión de Cola (`/my-bookings`)
* **Propósito**: Panel de control del usuario para ver sus viajes como pasajero o conductor.
* **Componentes en Angular**:
  1. `BookingTabsComponent`:
     * Tab 1: `[Como Pasajero]` | Tab 2: `[Como Conductor]`.
  2. `PassengerBookingsListComponent`:
     * **Muestra**: Tarjetas de reservas confirmadas + Tarjetas de **Solicitudes en Lista de Espera** con su posición en tiempo real (#1, #2...).
     * **Funciones**: Botón `[Cancelar Reserva]` (que libera la plaza para el 1º de la cola) o `[Salir de la Cola]`.
  3. `DriverTripsListComponent`:
     * **Muestra**: Sus viajes publicados + Lista de pasajeros confirmados en su coche + Lista de usuarios en cola.
