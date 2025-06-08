# Boza-videos

Plataforma de streaming de videos desarrollada con Angular 16 para el frontend, NestJS para el backend y MariaDB como base de datos, desplegada en servidores CentOS. El proyecto implementa una arquitectura moderna y escalable siguiendo principios de clean code y desarrollo guiado por pruebas.

## Arquitectura del Sistema

La aplicación está construida siguiendo una arquitectura hexagonal que separa claramente las responsabilidades entre las diferentes capas del sistema. El frontend Angular utiliza una estructura modular con feature modules y lazy loading para optimizar el rendimiento, mientras que el backend NestJS implementa una arquitectura basada en dominios funcionales con módulos especializados para autenticación, gestión de usuarios y administración de contenido multimedia.

## Stack Tecnológico

### Frontend
- **Angular 16** con TypeScript estricto y standalone components
- **Angular Material** o **PrimeNG** para componentes UI consistentes
- **RxJS** para programación reactiva y manejo de streams
- **Angular Router** con lazy loading y guards de autenticación
- **Reactive Forms** con validaciones robustas

### Backend
- **NestJS** con TypeScript y sistema de decoradores
- **TypeORM** como ORM principal para interacción con base de datos
- **JWT** para autenticación stateless
- **Swagger/OpenAPI** para documentación automática de APIs
- **Class-validator** para validación de DTOs

### Base de Datos
- **MariaDB** con optimizaciones para consultas de video
- **Migraciones versionadas** para control de esquema
- **Connection pooling** para manejo eficiente de conexiones
- **Índices especializados** para búsquedas y categorización

### Infraestructura
- **CentOS** como sistema operativo de producción
- **PM2** para gestión de procesos Node.js
- **Nginx** como reverse proxy y servidor de archivos estáticos
- **Docker** para containerización (opcional)

## Características Principales

### Gestión de Contenido
El sistema permite la carga, categorización y gestión de contenido multimedia con soporte para múltiples formatos de video. Implementa transcoding automático para generar diferentes resoluciones y optimizar la experiencia de streaming según la conexión del usuario.

### Sistema de Usuarios
Autenticación y autorización robusta con JWT, perfiles de usuario personalizables, sistema de favoritos y listas personalizadas. Incluye roles diferenciados para administradores y usuarios finales con permisos granulares.

### Búsqueda y Categorización
Motor de búsqueda avanzada con filtros por categoría, duración, fecha de publicación y popularidad. Sistema de recomendaciones basado en historial de visualización y preferencias del usuario.

### Analytics y Monitoreo
Seguimiento detallado de métricas de visualización, tiempo de reproducción y patrones de uso. Dashboard administrativo para análisis de contenido y comportamiento de usuarios.

## Estructura del Proyecto

```
boza-videos/
├── frontend/                 # Aplicación Angular 16
│   ├── src/
│   │   ├── app/
│   │   │   ├── core/        # Servicios singleton y guards
│   │   │   ├── shared/      # Componentes y módulos compartidos
│   │   │   ├── features/    # Módulos de funcionalidades
│   │   │   └── layouts/     # Layouts de la aplicación
│   │   ├── assets/          # Recursos estáticos
│   │   └── environments/    # Configuraciones de entorno
├── backend/                  # API NestJS
│   ├── src/
│   │   ├── auth/            # Módulo de autenticación
│   │   ├── users/           # Gestión de usuarios
│   │   ├── videos/          # Gestión de contenido
│   │   ├── common/          # Utilidades compartidas
│   │   └── database/        # Configuración de base de datos
├── database/                 # Scripts y migraciones
│   ├── migrations/          # Migraciones de esquema
│   ├── seeders/            # Datos iniciales
│   └── scripts/            # Scripts de mantenimiento
└── deployment/              # Configuraciones de despliegue
    ├── nginx/              # Configuración Nginx
    ├── pm2/                # Configuración PM2
    └── docker/             # Dockerfiles (opcional)
```

## Instalación y Configuración

### Prerrequisitos
- Node.js 18+ y npm/yarn
- MariaDB 10.6+
- Git para control de versiones
- CentOS 7+ para producción

### Configuración del Backend

```bash
cd backend
npm install
cp .env.example .env
# Configurar variables de entorno en .env
npm run migration:run
npm run seed:run
npm run start:dev
```

### Configuración del Frontend

```bash
cd frontend
npm install
ng serve --open
```

### Variables de Entorno

El archivo `.env` debe incluir configuraciones para conexión a base de datos, secretos JWT, configuración de CORS y rutas de almacenamiento de archivos multimedia. Es fundamental configurar apropiadamente las variables de producción antes del despliegue.

## Testing

### Backend Testing
```bash
npm run test              # Unit tests
npm run test:e2e         # Integration tests
npm run test:cov         # Coverage report
```

### Frontend Testing
```bash
ng test                  # Unit tests con Jest
ng e2e                   # End-to-end tests
```

## Despliegue en Producción

### Configuración de Nginx
El servidor Nginx actúa como reverse proxy para el backend NestJS y sirve los archivos estáticos del frontend Angular. La configuración incluye compresión gzip, cache headers apropiados y redirecciones HTTPS.

### Gestión de Procesos con PM2
PM2 maneja los procesos Node.js del backend, proporcionando restart automático, clustering y monitoreo de recursos. La configuración incluye logs centralizados y alertas de rendimiento.

### SSL/TLS con Let's Encrypt
Implementación de certificados SSL gratuitos con renovación automática para garantizar conexiones seguras en producción.

## Contribución

El proyecto sigue conventional commits para mensajes de Git y utiliza pull requests para code review. Todas las contribuciones deben incluir tests apropiados y mantener el coverage mínimo del 80%. Se requiere que el código pase los linters de TypeScript y las validaciones de formato antes de ser integrado.

## Licencia

Este proyecto está licenciado bajo los términos especificados en el archivo LICENSE del repositorio.

## Soporte y Documentación

Para documentación técnica detallada, consulta la documentación automática de Swagger disponible en `/api/docs` una vez que el backend esté ejecutándose. Para reportar issues o solicitar nuevas funcionalidades, utiliza el sistema de issues de GitHub del proyecto.