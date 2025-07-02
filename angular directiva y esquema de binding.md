Aquí tienes cada directiva y esquema de binding con una breve explicación y un ejemplo mínimo. Todo funciona igual en Angular 2+ hasta la última versión.

---

## 🔨 Directivas estructurales

### `*ngIf`

Muestra u oculta un bloque de DOM según una condición booleana.

```html
<!-- en el componente: mostrar = true/false -->
<div *ngIf="mostrar">
  Este bloque aparece solo si mostrar === true
</div>
```

---

### `*ngFor`

Itera sobre una colección, creando un elemento por cada ítem.

```html
<ul>
  <li *ngFor="let fruta of frutas; index as i">
    {{ i + 1 }}. {{ fruta }}
  </li>
</ul>
<!-- frutas = ['Manzana','Pera','Uva'] -->
```

---

### `*ngSwitch` / `*ngSwitchCase` / `*ngSwitchDefault`

Selecciona entre varios bloques según el valor de una expresión.

```html
<div [ngSwitch]="color">
  <p *ngSwitchCase="'rojo'">¡Es rojo!</p>
  <p *ngSwitchCase="'verde'">¡Es verde!</p>
  <p *ngSwitchDefault>Otro color</p>
</div>
<!-- color = 'verde' -->
```

---

### `*ngTemplateOutlet`

Inserta un `<ng-template>` en tiempo de ejecución, pudiendo pasarle contexto.

```html
<ng-template #plantilla let-nom="nombre">
  Hola, {{ nom }}!
</ng-template>

<ng-container
  *ngTemplateOutlet="plantilla; context: { nombre: 'Ana' }">
</ng-container>
```

---

### `<ng-container>`

Contenedor lógico sin tag extra en el DOM, ideal para agrupar directivas.

```html
<ng-container *ngIf="usuario">
  <p>Bienvenido, {{ usuario.nombre }}</p>
</ng-container>
```

---

## 🎨 Directivas de atributo

### `ngClass`

Aplica clases condicionalmente.

```html
<div [ngClass]="{ 'resaltado': esActivo }">
  Texto que puede resaltarse
</div>
<!-- CSS: .resaltado { background: yellow } -->
```

---

### `ngStyle`

Aplica estilos en línea dinámicamente.

```html
<div
  [ngStyle]="{
    'font-size.px': tamañoFuente,
    color: colorTexto
  }">
  Texto con estilo dinámico
</div>
```

---

### Bindings directos de clases y estilos

```html
<p
  [class.destacado]="isFocus"
  [style.border.px]="grosorBorde">
  Ejemplo sin ngClass/ngStyle
</p>
```

---

### `ngComponentOutlet`

Renderiza un componente de forma dinámica (requiere import de `CommonModule`).

```html
<ng-container
  *ngComponentOutlet="componenteADesplegar">
</ng-container>
```

```ts
// en el componente padre:
componenteADesplegar = MiComponenteDinámico;
```

---

## 📝 Formularios

### **Template-driven** (FormsModule)

```html
<form #f="ngForm" (ngSubmit)="onSubmit(f.value)">
  <input
    name="email"
    [(ngModel)]="email"
    required
    email>
  <button [disabled]="f.invalid">Enviar</button>
</form>
```

```ts
// en el componente:
email: string = '';
onSubmit(datos: any) {
  console.log(datos.email);
}
```

---

### **Reactivas** (ReactiveFormsModule)

```ts
// en el componente:
formulario = new FormGroup({
  usuario: new FormControl('', Validators.required),
  edad:    new FormControl(0, [
              Validators.min(0),
              Validators.max(120)
            ])
});
```

```html
<form [formGroup]="formulario" (ngSubmit)="salvar()">
  <input formControlName="usuario" placeholder="Usuario">
  <input formControlName="edad" type="number" placeholder="Edad">
  <button [disabled]="formulario.invalid">Guardar</button>
</form>
```

---

## ⚡ Binding de eventos

### 1. Eventos de ratón

```html
<button (click)="onClick()">Haz clic</button>
<div (mouseenter)="onEnter()" (mouseleave)="onLeave()">
  Zona sensible al ratón
</div>
```

---

### 2. Eventos de teclado (con filtros)

```html
<input
  (keydown.enter)="onEnter()"
  (keyup.ArrowUp)="onArrowUp()">
```

---

### 3. Eventos de formulario

```html
<input
  (input)="onInput($event.target.value)"
  (change)="onChange($event)">
```

---

### 4. Eventos táctiles

```html
<div
  (touchstart)="onTouchStart()"
  (touchend)="onTouchEnd()">
  Área táctil
</div>
```

---

### 5. Eventos de ventana con `@HostListener`

```ts
@Component({/*...*/})
export class MiComponente {
  @HostListener('window:resize', ['$event'])
  onResize(evt: UIEvent) {
    console.log('Nuevo tamaño:', window.innerWidth);
  }
}
```

---

## 🔄 Salidas de componentes y animaciones

### `@Output()` personalizado

```ts
// componente hijo
@Component({ selector: 'app-hijo', template: `<button (click)="emitir()">OK</button>` })
export class HijoComponent {
  @Output() confirmado = new EventEmitter<void>();
  emitir() { this.confirmado.emit(); }
}
```

```html
<!-- componente padre -->
<app-hijo (confirmado)="alConfirmar()"></app-hijo>
```

---

### Eventos de animación

```ts
// en el componente
@Component({
  /* ... */,
  animations: [
    trigger('fadeIn', [
      transition(':enter', [
        style({ opacity: 0 }),
        animate('300ms ease-in', style({ opacity: 1 }))
      ])
    ])
  ]
})
export class MiComponente { 
  onAnimDone(evt: AnimationEvent) {
    console.log('Animación terminada', evt);
  }
}
```

```html
<div
  *ngIf="mostrar"
  [@fadeIn]
  (@fadeIn.done)="onAnimDone($event)">
  Aparezco con fade-in
</div>
```

---
