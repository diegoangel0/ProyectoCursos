



          
# Proyecto PlataformaCursos

## Descripción General

Proyecto Plataforma educativa de cursos; plataforma desarrollada con React en el frontend y PHP/MySQL en el backend. Resumen detallado de la estructura y funcionalidades del proyecto:

### Tecnologías Principales

- **Frontend**: React.js (v16.13.1)
- **Backend**: PHP con Apache
- **Base de datos**: MySQL
- **Gestión de paquetes**: npm y yarn
- **Estilos**: SASS, Bootstrap, MDBreact

### Estructura del Proyecto

El proyecto está organizado en las siguientes carpetas principales:

- `/src`: Código fuente de React
- `/server_apache_code`: Código PHP del backend
- `/public`: Archivos estáticos
- `/img_example`: Imágenes de ejemplo para la documentación

### Funcionalidades Principales

1. **Sistema de Gestión de Cursos**:
   - Panel administrativo para gestionar estudiantes
   - Creación y gestión de cursos
   - Creación y gestión de talleres dentro de cada curso
   - Cuestionarios, materiales didácticos y videos educativos

2. **Sistema de Usuarios**:
   - Registro y autenticación
   - Perfiles de usuario (estudiante, profesor, administrador)
   - Recuperación de contraseña por email
   - Gestión de información de perfil

3. **Funcionalidades para Estudiantes**:
   - Acceso a cursos asignados
   - Resolución de talleres
   - Visualización de notas
   - Recepción de notas por correo electrónico

4. **Funcionalidades para Administradores**:
   - Matriculación de estudiantes
   - Visualización de notas
   - Gestión de usuarios
   - Monitoreo de actividad (logins)
   - Configuración de caducidad de cursos

### Arquitectura

- **Frontend**: Aplicación SPA (Single Page Application) con React
- **Backend**: API REST en PHP
- **Seguridad**: Tokens de acceso, verificación de cookies, encriptación de contraseñas
- **Base de datos**: Procedimientos almacenados para operaciones complejas

## Configuración del Entorno

### Desarrollo

Para configurar el entorno de desarrollo:

1. Clonar el repositorio
2. Instalar Node.js
3. Ejecutar `npm install` en la carpeta raíz
4. Ejecutar `npm install yarn`
5. Ejecutar `yarn start` para iniciar el servidor de desarrollo

### Producción

Para desplegar en producción:

1. Ejecutar `yarn build`
2. Copiar el contenido de la carpeta `build` al directorio raíz del servidor
3. Copiar el contenido de `/server_apache/` a la misma carpeta
4. Configurar las variables de entorno según lo indicado en el README
5. Importar la estructura de la base de datos desde `/data_base_for_import/`
6. Crear un administrador ejecutando el script `creando_user.php`

## Consideraciones Importantes

- El proyecto tiene configuraciones específicas para desarrollo y producción
- Existen tareas cron que deben ejecutarse en el servidor (`regenerate_tokens.php` y `delete_token_restore_old.php`)
- La seguridad se maneja a través de tokens de acceso y verificación de cookies
- Las contraseñas se almacenan encriptadas en la base de datos

## Recomendaciones

1. **Seguridad**: Revisar y actualizar las dependencias con vulnerabilidades
2. **Optimización**: Considerar la implementación de lazy loading para mejorar el rendimiento
3. **Mantenimiento**: Establecer un sistema de logs más robusto para facilitar la depuración
4. **Escalabilidad**: Considerar la migración a una arquitectura más modular para facilitar el mantenimiento

Este análisis proporciona una visión general del proyecto. Para implementar mejoras específicas, sería necesario profundizar en componentes particulares según los requerimientos.

        



          
# Plataforma de Gestión de Cursos

## Tabla de Contenidos
- [Descripción del Proyecto](#descripción-del-proyecto)
- [Características Principales](#características-principales)
- [Arquitectura Técnica](#arquitectura-técnica)
- [Configuración de Desarrollo](#configuración-de-desarrollo)
- [Configuración del Entorno](#configuración-del-entorno)
- [Proceso de Compilación](#proceso-de-compilación)
- [Scripts Disponibles](#scripts-disponibles)
- [Consideraciones de Seguridad](#consideraciones-de-seguridad)

## Descripción del Proyecto
Sistema completo de gestión académica con acceso multi-rol (administrador/estudiante) construido con:
- **Frontend**: React + Bootstrap
- **Backend**: PHP + Apache
- **Base de Datos**: MySQL
- **API**: Arquitectura RESTful con autenticación JWT

En este proyecto se tiene un sistema de gestión de cursos desde un panel administrativo donde se podrá matricular estudiantes, visualizar sus notas, eliminarlos, monitorear quienes se han conectado, recuperar contraseñas por email, y modificar información en el perfil de cada usuario.

El sistema permite crear cursos, cada curso contiene talleres, y cada taller puede incluir cuestionarios, materiales didácticos y videos educativos. Todos estos elementos son editables, eliminables y están organizados en un buscador paginado. Cada curso tiene configuración de caducidad por fecha para cada usuario, gestionable desde el panel administrativo.

## Características Principales

### Panel de Administrador
| Característica         | Descripción                                                             |
|------------------------|-------------------------------------------------------------------------|
| Gestión de Usuarios    | Operaciones CRUD con monitoreo de actividad                            |
| Creación de Cursos     | Estructura jerárquica con políticas de vencimiento                     |
| Gestión de Contenidos  | Talleres dinámicos con cuestionarios, materiales y videos              |
| Controles de Seguridad | Sistema de recuperación de contraseña con validación por correo        |

### Portal del Estudiante
| Característica         | Descripción                                                             |
|------------------------|-------------------------------------------------------------------------|
| Gestión de Perfil      | Rotación segura de credenciales y modificación de datos                |
| Interacción con Cursos | Sistema de finalización de talleres con calificación automática        |
| Seguimiento de Progreso| Visualización de calificaciones en tiempo real y notificaciones por correo |

## Arquitectura Técnica

```text
Capa Cliente                  Capa Servidor                Capa de Datos
┌──────────────────────┐       ┌───────────────────┐        ┌──────────────┐
│ React SPA            │◄─────►│ Endpoints PHP API │◄─────► │ MySQL DB     │
│ Componentes Bootstrap│ HTTP  │ Autenticación JWT │   SQL  │ Tablas InnoDB│
│ Cliente Axios        │       │ Rutas RESTful     │        │              │
└──────────────────────┘       └───────────────────┘        └──────────────┘
```

## Configuración de Desarrollo

### Instalación
1. Clonar el proyecto:
```bash
git clone [url-repositorio]
```

2. Asegurarse de tener Node.js instalado para ejecutar comandos npm

3. Situarse dentro de la carpeta raíz y ejecutar:
```bash
npm install
```

4. Instalar Yarn:
```bash
npm install yarn
```

5. Configuración de base de datos:
```bash
mysql -u root -p < database/academic_system.sql
```

6. Configurar entorno:
```php
// apis/config.php
const MYSQL_HOST = 'localhost';
const MYSQL_USER = 'db_user';
const MYSQL_PASS = 'db_password';
const MODE_PROD = false;
```

7. Iniciar servidor de desarrollo:
```bash
yarn start
```

## Configuración del Entorno

Existen archivos o variables que se usan de manera diferente en desarrollo y producción:

| Configuración          | Desarrollo        | Producción              |
|------------------------|-------------------|-------------------------|
| IP_SERVIDOR_PETICIONES | http://localhost:3000 | ""                  |
| Seguridad de Cookies   | Secure=False      | Secure=True             |
| Modo Depuración API    | Habilitado        | Deshabilitado           |
| Validación de Token    | Opcional          | Aplicación Estricta     |

Detalles adicionales:
- En `constant_class` para producción, IP_SERVIDOR_PETICIONES_PHP va en blanco "", para desarrollo debe ser la URL donde se alojó el contenido de /server_apache_code/
- En `base_loginSystem` debe desactivarse el debugger en producción para no mostrar información en consola
- En `apis/config.php` el modo_produccion debe estar en true para producción, aceptando solo login con verificación de access token

## Proceso de Compilación

Para generar la versión de producción:

```bash
# Crear build de producción
yarn build

# Desplegar en servidor Apache
cp -r build/* /var/www/html/
cp -r server_apache_code/* /var/www/html/
```

## Scripts Disponibles

### Comandos Yarn/NPM
```bash
yarn start    # Iniciar servidor de desarrollo en http://localhost:3000
yarn build    # Crear build de producción optimizado
yarn test     # Ejecutar suite de pruebas
```

### Tareas Programadas (Cron Jobs)
```bash
# Rotación de tokens (diaria)
0 0 * * * php /var/www/html/apis/regenerate_tokens.php

# Limpieza de tokens (cada hora)
0 * * * * php /var/www/html/apis/delete_token_restore_old.php
```

## Consideraciones de Seguridad

### Protecciones Implementadas
- Prevención XSS mediante Content Security Policy
- Tokens CSRF en operaciones que modifican el estado
- Algoritmo de hashing de contraseñas seguro
- Forzado de HTTPS en producción

### Lista de Verificación Post-Despliegue
- Eliminar script de configuración:
```bash
rm apis/creando_user.php
```
- Configurar encriptación SSL/TLS
- Implementar limitación de tasa en endpoints de autenticación



# Documentación del Sistema de Gestión de Cursos

## 1. Diagramas de Casos de Uso

### 1.1 Diagrama de Caso de Uso: Registro de Usuario

```
+-----------------------------------+
|                                   |
|        Sistema de Cursos          |
|                                   |
+-----------------------------------+
              ^
              |
+-------------+-------------+
|                           |
|      Registrar Usuario    |
|                           |
+---------------------------+
              ^
              |
+-------------+-------------+
|        Usuario            |
+---------------------------+
              |
              v
+-------------+-------------+
|  Ingresar Datos Personales|<------+
+---------------------------+       |
              |                     |
              v                     |
+-------------+-------------+       |
|  Validar Información      |       |
+---------------------------+       |
              |                     |
              v                     |
+-------------+-------------+       |
|  ¿Datos Válidos?          |-------+ No
+---------------------------+
              | Sí
              v
+-------------+-------------+
|  Crear Cuenta             |
+---------------------------+
              |
              v
+-------------+-------------+
|  Enviar Confirmación      |
+---------------------------+
```

### 1.2 Diagrama de Caso de Uso: Creación de Cursos

```
+-----------------------------------+
|                                   |
|        Sistema de Cursos          |
|                                   |
+-----------------------------------+
              ^
              |
+-------------+-------------+
|                           |
|      Crear Curso          |
|                           |
+---------------------------+
              ^
              |
+-------------+-------------+
|     Administrador         |
+---------------------------+
              |
              v
+-------------+-------------+
|  Ingresar Datos del Curso |
+---------------------------+
              |
              v
+-------------+-------------+
|  Subir Imagen del Curso   |
+---------------------------+
              |
              v
+-------------+-------------+
|  Validar Información      |
+---------------------------+
              |
              v
+-------------+-------------+
|  Guardar en Base de Datos |
+---------------------------+
              |
              v
+-------------+-------------+
|  Curso Disponible         |
+---------------------------+
```

### 1.3 Diagrama de Caso de Uso: Creación de Talleres

```
+-----------------------------------+
|                                   |
|        Sistema de Cursos          |
|                                   |
+-----------------------------------+
              ^
              |
+-------------+-------------+
|                           |
|      Crear Taller         |
|                           |
+---------------------------+
              ^
              |
+-------------+-------------+
|     Administrador         |
+---------------------------+
              |
              v
+-------------+-------------+
|  Seleccionar Curso        |
+---------------------------+
              |
              v
+-------------+-------------+
|  Ingresar Datos del Taller|
+---------------------------+
              |
              v
+-------------+-------------+
|  Agregar Cuestionario     |
+---------------------------+
              |
              v
+-------------+-------------+
|  Agregar Material Didáctico|
+---------------------------+
              |
              v
+-------------+-------------+
|  Agregar Videos Educativos|
+---------------------------+
              |
              v
+-------------+-------------+
|  Guardar en Base de Datos |
+---------------------------+
              |
              v
+-------------+-------------+
|  Taller Disponible        |
+---------------------------+
```

### 1.4 Diagrama de Caso de Uso Completo

```
+-----------------------------------------------------------------------+
|                                                                       |
|                     Sistema de Gestión de Cursos                      |
|                                                                       |
+-----------------------------------------------------------------------+
                ^                    ^                    ^
                |                    |                    |
    +-----------+-----------+ +------+------+ +-----------+-----------+
    |                       | |             | |                       |
    |  Gestión de Usuarios  | | Gestión de  | |  Gestión de Talleres  |
    |                       | |   Cursos    | |                       |
    +-----------------------+ +-------------+ +-----------------------+
                ^                    ^                    ^
                |                    |                    |
    +-----------+-----------+ +------+------+ +-----------+-----------+
    | - Registrar Usuario   | | - Crear     | | - Crear Taller       |
    | - Modificar Perfil    | |   Curso     | | - Agregar Cuestionario|
    | - Cambiar Contraseña  | | - Matricular| | - Agregar Material   |
    | - Recuperar Contraseña| |   Estudiante| | - Calificar Talleres |
    +-----------------------+ +-------------+ +-----------------------+
                ^                    ^                    ^
                |                    |                    |
    +-----------+-----------+ +------+------+ +-----------+-----------+
    |                       | |             | |                       |
    |      Estudiante       | |Administrador| |      Administrador    |
    |                       | |             | |                       |
    +-----------------------+ +-------------+ +-----------------------+
                ^                    ^                    ^
                |                    |                    |
    +-----------+-----------+ +------+------+ +-----------+-----------+
    | - Ver Cursos          | | - Ver       | | - Ver Estadísticas   |
    | - Resolver Talleres   | |   Reportes  | | - Monitorear Accesos |
    | - Ver Notas           | | - Gestionar | | - Gestionar Fechas   |
    | - Ver Perfil          | |   Usuarios  | |   de Caducidad       |
    +-----------------------+ +-------------+ +-----------------------+
```

## 2. Ficha de Requerimientos

### 2.1 Requerimientos Funcionales

| ID Requerimiento | Descripción |
|-----------------|-------------|
| RF01 | Registro de usuarios: El sistema debe permitir el registro de nuevos usuarios con roles de estudiante, profesor o administrador. |
| RF02 | Autenticación de usuarios: El sistema debe permitir el inicio de sesión mediante email y contraseña, con validación de tokens de acceso. |
| RF03 | Recuperación de contraseña: El sistema debe permitir la recuperación de contraseña mediante correo electrónico. |
| RF04 | Gestión de perfil: Los usuarios deben poder ver y modificar su información personal y cambiar su contraseña. |
| RF05 | Creación de cursos: Los administradores deben poder crear nuevos cursos con título, descripción e imagen. |
| RF06 | Matriculación de estudiantes: Los administradores deben poder matricular estudiantes en cursos específicos. |
| RF07 | Creación de talleres: Los administradores deben poder crear talleres dentro de los cursos. |
| RF08 | Creación de cuestionarios: El sistema debe permitir la creación de cuestionarios con diferentes tipos de preguntas. |
| RF09 | Gestión de material didáctico: El sistema debe permitir agregar material didáctico a los talleres. |
| RF10 | Gestión de videos educativos: El sistema debe permitir agregar hasta 4 videos educativos por taller. |
| RF11 | Resolución de talleres: Los estudiantes deben poder resolver los talleres de los cursos en los que están matriculados. |
| RF12 | Calificación automática: El sistema debe calificar automáticamente los cuestionarios resueltos. |
| RF13 | Visualización de notas: Los estudiantes deben poder ver sus notas por taller y curso. |
| RF14 | Gestión de fechas de caducidad: El sistema debe controlar las fechas de caducidad de acceso a los cursos. |
| RF15 | Monitoreo de accesos: El sistema debe registrar los accesos de los usuarios. |
| RF16 | Reportes de notas: Los administradores deben poder ver reportes de notas por curso. |
| RF17 | Reportes de estudiantes inactivos: El sistema debe permitir identificar estudiantes que no han accedido a los cursos. |
| RF18 | Notificación por correo: El sistema debe enviar notificaciones por correo electrónico sobre notas y recuperación de contraseña. |

### 2.2 Requerimientos No Funcionales

| ID Requerimiento | Descripción |
|-----------------|-------------|
| RNF01 | Seguridad: El sistema debe encriptar las contraseñas y utilizar tokens de acceso para validar sesiones. |
| RNF02 | Compatibilidad: El sistema debe funcionar en los navegadores web más comunes (Chrome, Firefox, Safari). |
| RNF03 | Rendimiento: El sistema debe responder en menos de 3 segundos a las solicitudes del usuario. |
| RNF04 | Escalabilidad: El sistema debe soportar múltiples usuarios concurrentes. |
| RNF05 | Usabilidad: La interfaz debe ser intuitiva y fácil de usar para todos los tipos de usuarios. |
| RNF06 | Disponibilidad: El sistema debe estar disponible 24/7 con un tiempo de inactividad mínimo. |
| RNF07 | Mantenibilidad: El código debe estar bien estructurado para facilitar su mantenimiento. |
| RNF08 | Adaptabilidad: La interfaz debe ser responsive para adaptarse a diferentes dispositivos. |
| RNF09 | Interoperabilidad: El sistema debe poder integrarse con servicios de correo electrónico. |
| RNF10 | Configurabilidad: El sistema debe permitir configuraciones diferentes para entornos de desarrollo y producción. |

## 3. Diagrama de Clases

```
+------------------------+       +------------------------+       +------------------------+
|         User           |       |         Curso          |       |         Taller         |
+------------------------+       +------------------------+       +------------------------+
| - id: int              |       | - id_curso: int        |       | - id_taller: int       |
| - email: string        |       | - nombre: string       |       | - nombre_taller: string|
| - password: string     |       | - descripcion: string  |       | - descripcion: string  |
| - rol: string          |       | - imagen: blob         |       | - id_curso: int        |
| - nombres: string      |       +------------------------+       | - id_cuestionario: int |
| - apellidos: string    |       | + getCursos()          |       | - video_1: string      |
| - telefono: string     |       | + crearCurso()         |       | - video_2: string      |
| - tkn_accs: string     |       | + eliminarCurso()      |       | - video_3: string      |
+------------------------+       | + actualizarCurso()    |       | - video_4: string      |
| + login()              |       +------------------------+       +------------------------+
| + logout()             |               |                        | + getTalleres()        |
| + registrar()          |               |                        | + crearTaller()        |
| + actualizarPerfil()   |               |                        | + eliminarTaller()     |
| + cambiarPassword()    |               |                        | + actualizarTaller()   |
| + recuperarPassword()  |               |                        +------------------------+
+------------------------+               |                                    |
        |                                |                                    |
        |                                |                                    |
        v                                v                                    v
+------------------------+       +------------------------+       +------------------------+
|    CaducidadCurso      |       |         Nota           |       |     Cuestionario      |
+------------------------+       +------------------------+       +------------------------+
| - id_curso: int        |       | - id_nota: int         |       | - id_cuestionario: int|
| - id_usuario: int      |       | - id_estudiante: int   |       | - num_pregunta: int   |
| - caducidad_acceso: date|       | - id_taller: int       |       | - tipo_pregunta: string|
+------------------------+       | - id_curso: int        |       | - pregunta_txt: string|
| + asignarCaducidad()   |       | - nota: float          |       | - posibles_respuestas: string|
| + verificarCaducidad() |       +------------------------+       | - respuesta_correcta: string|
+------------------------+       | + obtenerNotas()       |       | - imagen_va_pregunta: blob|
                                | + asignarNota()        |       | - imagen_posible_r_1: blob|
                                +------------------------+       | - imagen_posible_r_2: blob|
                                                                | - imagen_posible_r_3: blob|
                                                                | - imagen_posible_r_4: blob|
                                                                +------------------------+
                                                                | + crearCuestionario()  |
                                                                | + obtenerCuestionario()|
                                                                +------------------------+
```

## 4. Diagrama de Paquetes

```
+-----------------------------------------------------------------------+
|                                                                       |
|                     Sistema de Gestión de Cursos                      |
|                                                                       |
+-----------------------------------------------------------------------+
                |                    |                    |
    +-----------+-----------+ +------+------+ +-----------+-----------+
    |                       | |             | |                       |
    |    Frontend (React)   | |   Backend   | |    Base de Datos      |
    |                       | |    (PHP)    | |      (MySQL)          |
    +-----------------------+ +-------------+ +-----------------------+
                |                    |                    |
    +-----------+-----------+ +------+------+ +-----------+-----------+
    | - Componentes         | | - APIs       | | - Tablas            |
    | - Páginas             | | - Servicios  | | - Procedimientos    |
    | - Estilos             | | - Seguridad  | | - Funciones         |
    | - Utilidades          | | - Validación | | - Relaciones        |
    +-----------------------+ +-------------+ +-----------------------+
                |                    |                    |
    +-----------+-----------+ +------+------+ +-----------+-----------+
    | - admin-panel         | | - admin_panel| | - users             |
    | - curso               | | - apis       | | - cursos            |
    | - cursos              | | - e_c_p.php  | | - talleres          |
    | - login               | | - config.php | | - notas             |
    | - perfil              | | - cookie_check| | - caducidad_cursos  |
    | - taller              | | - data_base  | | - cuestionarios     |
    +-----------------------+ +-------------+ +-----------------------+
```

## Resumen
La Visión general del sistema de gestión de cursos, incluimos los diagramas de casos de uso para registro de usuario, creación de cursos y talleres, así como un diagrama de casos de uso completo. También se adiciona una ficha con los requerimientos funcionales y no funcionales, un diagrama de clases que muestra las principales entidades del sistema y sus relaciones, y un diagrama de paquetes que ilustra la arquitectura general del sistema.
