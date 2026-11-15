# 🏗️ Propuesta de Arquitectura y Tecnologías

Dado que el requisito obligatorio de Base de Datos es **Microsoft SQL Server**, proponemos dos alternativas tecnológicamente sólidas para el desarrollo de la aplicación.

---

## 🛠️ Stack Tecnológico Recomendado

### Opción 1: Ecosistema Microsoft Nativo (RECOMENDADO PARA TAJAMAR)
- **Backend**: **.NET 8 Web API (C#)**
  - *Ventajas*: Integración perfecta y nativa con SQL Server mediante **Entity Framework Core 8**. Alto rendimiento, fuertemente tipado y muy alineado con la formación académica en Tajamar.
- **Frontend**: **React + Vite (TypeScript)** + **Tailwind CSS**
  - *Ventajas*: Componentización limpia, rápido tiempo de desarrollo, soporte excelente de tipos compartidos con el backend.
- **Base de Datos**: **Microsoft SQL Server** (A cargo de Paco).

### Opción 2: Ecosistema TypeScript Fullstack
- **Backend**: **Node.js + Express (o NestJS) + TypeScript**
  - *ORM*: **Prisma** o **TypeORM** con driver `mssql` / `tedious`.
- **Frontend**: **React + Vite / Next.js (TypeScript)** + **Tailwind CSS**.
- **Base de Datos**: **Microsoft SQL Server**.

---

## 📐 Estructura de Arquitectura Backend (Clean / Layered Architecture)

Para asegurar un código ordenado y escalable en el equipo:

```text
backend/
├── src/
│   ├── Controllers/     # Endpoints HTTP (Auth, Trayectos, Reservas, Eventos, ColaEspera)
│   ├── Services/        # Lógica de negocio (Reglas de cancelación, gestión de la cola FIFO)
│   ├── Repositories/    # Acceso a datos / EF Core DbContext
│   ├── Models/ Entities # Clases mapeadas a la DB de SQL Server
│   ├── DTOs/            # Data Transfer Objects para requests y responses
│   └── Middlewares/     # Manejo de errores globales, Autenticación JWT
└── Program.cs / app.ts  # Configuración e inyección de dependencias
```

---

## 💻 Estructura del Frontend

```text
frontend/
├── src/
│   ├── assets/          # Imágenes, iconos, estilos globales (Tailwind)
│   ├── components/      # Componentes UI reutilizables (Navbar, Cards, Modales, Inputs)
│   ├── pages/           # Páginas principales (Home, Login, Register, Trayectos, Eventos, Perfil)
│   ├── services/        # Cliente HTTP (Axios / Fetch) configurado con el Token JWT
│   ├── hooks/           # Custom Hooks (useAuth, useTrips, useWaitlist)
│   ├── context/         # Estado global (AuthContext, ThemeContext)
│   └── types/           # Interfaces e tipos de datos (User, Trip, Event, Booking)
```

---

## 🔌 Principales Endpoints API REST (Propuesta Inicial)

| Módulo | Método | Endpoint | Descripción |
| :--- | :--- | :--- | :--- |
| **Auth** | `POST` | `/api/auth/register` | Registro de usuario |
| **Auth** | `POST` | `/api/auth/login` | Login y obtención de JWT |
| **Usuarios**| `GET` | `/api/users/profile` | Obtener datos del perfil actual y vehículos |
| **Trayectos**| `GET` | `/api/trips` | Listar trayectos con filtros (origen, evento, etc.) |
| **Trayectos**| `POST` | `/api/trips` | Crear un nuevo trayecto (Recurrente o Puntual) |
| **Reservas** | `POST` | `/api/trips/{id}/book` | Reservar plaza en un trayecto |
| **Reservas** | `DELETE`| `/api/bookings/{id}` | Cancelar reserva (desencadena aviso a la cola) |
| **Cola** | `POST` | `/api/trips/{id}/waitlist` | Apuntarse a la lista de espera de un trayecto lleno |
| **Eventos** | `GET` | `/api/events` | Listar eventos de Tajamar |
