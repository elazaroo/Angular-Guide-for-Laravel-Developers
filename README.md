# 📘 Guía Angular para Desarrolladores Laravel

## 🔄 Comparativa Rápida: Laravel vs Angular

| Laravel (Backend) | Angular (Frontend) |
|-------------------|-------------------|
| `php artisan serve` | `npm run start` |
| Blade templates (`.blade.php`) | Templates Angular (`.html`) |
| Controladores | Componentes |
| `{{ $variable }}` | `{{ variable }}` |
| `@if`, `@foreach` | `*ngIf`, `*ngFor` |
| Modelos Eloquent | Interfaces TypeScript |
| `composer.json` | `package.json` |
| `vendor/` | `node_modules/` |

---

## 🚀 Crear un Proyecto Angular

### En Laravel:
```bash
composer create-project laravel/laravel mi-proyecto
```

### En Angular:
```bash
npx @angular/cli new mi-proyecto
# o si tienes Angular CLI instalado globalmente:
ng new mi-proyecto
```

---

## 📁 Estructura del Proyecto

### Laravel tendría:
```
app/
├── Http/Controllers/    # Lógica
├── Models/              # Modelos de datos
resources/
├── views/               # Vistas Blade
public/
├── css/
├── js/
```

### Angular tiene:
```
src/
├── app/
│   ├── models/          # Interfaces (como Modelos)
│   ├── app.ts           # Componente principal (como un Controller)
│   ├── app.html         # Template (como una vista Blade)
│   └── app.css          # Estilos del componente
├── index.html           # Punto de entrada
└── styles.css           # Estilos globales
```

---

## 🧩 ¿Qué es un Componente?

**En Laravel** tienes Controladores + Vistas Blade.
**En Angular** tienes **Componentes** = Lógica + Vista + Estilos, todo junto.

```
┌─────────────────────────────────┐
│         COMPONENTE              │
├─────────────────────────────────┤
│  app.ts     → Lógica (TS)       │  ← Como un Controller
│  app.html   → Vista (HTML)      │  ← Como una vista Blade
│  app.css    → Estilos (CSS)     │  ← Estilos específicos
└─────────────────────────────────┘
```

---

## 📝 Sintaxis: Blade vs Angular Templates

### Variables

**Blade (Laravel):**
```blade
<p>Hola {{ $nombre }}</p>
```

**Angular:**
```html
<p>Hola {{ nombre }}</p>
```
> ¡Casi igual! Solo que en Angular no usamos `$`.

---

### Condicionales

**Blade (Laravel):**
```blade
@if($mostrar)
    <p>Visible</p>
@endif
```

**Angular:**
```html
<p *ngIf="mostrar">Visible</p>
```
> El `*ngIf` se pone como atributo del elemento.

---

### Bucles

**Blade (Laravel):**
```blade
@foreach($usuarios as $usuario)
    <li>{{ $usuario->nombre }}</li>
@endforeach
```

**Angular:**
```html
<li *ngFor="let usuario of usuarios">{{ usuario.nombre }}</li>
```

---

### Formularios (Two-Way Binding)

**Blade + JS (Laravel):**
```blade
<input type="text" id="nombre" value="{{ old('nombre') }}">
<script>
    document.getElementById('nombre').addEventListener('input', function(e) {
        // Actualizar variable manualmente
    });
</script>
```

**Angular (automático):**
```html
<input type="text" [(ngModel)]="nombre">
```
> `[(ngModel)]` sincroniza automáticamente el input con la variable.
> ¡Sin necesidad de JavaScript adicional!

---

### Eventos (Click)

**Blade + JS:**
```blade
<button onclick="enviarDatos()">Enviar</button>
<script>
    function enviarDatos() {
        // lógica
    }
</script>
```

**Angular:**
```html
<button (click)="enviarDatos()">Enviar</button>
```
```typescript
// En el componente .ts
enviarDatos() {
    // lógica
}
```

---

### Deshabilitar Elementos

**Blade + JS:**
```blade
<button id="btn" disabled>Enviar</button>
<script>
    if (formularioValido) {
        document.getElementById('btn').removeAttribute('disabled');
    }
</script>
```

**Angular (reactivo):**
```html
<button [disabled]="!formularioValido">Enviar</button>
```
> Se actualiza automáticamente cuando cambia `formularioValido`.

---

## 📦 Modelos: Eloquent vs Interfaces TypeScript

### En Laravel usas Modelos Eloquent:
```php
// app/Models/Configuracion.php
class Configuracion extends Model {
    protected $fillable = ['nombre', 'apellido', 'rango', 'intentos'];
}
```

### En Angular usas Interfaces TypeScript:
```typescript
// src/app/models/configuracion.ts
export interface Configuracion {
    nombre: string;
    apellido: string;
    rangoMaximo: number;
    intentos: number;
}
```

> La diferencia: Eloquent conecta con la BD. Las interfaces de Angular solo definen la "forma" de los datos en el frontend.

---

## ⚡ Getters: Propiedades Calculadas

### En Laravel (Modelo):
```php
class Usuario extends Model {
    public function getNombreCompletoAttribute() {
        return $this->nombre . ' ' . $this->apellido;
    }
}
// Uso: $usuario->nombre_completo
```

### En Angular (Componente):
```typescript
export class App {
    nombre = 'Juan';
    apellido = 'García';
    
    get nombreCompleto(): string {
        return this.nombre + ' ' + this.apellido;
    }
}
```
```html
<!-- Uso en template -->
<p>{{ nombreCompleto }}</p>
```

---

## 🔧 Comandos Útiles

| Acción | Laravel | Angular |
|--------|---------|---------|
| Iniciar servidor | `php artisan serve` | `npm run start` |
| Instalar dependencias | `composer install` | `npm install` |
| Crear proyecto | `composer create-project laravel/laravel` | `ng new` |
| Generar componente | `php artisan make:controller` | `ng generate component` |

---

## 💡 Tips Finales

1. **Angular es SPA**: No se recarga la página, todo se actualiza dinámicamente (a diferencia de Laravel donde cada ruta recarga).

2. **TypeScript**: Es JavaScript con tipos. Si defines `nombre: string`, TypeScript te avisa si intentas asignar un número.

3. **Reactividad automática**: Cuando cambias una variable, la vista se actualiza sola. No necesitas manipular el DOM.

4. **Componentes reutilizables**: Puedes crear componentes pequeños (como un botón o un formulario) y usarlos en múltiples lugares.

