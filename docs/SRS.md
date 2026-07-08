# Especificación de Requisitos de Software (SRS)
## Proyecto: TV Catalog

---

## 1. Introducción
Este documento detalla los requisitos funcionales, no funcionales y el stack tecnológico para el desarrollo de la aplicación móvil **TV Catalog**. La aplicación está diseñada para que los usuarios puedan explorar, buscar, organizar y hacer seguimiento de sus series de televisión favoritas, ofreciendo una experiencia fluida e interactiva en tiempo real.

---

## 2. Stack Tecnológico

La arquitectura de la aplicación se basará en una solución moderna, multiplataforma y *serverless*, optimizada para el rendimiento multimedia y la actualización de datos constante.

| Componente | Tecnología | Razón de Selección |
| :--- | :--- | :--- |
| **Frontend Móvil** | Dart / Flutter | Permite un desarrollo multiplataforma (iOS y Android) con un solo código base, garantizando animaciones fluidas (60/120 fps) ideales para navegación de catálogos visuales. |
| **Base de Datos** | Firebase Cloud Firestore | Base de Datos NoSQL que permite almacenar la información de las series, temporadas, episodios y el progreso del usuario con sincronización instantánea. |
| **Autenticación** | Firebase Authentication | Manejo seguro de sesiones (Email, Google, Apple) para que el usuario mantenga su lista de favoritos sincronizada en cualquier dispositivo. |
| **Almacenamiento** | Firebase Cloud Storage | Almacenamiento optimizado para imágenes de perfil de usuarios y assets multimedia si es requerido. |
| **Integración de Datos** | API Externa (Opcional, ej. TMDB) | Consumo de servicios REST para alimentar el catálogo con miles de series actualizadas, conectándose mediante Flutter (paquete `http` o `dio`). |

---

## 3. Requisitos Funcionales (RF)

### RF01: Gestión de Usuarios y Perfiles
* **RF01.1:** El sistema debe permitir el registro e inicio de sesión mediante correo/contraseña y cuentas de Google/Apple.
* **RF01.2:** El sistema debe permitir al usuario personalizar su perfil (nombre, foto y géneros de series favoritos).
* **RF01.3:** Los datos de personalización del usuario deben almacenarse de forma persistente en Firestore.

### RF02: Catálogo y Exploración de Series
* **RF02.1:** La aplicación debe mostrar una pantalla principal con secciones organizadas: "Series Tendencia", "Estrenos", "Más Populares" y "Recomendadas por Género".
* **RF02.2:** El sistema debe permitir visualizar el detalle de cada serie, incluyendo: sinopsis, póster, año de lanzamiento, calificación, elenco, y lista de temporadas/episodios.
* **RF02.3:** El sistema debe permitir la reproducción de trailers de las series (mediante reproductores integrados en Flutter).

### RF03: Motor de Búsqueda y Filtros
* **RF03.1:** El usuario debe poder buscar series por título en tiempo real a través de una barra de búsqueda.
* **RF03.2:** El sistema debe ofrecer filtros avanzados por género, año de emisión, estado de la serie (En emisión / Finalizada) y plataforma de streaming original.

### RF04: Gestión de Favoritos y Seguimiento ("Mi Lista")
* **RF04.1:** El usuario debe poder marcar series como "Favoritas" o agregarlas a una lista de "Por ver".
* **RF04.2:** El sistema debe permitir al usuario marcar episodios individuales como "Vistos" para llevar un control del progreso de la temporada.
* **RF04.3:** La lista de seguimiento y progreso de episodios debe sincronizarse automáticamente en la cuenta de Firebase del usuario.

### RF05: Notificaciones push
* **RF05.1:** El sistema debe enviar notificaciones push automáticas (vía Firebase Cloud Messaging) cuando se estrene un nuevo episodio de una serie que el usuario tenga en su lista de favoritos.

---

## 4. Requisitos No Funcionales (RNF)

### RNF01: Rendimiento y Experiencia de Usuario (UX)
* **RNF01.1:** El catálogo de imágenes (pósters y banners) debe implementar una estrategia de *lazy loading* y caché local de imágenes (usando `cached_network_image` en Flutter) para evitar el consumo excesivo de datos.
* **RNF01.2:** La navegación entre pantallas y el scroll de las listas de series deben mantener una tasa constante de 60fps.

### RNF02: Seguridad y Reglas de Acceso
* **RNF02.1:** El acceso a la lectura y escritura de las listas de favoritos e historial de visualización en Firestore debe estar restringido estrictamente al usuario propietario mediante **Firebase Security Rules**.
* **RNF02.2:** Las llaves de API externas (si se usan) deben mantenerse protegidas y no exponerse directamente en el código fuente público.

### RNF03: Disponibilidad y Soporte Offline
* **RNF03.1:** La aplicación debe permitir el acceso a "Mi Lista" y al progreso de las series guardadas incluso si el dispositivo no cuenta con conexión a Internet, sincronizando los cambios pendientes con Firestore tan pronto como se recupere la conectividad.

### RNF04: Compatibilidad
* **RNF04.1:** La aplicación móvil debe ser totalmente responsiva y compatible con teléfonos inteligentes Android (versión 8.0 o posterior) e iOS (versión 15 o posterior).

---

## 5. Estructura del Proyecto (Flutter)

Para asegurar la escalabilidad de **TV Catalog**, se estructurará el frontend utilizando arquitectura de capas orientada a funciones (Feature-First) junto con un gestor de estado eficiente (*Bloc* o *Riverpod*):

```text
lib/
│
├── core/                  # Configuraciones globales, temas, router y servicios de Firebase
│
├── features/              # Funcionalidades de la aplicación
│   ├── auth/              # Autenticación de usuarios
│   ├── catalog/           # Exploración, búsqueda y detalle de series
│   └── user_list/         # Favoritos, historial y seguimiento de episodios
│
└── main.dart              # Punto de entrada de la aplicación
