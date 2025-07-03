Aquí tienes un reto al estilo HackerRank, pero enfocado a AngularJS (1.x).

---

### Desafío: Directorio de Usuarios con Filtro y Paginación

**Descripción**
Crea una pequeña aplicación en AngularJS que consuma un API de usuarios y muestre la lista en una tabla con las siguientes funcionalidades:

1. **Listado de usuarios**: Mostrar nombre, correo y rol.
2. **Búsqueda en tiempo real**: Filtrar por nombre o correo.
3. **Paginación**: Mostrar 5 usuarios por página, con controles “Anterior” y “Siguiente”.
4. **Ordenamiento**: Permitir ordenar asc/desc por nombre y correo al hacer clic en el encabezado de la columna.
5. **Indicador de carga**: Mostrar un spinner mientras se cargan los datos.

**Tecnologías**

* AngularJS 1.x (módulo, controlador, servicio, directiva si gustas).
* HTML + CSS minimalista (puedes usar Bootstrap o incluso puro CSS).

---

#### 1. Estructura de archivos sugerida

```
/index.html
/app.js
/services/userService.js
/controllers/userCtrl.js
/directives/spinnerDirective.js   (opcional)
```

---

#### 2. API de prueba

Simula o consume esta URL (puedes usar `$http.get` o `$http.jsonp`):

```
GET https://jsonplaceholder.typicode.com/users
```

Respuesta (ejemplo abreviado):

```json
[
  {
    "id": 1,
    "name": "Leanne Graham",
    "email": "Sincere@april.biz",
    "username": "Bret"
  },
  {
    "id": 2,
    "name": "Ervin Howell",
    "email": "Shanna@melissa.tv",
    "username": "Antonette"
  },
  …
]
```

Trata `username` como “rol” en la tabla.

---

#### 3. Requisitos Funcionales

1. **Carga inicial**:

   * Al iniciar, la app muestra el spinner.
   * Luego hace la petición al API y oculta el spinner.

2. **Tabla de usuarios**:

   * Columnas: Nombre, Correo, Rol.
   * Cada encabezado es clickeable para alternar orden asc/desc.

3. **Búsqueda**:

   * Un input de texto que filtra instantáneamente la lista (por nombre o correo).

4. **Paginación**:

   * Mostrar 5 registros por página.
   * Botones “Anterior”/“Siguiente” deshabilitados al llegar al límite.

---

#### 4. Criterios de Corrección

* **Funcionalidad completa**: todas las características solicitadas funcionan.
* **Código organizado**: uso de módulos, servicios y controladores.
* **Buen manejo de estados**: spinner y paginación sin recargar la página.
* **Legibilidad**: nombres claros, separación de lógica en el servicio para el API.

---

#### 5. Ejemplo de uso

1. El usuario abre la página y ve el spinner.
2. Carga la lista de 10 usuarios.
3. Al escribir “Leanne” en el filtro, sólo aparece “Leanne Graham”.
4. Hace clic en “Correo” y la lista se ordena por dirección de email.
5. Con más de 5 usuarios, navega a la página 2 con “Siguiente”.

---

¡Listo! Empieza creando tu módulo y controlador en `app.js`, luego el servicio para el API, y finalmente tu vista en `index.html`. Cuando termines, comparte tu código y lo revisamos juntos.
