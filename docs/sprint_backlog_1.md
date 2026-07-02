## Sprint Goal
"Implementar el núcleo de la aplicación permitiendo a los usuarios registrarse e iniciar sesión de forma segura, gestionar el catálogo de series (crear, editar, eliminar) y buscar series específicas por su nombre en tiempo real."

 Definition of Done (DoD)
Para que cualquier elemento del Sprint Backlog se considere Hecho (Done):

El código compila sin errores ni warnings de linter severos en Dart/Flutter.

La arquitectura (ej. BLoC, Riverpod o Provider) separa limpiamente la UI de la lógica de Firebase.

Las reglas de seguridad en Firebase Auth y Firestore están configuradas para que solo usuarios autenticados operen el catálogo.

Las búsquedas responden en menos de 1 segundo y gestionan correctamente estados vacíos (cuando no hay coincidencias).

Se ejecutaron y aprobaron los escenarios Gherkin definidos mediante pruebas de caja negra o manuales.

 Sprint Backlog (Desglose de Tareas)
 EPIC 6 & 7: Registro e Inicio de Sesión
Historias incluidas: HU-06 (Registro de Usuario) y HU-07 (Inicio de Sesión).

Task 1: Setup Inicial del Proyecto e Infraestructura Firebase

Subtáreas:

Crear el proyecto Flutter y configurar la estructura de directorios por capas o features.

Vincular la App en la consola de Firebase (Android/iOS) e instalar firebase_core y firebase_auth.

Dependencies: Ninguna.

Impediments: Retrasos técnicos con las llaves SHA-1 de Android o certificados de desarrollo en iOS.

Task 2: UI de Autenticación (Login y Registro)

Subtáreas:

Diseñar pantallas de login y registro usando componentes de Material 3.

Implementar validaciones locales en los formularios (campos vacíos, formato de correo, contraseñas coincidentes).

Dependencies: Task 1.

Impediments: Ninguno.

Task 3: Servicio de Autenticación con Firebase Auth

Subtáreas:

Crear los métodos de login y registro conectando con las funciones nativas de Firebase.

Mapear los códigos de error de Firebase (ej: email-already-in-use, invalid-credential) para mostrarlos como alertas amigables al usuario.

Dependencies: Task 2.

Impediments: Bloqueos temporales de IP por parte de Firebase si se realizan pruebas repetitivas de forma brusca.

 EPIC 1: Gestión de Series (CRUD)
Historias incluidas: HU-01 (Gestión de Series).

Task 4: Modelado de Datos y Base de Datos (Cloud Firestore)

Subtáreas:

Definir la entidad y modelo TvShow en Dart (id, nombre, sinopsis, urlImagen).

Crear la colección series en Firestore y configurar las reglas de acceso (Read/Write solo para usuarios con Auth activa).

Dependencies: Task 1.

Impediments: Ninguno.

Task 5: Vista de Catálogo Principal (Lectura y Eliminación)

Subtáreas:

Implementar la pantalla principal que consume el Stream de Firestore en tiempo real.

Diseñar las tarjetas de las series y añadir un botón/gesto para eliminar, incluyendo un diálogo de confirmación ("¿Estás seguro?").

Dependencies: Task 4.

Impediments: Errores de permisos en las reglas de Firestore al intentar ejecutar el método delete.

Task 6: Formulario para Agregar y Editar Series (Escritura y Actualización)

Subtáreas:

Crear un formulario reutilizable para capturar el nombre, sinopsis y link de imagen de la serie.

Programar la lógica para que, si recibe una serie existente, rellene los campos automáticamente en modo "Editar".

Integrar los servicios add() y update() de Firestore.

Dependencies: Task 5.

Impediments: Controlar el desbordamiento de texto en la interfaz si el usuario ingresa sinopsis extremadamente largas.

 EPIC 2: Búsqueda de Series
Historias incluidas: HU-02 (Búsqueda de Series).

Task 7: Barra de Búsqueda en UI y Filtrado Local/Remoto

Subtáreas:

Integrar un componente de búsqueda (ej. SearchAnchor o un TextField dinámico) en la parte superior del catálogo principal.

Implementación técnica: Dado que Firestore no tiene búsqueda por texto completo nativa avanzada (tipo algolia), implementar un filtrado mediante queries de rango (where('nombre', isGreaterThanOrEqualTo: query)) o cargar la lista inicial y filtrarla localmente en el cliente con Dart si el volumen de datos es pequeño/controlado.

Diseñar un estado visual de "No se encontraron resultados" si la búsqueda es infructífera.

Dependencies: Task 5 (Debe existir un catálogo y datos que buscar).

Impediments: Limitaciones de Firestore para búsquedas parciales (case-insensitive o subcadenas intermedias), lo cual requerirá normalizar los nombres guardándolos en minúsculas en un campo oculto (ej: nombre_lowercase).

 Flujo de Trabajo y Dependencias del Sprint
Para evitar que los desarrolladores se bloqueen entre sí, el orden de ejecución recomendado es:

[Task 1: Configuración General]
       │
       ├──► [Task 2 & 3: Flujo Completo de Autenticación (Epics 6 y 7)]
       │
       └──► [Task 4: Base de Datos] ──► [Task 5 & 6: CRUD de Series (Epic 1)] ──► [Task 7: Búsqueda (Epic 2)]
 Impedimentos Generales del Equipo
Normalización de búsquedas en Firestore: Firestore distingue entre mayúsculas y minúsculas. Si este impedimento no se ataja en la Task 4 (creando un campo indexado en minúsculas), la búsqueda de la Epic 2 fallará cuando el usuario busque "breaking bad" en lugar de "Breaking Bad".

Configuración del simulador/emulador: Asegurarse de que los emuladores locales tengan acceso a internet para comunicarse con Firebase sin problemas de proxy.
