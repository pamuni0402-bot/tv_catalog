# Product Backlog - TV Catalog

## EPIC 1: Gestión de Series

### HU-01: Gestión de Series

**Como** usuario
**Quiero** agregar, editar y eliminar series
**Para** mantener actualizado el catálogo.

```gherkin
Scenario: Agregar una serie
  Given que el usuario está en el catálogo
  When agrega una nueva serie con todos los datos requeridos
  Then la serie se guarda correctamente

Scenario: Editar una serie
  Given que existe una serie registrada
  When el usuario modifica su información
  Then los cambios se guardan correctamente

Scenario: HU-01.3 - Eliminar una serie
  Given que existe una serie registrada
  When el usuario la elimina
  Then la serie desaparece del catálogo
```

## EPIC 2: Búsqueda de Series

### HU-02: Búsqueda de Series

Como usuario
Quiero buscar una serie por su nombre
Para encontrarla rápidamente.

```gherkin
Scenario: HU-02.1 - Buscar una serie por nombre
  Given que existen series registradas
  When el usuario escribe el nombre de una serie
  Then el sistema muestra los resultados encontrados
```

# EPIC 3: Clasificación por Género
# HU-03: Clasificación por Género
# Objetivo: Organizar las series por categoría.
# Historia de Usuario:
# Como usuario
# Quiero filtrar las series por género
# Para encontrar contenido de mi interés.
Feature: HU-03 - Clasificación por Género

Scenario: HU-03.1 - Mostrar géneros disponibles
  Given que el usuario está en el catálogo de series
  When abre el filtro de géneros
  Then el sistema muestra los géneros disponibles

Scenario: HU-03.2 - Filtrar series por género
  Given que existen series de diferentes géneros
  When el usuario selecciona un género
  Then el sistema muestra únicamente las series de ese género


# EPIC 4: Calificaciones
# HU-04: Calificaciones
# Objetivo: Calificar las series.
# Historia de Usuario:
# Como usuario
# Quiero calificar una serie de 1 a 5 estrellas
# Para compartir mi opinión.
Feature: HU-04 - Calificaciones

Scenario: HU-04.1 - Registrar calificación
  Given que el usuario ha seleccionado una serie
  When asigna una calificación de 1 a 5 estrellas
  Then el sistema guarda la calificación correctamente

Scenario: HU-04.2 - Mostrar promedio
  Given que una serie tiene calificaciones registradas
  When el sistema calcula el promedio
  Then muestra el promedio actualizado de la serie


# EPIC 5: Favoritos
# HU-05: Favoritos
# Objetivo: Guardar series favoritas.
# Historia de Usuario:
# Como usuario
# Quiero guardar mis series favoritas
# Para acceder a ellas fácilmente.
Feature: HU-05 - Favoritos

Scenario: HU-05.1 - Agregar una serie a favoritos
  Given que el usuario ha iniciado sesión
  When selecciona la opción "Agregar a favoritos"
  Then la serie se agrega a la lista de favoritos

Scenario: HU-05.2 - Eliminar una serie de favoritos
  Given que la serie está en favoritos
  When el usuario selecciona "Eliminar de favoritos"
  Then la serie deja de aparecer en la lista

Scenario: HU-05.3 - Mostrar lista de favoritos
  Given que el usuario tiene series guardadas como favoritas
  When accede a su lista de favoritos
  Then el sistema muestra todas sus series favoritas


# EPIC 6: Registro de Usuario
# HU-06: Registro de Usuario
# Objetivo: Registrar nuevos usuarios en el sistema.
# Historia de Usuario:
# Como nuevo usuario
# Quiero registrarme con mis datos personales
# Para poder acceder al sistema de series de televisión.
Feature: HU-06 - Registro de Usuario

Scenario: HU-06.1 - Registro exitoso
  Given que el usuario se encuentra en la pantalla de registro
  When ingresa un nombre válido, un correo no registrado, una contraseña y la confirma correctamente
  Then el sistema crea la cuenta y muestra el mensaje "Registro exitoso"

Scenario: HU-06.2 - Correo ya registrado
  Given que el correo ya existe en el sistema
  When el usuario intenta registrarse con ese correo
  Then el sistema muestra el mensaje "El correo ya está registrado"

Scenario: HU-06.3 - Contraseñas diferentes
  Given que el usuario está llenando el formulario de registro
  When la contraseña y la confirmación no coinciden
  Then el sistema muestra el mensaje "Las contraseñas no coinciden"


# EPIC 7: Inicio de Sesión
# HU-07: Inicio de Sesión
# Objetivo: Autenticar usuarios registrados.
# Historia de Usuario:
# Como usuario registrado
# Quiero iniciar sesión con mi correo y contraseña
# Para acceder a mi cuenta.
Feature: HU-07 - Inicio de Sesión

Scenario: HU-07.1 - Inicio de sesión exitoso
  Given que el usuario tiene una cuenta registrada
  When ingresa un correo y una contraseña correctos
  Then el sistema permite el acceso a la aplicación

Scenario: HU-07.2 - Contraseña incorrecta
  Given que el usuario está registrado
  When ingresa una contraseña incorrecta
  Then el sistema muestra el mensaje "Correo o contraseña incorrectos"

Scenario: HU-07.3 - Campos vacíos
  Given que el usuario se encuentra en la pantalla de inicio de sesión
  When intenta iniciar sesión sin completar todos los campos
  Then el sistema solicita completar la información requerida
```

