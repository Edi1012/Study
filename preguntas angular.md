¡Por supuesto! A continuación te presento las **respuestas a todas las preguntas teóricas de Angular**, organizadas por nivel:

---

## 🔹 Nivel Básico

### 1. ¿Qué es Angular y para qué se utiliza?

Angular es un framework de desarrollo de aplicaciones web frontend creado por Google. Se utiliza para construir aplicaciones web dinámicas, escalables y de una sola página (SPA).

### 2. ¿Cuál es la diferencia entre AngularJS y Angular (2+)?

AngularJS (1.x) usa JavaScript y un enfoque basado en controladores, mientras que Angular 2+ usa TypeScript y está basado en componentes. Angular 2+ es más rápido, modular y adecuado para aplicaciones grandes.

### 3. ¿Qué es un componente en Angular?

Un componente es una clase TypeScript con un decorador `@Component` que define una parte de la interfaz de usuario. Cada componente tiene una plantilla HTML, un archivo de estilos y una clase que maneja la lógica.

### 4. ¿Qué es un módulo en Angular?

Un módulo es una agrupación de componentes, directivas, pipes y servicios relacionados. Angular utiliza módulos (`@NgModule`) para organizar y cargar partes de la aplicación.

### 5. ¿Qué es el `NgModule` y cuál es su propósito?

`NgModule` es un decorador que convierte una clase en un módulo de Angular. Define metadatos como componentes, servicios y otros módulos que se usan en la aplicación.

### 6. ¿Qué es el `ngIf`, `ngFor`, y cómo se utilizan?

* `*ngIf`: muestra u oculta elementos basado en una condición booleana.
* `*ngFor`: itera sobre listas para renderizar múltiples elementos.

```html
<div *ngIf="user.isLoggedIn">Bienvenido</div>
<li *ngFor="let item of items">{{ item }}</li>
```

### 7. ¿Qué es data binding en Angular y qué tipos existen?

Data binding es la forma en que Angular enlaza los datos entre la lógica y la vista. Tipos:

* Interpolación (`{{valor}}`)
* Property binding (`[src]="imagen"`)
* Event binding (`(click)="doSomething()"`)
* Two-way binding (`[(ngModel)]="dato"`)

### 8. ¿Qué es el two-way data binding? ¿Cómo se implementa?

Es una forma de vincular el modelo y la vista de forma bidireccional. Se usa con `[(ngModel)]`, que combina `[value]` y `(input)`.

```html
<input [(ngModel)]="nombre">
```

### 9. ¿Qué es un servicio en Angular?

Un servicio es una clase que contiene lógica de negocio o acceso a datos. Se utiliza para separar la lógica de los componentes.

### 10. ¿Qué es la inyección de dependencias (DI) en Angular?

Es un patrón en el que las dependencias (servicios, por ejemplo) se inyectan en las clases que las necesitan, en lugar de crearlas directamente. Angular lo hace automáticamente si declaras los servicios en los constructores.

---

## 🔹 Nivel Intermedio

### 1. ¿Qué es el ciclo de vida de un componente en Angular?

Son métodos que Angular ejecuta en momentos específicos del ciclo de vida del componente: `ngOnInit`, `ngOnChanges`, `ngOnDestroy`, etc. Permiten reaccionar a eventos como la creación o destrucción del componente.

### 2. ¿Qué son los decoradores en Angular?

Son funciones que se usan para añadir metadatos a clases:

* `@Component`: para componentes.
* `@Injectable`: para servicios.
* `@Input`: para recibir datos del padre.
* `@Output`: para emitir eventos al padre.

### 3. ¿Cuál es la diferencia entre `@Input()` y `@Output()`?

* `@Input()`: permite recibir datos desde el componente padre.
* `@Output()`: permite emitir eventos al padre.

### 4. ¿Qué es un observable? ¿Cómo se usa en Angular?

Un `Observable` es una colección de valores futuros (asincrónicos). Angular lo usa para manejar datos como peticiones HTTP, eventos de usuario, etc.

```ts
this.servicio.getDatos().subscribe(datos => this.lista = datos);
```

### 5. ¿Cuál es la diferencia entre `subscribe()` y `async` pipe?

* `subscribe()`: se usa manualmente para recibir valores.
* `async`: gestiona la suscripción automáticamente en la plantilla.

```html
<ul>
  <li *ngFor="let item of datos$ | async">{{ item }}</li>
</ul>
```

### 6. ¿Qué es el `HttpClientModule` y cómo se utiliza?

Es un módulo que permite hacer peticiones HTTP. Se importa en el `AppModule` y se utiliza con el servicio `HttpClient`.

```ts
constructor(private http: HttpClient) {}
this.http.get('api/usuarios').subscribe();
```

### 7. ¿Qué son los pipes en Angular? ¿Cómo se crean pipes personalizados?

Un pipe transforma datos en la vista.

Ejemplo:

```html
{{ fecha | date:'short' }}
```

Para crear uno:

```ts
@Pipe({ name: 'miPipe' })
export class MiPipe implements PipeTransform {
  transform(valor: string): string {
    return valor.toUpperCase();
  }
}
```

### 8. ¿Cómo se maneja la navegación (routing) en Angular?

Angular usa `RouterModule` y rutas definidas como objetos.

```ts
const routes: Routes = [
  { path: 'home', component: HomeComponent }
];
```

### 9. ¿Qué es lazy loading y cómo se implementa en Angular?

Lazy loading permite cargar módulos bajo demanda para mejorar el rendimiento.

```ts
{ path: 'admin', loadChildren: () => import('./admin/admin.module').then(m => m.AdminModule) }
```

### 10. ¿Cómo manejar formularios en Angular?

Angular ofrece:

* **Template-driven**: más simple, declarativo.
* **Reactive forms**: más estructurado, ideal para formularios complejos.

---

## 🔹 Nivel Avanzado

### 1. ¿Qué son los guards (`CanActivate`, `CanDeactivate`, etc.) y cómo se usan?

Los guards controlan el acceso a rutas.

```ts
canActivate(): boolean {
  return this.authService.estaAutenticado();
}
```

### 2. ¿Qué es un interceptor en Angular?

Es una clase que intercepta las peticiones/respuestas HTTP, útil para añadir encabezados, logs o manejar errores.

```ts
intercept(req: HttpRequest<any>, next: HttpHandler): Observable<HttpEvent<any>> {
  const modificado = req.clone({ setHeaders: { Authorization: 'Bearer token' }});
  return next.handle(modificado);
}
```

### 3. ¿Cómo se implementa la seguridad en Angular?

* Protección de rutas con guards.
* Tokens JWT.
* Almacenamiento seguro (nunca en `localStorage` sin cifrar).
* Interceptores para añadir el token a cada petición.

### 4. ¿Cómo optimizar el rendimiento de una aplicación Angular?

* Lazy loading.
* ChangeDetectionStrategy `OnPush`.
* TrackBy en `*ngFor`.
* Minificación y AOT compilation.

### 5. ¿Qué son las directivas estructurales vs de atributo?

* **Estructurales**: alteran el DOM (`*ngIf`, `*ngFor`).
* **De atributo**: cambian el comportamiento o estilo (`[ngClass]`, `[ngStyle]`).

### 6. ¿Qué es el Change Detection Strategy?

Es el mecanismo que Angular usa para detectar y aplicar cambios. Dos estrategias:

* `Default`: verifica todo.
* `OnPush`: solo si cambian los inputs o se dispara manualmente.

### 7. ¿Cómo se usa el patrón Redux o NgRx en Angular?

NgRx es una implementación de Redux para Angular. Usa acciones, efectos y un store centralizado para manejar el estado global de la app.

### 8. ¿Cómo funciona el Angular Compiler (AOT vs JIT)?

* **AOT (Ahead-of-Time)**: compila en build time, más rápido en producción.
* **JIT (Just-in-Time)**: compila en tiempo de ejecución, útil en desarrollo.

### 9. ¿Qué es Zone.js y qué papel juega en Angular?

Zone.js parchea operaciones asincrónicas y notifica a Angular cuándo actualizar el DOM. Es esencial para el sistema de detección de cambios.

### 10. ¿Cómo manejar la internacionalización (i18n) en Angular?

Angular soporta i18n con herramientas como `@angular/localize`, archivos `.xlf`, y marcas en los templates (`i18n="..."`). Se compilan versiones diferentes del app según el idioma.

---

¿Te gustaría que prepare un **PDF con estas respuestas** o que practiquemos con un simulacro de entrevista?
