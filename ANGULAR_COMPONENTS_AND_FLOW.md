# 🅰️ Arquitectura Angular, Componentes y Flujo de Pantallas (Sprints 2 y 3)

Este documento define la estructura de componentes en **Angular**, el flujo de pantallas y botones para las fases clave del proyecto (*Gestión de Trayectos, Perfiles, Eventos y Reservas*).

---

## 🧩 1. Estructura de Componentes en Angular

Usaremos componentes de Angular ordenados por módulos/carpetas (`Standalone Components` o módulos por funcionalidad):

```text
src/app/
├── core/                        # Servicios globales, Guards e Interceptors
│   ├── guards/ (auth.guard.ts)
│   ├── interceptors/ (jwt.interceptor.ts)
│   └── services/ (auth.service.ts, trip.service.ts, event.service.ts)
│
├── shared/                      # Componentes UI reutilizables
│   ├── components/
│   │   ├── navbar/ (navbar.component.ts)
│   │   ├── footer/ (footer.component.ts)
│   │   ├── trip-card/ (trip-card.component.ts)
│   │   ├── event-card/ (event-card.component.ts)
│   │   ├── vehicle-card/ (vehicle-card.component.ts)
│   │   ├── badge-status/ (badge-status.component.ts)
│   │   └── modal/ (modal.component.ts)
│
└── features/                    # Módulos / Páginas por funcionalidad
    ├── profile/                 # SPRINT 2
    │   ├── profile-view/
    │   └── vehicle-manager/
    │
    ├── trips/                   # SPRINT 2
    │   ├── trip-list/ (Búsqueda y filtros)
    │   ├── trip-create/ (Formulario recurrente / puntual)
    │   └── trip-detail/ (Información completa + botón reservar)
    │
    ├── events/                  # SPRINT 3
    │   ├── event-list/ (Eventos Tajamar)
    │   └── event-detail/ (Evento + viajes temporales asociados)
    │
    └── bookings/                # SPRINT 3
        └── my-bookings/ (Mis reservas activas como pasajero / viajes creados como conductor)
```

---

## 📱 2. Flujo de Pantallas y Botones (Step-by-Step)

### 🔴 FLUJO 1: Conductor registra vehículo y publica un trayecto (Sprint 2)

```text
[ Pantalla Mi Perfil ] ──( Botón "Mis Vehículos" )──> [ Modal / Lista Vehículos ] ──( Botón "+ Añadir Coche" )──> [ Formulario Vehículo ]
                                                                                                                         │ (Guardar)
                                                                                                                         ▼
[ Dashboard / Navbar ] ──( Botón "+ Publicar Trayecto" )──> [ Formulario Crear Viaje ] <───────────────────────────────────┘
                                                                 │
                                                                 ├── Selector Tipo: [ Recurrente ] vs [ Puntual / Evento ]
                                                                 ├── Inputs: Origen, Destino (Tajamar por defecto), Horarios, Días, Plazas, Vehículo
                                                                 │
                                                                 └── ( Botón "Publicar Viaje" ) ──> Redirección a [ Mis Trayectos ]
```

---

### 🟢 FLUJO 2: Pasajero busca y reserva un trayecto recurrente (Sprint 2)

```text
[ Navbar ] ──( Botón "Buscar Viaje" )──> [ Pantalla TripList ]
                                              │
                                              ├── Bar de Filtros: [ Origen ] | [ Hora Entrada/Salida ] | [ Curso/Grado ]
                                              │
                                              ├── Grid de `TripCardComponent`
                                              │      └── Muestra: Avatar Conductor, Ruta, Plazas Restantes (Badge Verde), Horario
                                              │
                                              └── ( Botón "Ver Detalle" ) ──> [ Pantalla TripDetail ]
                                                                                  │
                                                                                  ├── Mapa/Ruta + Info Vehículo
                                                                                  └── ( Botón "Solicitar Plaza" ) ──> [ Modal Confirmación ]
                                                                                                                          │ (Confirmar)
                                                                                                                          ▼
                                                                                                                [ Pantalla Mis Reservas ]
```

---

### 🟡 FLUJO 3: Pasajero consulta Evento Tajamar y reserva / entra en cola (Sprint 3)

```text
[ Navbar ] ──( Botón "Eventos Tajamar" )──> [ Pantalla EventList ]
                                                 │
                                                 └── Tarjeta de Evento (ej: "Hackathon 2026") ──( Botón "Ver Trayectos" )──> [ Pantalla EventDetail ]
                                                                                                                                  │
                                                                                                                                  ├── Lista de viajes temporales creados para este evento
                                                                                                                                  │
                                                                                                                                  ├── Si Hay Plazas (Plazas > 0):
                                                                                                                                  │    └── ( Botón Verde "Reservar Plaza" )
                                                                                                                                  │
                                                                                                                                  └── Si NO Hay Plazas (Plazas == 0):
                                                                                                                                       └── ( Botón Naranja "Unirse a Lista de Espera" )
                                                                                                                                                │ (Click)
                                                                                                                                                ▼
                                                                                                                                    Se registra la posición FIFO (ej: Posición 2 en la cola)
```
