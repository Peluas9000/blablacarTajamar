# 🌿 Estrategia de Git, Ramas y Integración Continua

Para evitar conflictos y mantener el código limpio en el proyecto de equipo, utilizaremos una adaptación de **GitFlow / GitHub Flow**.

---

## 🌲 Estructura de Ramas

```text
main (Producción / Entregable estable)
 └── develop (Integración de características terminadas)
      ├── feature/frontend-login
      ├── feature/frontend-trip-card
      ├── feature/backend-waitlist-service
      └── feature/sql-schema-integration
```

### Roles de las Ramas:
1. **`main`**: Contiene únicamente código estable, probado y listo para presentar. **Nadie sube código directamente a `main`**.
2. **`develop`**: Rama base de trabajo diario donde se integran las funcionalidades probadas.
3. **`feature/frontend-*`**: Ramas individuales para tareas de Frontend.
4. **`feature/backend-*`**: Ramas individuales para tareas de Backend.
5. **`hotfix/*`**: Para corrección urgente de errores críticos.

---

## 🔄 Flujo de Integración y Merge al `main` (Paso a Paso)

### 1. Creación de una Feature
```bash
# Actualizar rama develop local
git checkout develop
git pull origin develop

# Crear nueva rama de función
git checkout -b feature/frontend-reserva-plazas
```

### 2. Desarrollo y Commits Limpios
Utilizar **Conventional Commits** para mantener un historial claro:
- `feat(frontend): añadir formulario de creación de viaje`
- `fix(backend): corregir validación de plazas negativas`
- `docs: actualizar readme con nuevos endpoints`
- `style: mejorar responsividad de la card de evento`

### 3. Creación del Pull Request (PR)
- Al finalizar una tarea en la rama `feature/frontend-...`, subir la rama a GitHub/GitLab:
  ```bash
  git push origin feature/frontend-reserva-plazas
  ```
- Abrir un **Pull Request (PR)** hacia la rama **`develop`**.

### 4. Reglas para Aceptar / Mergear un PR:
- 🟢 **Mínimo 1 revisión de código** por parte de otro compañero.
- 🟢 **Sin conflictos**: Resolver posibles conflictos localmente antes de mergear.
- 🟢 El código debe compilar/ejecutar correctamente sin romper la aplicación.

### 5. Merge Final a `main`
- El Merge de `develop` a **`main`** se realiza únicamente en hitos de entrega o al finalizar un Sprint donde todas las funcionalidades están probadas y validadas.
- El Merge al `main` del Frontend y Backend debe coordinarse asegurando que los endpoints desplegados coincidan con las llamadas de la interfaz.

---

## 🛡️ Buenas Prácticas del Equipo

1. **Pull Diario**: Antes de empezar a programar, hacer `git pull origin develop` en tu rama para mantenerte al día.
2. **Commits Pequeños**: Commits frecuentes y focalizados en una sola tarea.
3. **Comunicación en Cambios de API**: Si Backend cambia una respuesta HTTP o un parámetro, avisar al canal del equipo antes de mergear.
