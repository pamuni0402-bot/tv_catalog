## Backlog: TV Catalog

## EPIC 1: Gestión de Series
**Objetivo:** Administrar el catálogo de series.

### Historia de Usuario
**Como** usuario  
**Quiero** agregar, editar y eliminar series  
**Para** mantener actualizado el catálogo.

### Criterios de aceptación
- Agregar una serie.
- Editar una serie.
- Eliminar una serie.

---

## EPIC 2: Búsqueda de Series
**Objetivo:** Buscar series por nombre.

### Historia de Usuario
**Como** usuario  
**Quiero** buscar una serie por su nombre  
**Para** encontrarla rápidamente.

### Criterios de aceptación
- Buscar por título.
- Mostrar resultados encontrados.

---

## EPIC 3: Clasificación por Género
**Objetivo:** Organizar las series por categoría.

### Historia de Usuario
**Como** usuario  
**Quiero** filtrar las series por género  
**Para** encontrar contenido de mi interés.

### Criterios de aceptación
- Mostrar géneros disponibles.
- Filtrar correctamente.

---

## EPIC 4: Calificaciones
**Objetivo:** Calificar las series.

### Historia de Usuario
**Como** usuario  
**Quiero** calificar una serie de 1 a 5 estrellas  
**Para** compartir mi opinión.

### Criterios de aceptación
- Registrar calificación.
- Mostrar promedio.

---

## EPIC 5: Favoritos
**Objetivo:** Guardar series favoritas.

### Historia de Usuario
**Como** usuario  
**Quiero** guardar mis series favoritas  
**Para** acceder a ellas fácilmente.

### Criterios de aceptación
- Agregar a favoritos.
- Eliminar de favoritos.
- Mostrar lista de favoritos.

---

## EPIC 6: Registro de Usuario

## Historia de Usuario
**Como** nuevo usuario  
**Quiero** registrarme con mis datos personales  
**Para** poder acceder al sistema de series de televisión.

### Criterios de aceptación
Scenario: Registro exitoso 


Scenario: Registro exitoso
Given que el usuario está en registro
When completa los datos y confirma la contraseña 
Then el sistema crea la cuenta y muestra "Registro exitoso"

Scenario: Correo ya registrado
Given que el correo ya existe
When el usuario intenta registrarse 
Then el sistema muestra "El correo ya está registrado"

Scenario: Contraseñas diferentes
Given que el usuario llena el formulario 
When las contraseñas no coinciden
Then el sistema muestra "Las contraseñas no coinciden"

---

## EPIC 7: Inicio de Sesión

## Historia de Usuario
**Como** usuario registrado  
**Quiero** iniciar sesión con mi correo y contraseña  
**Para** acceder a mi cuenta.

### Criterios de aceptación
- El usuario debe ingresar:
  - Correo electrónico
  - Contraseña
- Si los datos son correctos, el sistema permitirá el acceso.
- Si los datos son incorrectos, mostrará:
  **"Correo o contraseña incorrectos".**

---
