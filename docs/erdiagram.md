# Formato de codigo 
```mermaid
erDiagram

    USUARIO ||--o{ CALIFICACION : "registra"
    USUARIO ||--o{ FAVORITO : "guarda"
    SERIE ||--o{ CALIFICACION : "recibe"
    SERIE ||--o{ FAVORITO : "pertenece_a"
    SERIE }o--o{ GENERO : "tiene"

    USUARIO {
        string id_usuario PK
        string nombre
        string correo
        string contrasena_hash
        date fecha_registro
    }

    SERIE {
        string id_serie PK
        string nombre
        string sinopsis
        int anio_lanzamiento
        float promedio_calificacion
    }

    GENERO {
        string id_genero PK
        string nombre
    }

    CALIFICACION {
        string id_calificacion PK
        string id_usuario FK
        string id_serie FK
        int estrellas "1 a 5"
        date fecha
    }

    FAVORITO {
        string id_favorito PK
        string id_usuario FK
        string id_serie FK
        date fecha_agregado
    }
```
# Descripción 
### USUARIO (EPIC 6 y 7): Almacena las credenciales y datos básicos generados en el registro e inicio de sesión.

### SERIE (EPIC 1 y 2): Contiene los datos requeridos por el catálogo. El atributo promedio_calificacion resuelve la HU-04.2, calculándose y actualizándose cada vez que se agregue una calificación.

### GENERO (EPIC 3): Permite categorizar las series. En Firestore, la relación de muchos a muchos (SERIE }o--o{ GENERO) se puede resolver de forma óptima guardando un Array de IDs de géneros directamente dentro del documento de la Serie.

### CALIFICACION (EPIC 4): Entidad intermedia que rompe la relación muchos a muchos entre Usuarios y Series. Registra cuántas estrellas asignó un usuario específico a una serie.

### FAVORITO (EPIC 5): Permite mapear qué series ha guardado el usuario en "Mi Lista". En un esquema puro de Firestore, esto se podría estructurar como una subcolección dentro de USUARIO llamada favoritos.
