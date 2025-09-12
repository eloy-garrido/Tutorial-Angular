# Angular 20 - Primeros Pasos (Tutorial Estructurado)

## Introducción

Este tutorial te guiará paso a paso para crear tu primera aplicación con Angular 20, siguiendo una progresión lógica desde lo más básico hasta conceptos avanzados.

## 🎯 Objetivos

Al finalizar este tutorial, sabrás:
- ✅ Crear un proyecto Angular 20 desde cero
- ✅ Implementar un componente "Hola Mundo" simple
- ✅ Entender la estructura básica de componentes
- ✅ Crear un componente contador interactivo
- ✅ Implementar la versión avanzada con Signals de Angular 20

## 🆕 Novedades en Angular 20

### Nomenclatura Simplificada de Archivos
Angular 20 introduce una nomenclatura más simple y limpia:

| **Antes (Angular 19 y anteriores)** | **Ahora (Angular 20)** |
|-------------------------------------|------------------------|
| `app.component.ts` | `app.ts` |
| `app.component.html` | `app.html` |
| `app.component.css` | `app.css` |
| `contador.component.ts` | `contador.ts` |

### Signals con `readonly`
Todos los inputs y outputs con signals ahora requieren el modificador `readonly`:

```typescript
// ✅ Angular 20
readonly titulo = input('Valor por defecto');
readonly cambioValor = output<number>();

// ❌ Angular 19 y anteriores
titulo = input('Valor por defecto');
cambioValor = output<number>();
```

## Requisitos previos

### Node.js (versión 20.18+ requerida)

```bash
# Verificar versión actual
node --version

# Si necesitas actualizar, descarga desde nodejs.org
# Versión recomendada: Node.js 22.x LTS
```

### Angular CLI actualizado

```bash
# Instalar Angular CLI 20+
npm install -g @angular/cli@latest

# Verificar instalación
ng version
```

---

## Paso 1: Crear proyecto básico

### 1.1. Crear el proyecto

```bash
# Crear proyecto básico sin routing
ng new mi-primera-app

# Navegar al directorio
cd mi-primera-app

# Ejecutar la aplicación
ng serve
```

### 1.2. Verificar que funciona

Abre tu navegador en `http://localhost:4200` y deberías ver la página de bienvenida de Angular.

### 1.3. Estructura del proyecto generado

```
mi-primera-app/
├── src/
│   ├── app/
│   │   ├── app.ts              # Componente principal (Angular 20)
│   │   ├── app.html            # Template del componente
│   │   ├── app.css             # Estilos del componente
│   │   └── app.spec.ts         # Tests
│   ├── main.ts                 # Punto de entrada
│   ├── index.html             # HTML base
│   └── styles.css             # Estilos globales
├── angular.json               # Configuración del CLI
├── package.json              # Dependencias
└── tsconfig.json            # Configuración TypeScript
```

---

## Paso 2: Hola Mundo simple

### 2.1. Modificar el componente principal

Edita `src/app/app.ts`:

```typescript
import { Component } from '@angular/core';

@Component({
  selector: 'app-root',
  standalone: true,
  imports: [],
  templateUrl: './app.html',
  styleUrl: './app.css'
})
export class App {
  title = '¡Hola Mundo con Angular 20!';
  mensaje = 'Mi primera aplicación Angular';
  contador = 0;
  
  cambiarMensaje() {
    this.mensaje = this.mensaje === 'Mi primera aplicación Angular' 
      ? '¡Angular 20 es genial!' 
      : 'Mi primera aplicación Angular';
    this.contador++;
  }
}
```

### 2.2. Actualizar el template

Edita `src/app/app.html`:

```html
<div class="container">
  <header>
    <h1>{{ title }}</h1>
  </header>
  
  <main>
    <p class="mensaje">{{ mensaje }}</p>
    <p class="contador">Clicks: {{ contador }}</p>
    
    <button class="btn-primary" (click)="cambiarMensaje()">
      Cambiar mensaje
    </button>
  </main>
  
  <footer>
    <p>Desarrollado con ❤️ usando Angular 20</p>
  </footer>
</div>
```

### 2.3. Agregar estilos básicos

Edita `src/app/app.css`:

```css
.container {
  max-width: 800px;
  margin: 0 auto;
  padding: 20px;
  font-family: Arial, sans-serif;
}

header {
  text-align: center;
  background: #1976d2;
  color: white;
  padding: 20px;
  border-radius: 8px;
  margin-bottom: 20px;
}

main {
  text-align: center;
  padding: 20px;
}

.mensaje {
  font-size: 1.2rem;
  color: #1976d2;
  margin: 20px 0;
}

.contador {
  font-size: 1rem;
  color: #666;
  margin: 10px 0;
}

.btn-primary {
  background: #1976d2;
  color: white;
  border: none;
  padding: 12px 24px;
  border-radius: 4px;
  cursor: pointer;
  font-size: 16px;
}

.btn-primary:hover {
  background: #1565c0;
}

footer {
  text-align: center;
  margin-top: 40px;
  padding: 20px;
  background: #f0f0f0;
  border-radius: 8px;
}
```
Edita `src/main.server.ts`:

```typescript
import { bootstrapApplication } from '@angular/platform-browser';
import { App } from './app/app';
import { config } from './app/app.config.server';

export default (context?: any) => bootstrapApplication(App, config, context);
```

### 2.4. Probar la aplicación

Guarda los archivos y verifica que la aplicación se actualiza automáticamente en el navegador.
ng serve
o
npm start

Si todo funciona bien, toca hacer commit y push a tu repositorio.


---

## Paso 3: Explicar componentes

### 3.1. ¿Qué son los componentes?

Los componentes son las **piezas fundamentales** de Angular. Cada componente tiene:

- **Template (HTML)**: La estructura visual
- **Estilos (CSS)**: La apariencia
- **Lógica (TypeScript)**: El comportamiento y datos
- **Metadatos**: Configuración del componente

### 3.2. Anatomía de un componente

```typescript
@Component({
  selector: 'app-mi-componente',    // Cómo se usa en HTML: <app-mi-componente>
  standalone: true,                 // Componente independiente (Angular 20)
  imports: [],                      // Otros componentes/módulos que necesita
  templateUrl: './mi-componente.html', // Archivo de template
  styleUrl: './mi-componente.css'   // Archivo de estilos
})
export class MiComponente {
  // Propiedades y métodos del componente
}
```

### 3.3. Ventajas de los componentes

1. **Reutilización**: Crear una vez, usar en muchos lugares
2. **Organización**: Dividir la aplicación en partes manejables
3. **Mantenimiento**: Cada componente tiene una responsabilidad específica
4. **Testeo**: Más fácil probar componentes individuales

---

## Paso 4: Crear componente contador

### 4.1. Generar el componente

```bash
# Crear componente contador
ng generate component contador

# O usando la forma corta:
ng g c contador
```

**Nota Angular 20**: El CLI ahora genera archivos con nomenclatura simplificada:
- `src/app/contador/contador.ts` (antes contador.component.ts)
- `src/app/contador/contador.html` (antes contador.component.html)
- `src/app/contador/contador.css` (antes contador.component.css)
- `src/app/contador/contador.spec.ts` (antes contador.component.spec.ts)

### 4.2. Implementar la lógica del contador

Edita `src/app/contador/contador.ts`:

```typescript
import { Component, Input, Output, EventEmitter } from '@angular/core';

@Component({
  selector: 'app-contador',
  standalone: true,
  imports: [],
  templateUrl: './contador.html',
  styleUrl: './contador.css'
})
export class ContadorComponent {
  @Input() titulo: string = 'Contador';
  @Input() valorInicial: number = 0;
  @Input() maximo: number = 10;
  
  @Output() cambioValor = new EventEmitter<number>();
  
  valor: number = 0;
  
  ngOnInit() {
    this.valor = this.valorInicial;
  }
  
  incrementar() {
    if (this.valor < this.maximo) {
      this.valor++;
      this.cambioValor.emit(this.valor);
    }
  }
  
  decrementar() {
    if (this.valor > 0) {
      this.valor--;
      this.cambioValor.emit(this.valor);
    }
  }
  
  reiniciar() {
    this.valor = this.valorInicial;
    this.cambioValor.emit(this.valor);
  }
}
```

### 4.3. Crear el template del contador

Edita `src/app/contador/contador.html`:

```html
<div class="contador-card">
  <h3>{{ titulo }}</h3>
  
  <div class="contador-display">
    <span class="valor">{{ valor }}</span>
    <span class="maximo">/ {{ maximo }}</span>
  </div>
  
  <div class="contador-botones">
    <button 
      class="btn btn-outline" 
      (click)="decrementar()"
      [disabled]="valor <= 0">
      -
    </button>
    
    <button 
      class="btn btn-primary" 
      (click)="incrementar()"
      [disabled]="valor >= maximo">
      +
    </button>
    
    <button 
      class="btn btn-secondary" 
      (click)="reiniciar()">
      Reset
    </button>
  </div>
</div>
```

### 4.4. Estilos del contador

Edita `src/app/contador/contador.css`:

```css
.contador-card {
  background: white;
  border: 2px solid #e0e0e0;
  border-radius: 8px;
  padding: 20px;
  text-align: center;
  margin: 10px;
  box-shadow: 0 2px 4px rgba(0,0,0,0.1);
}

.contador-card h3 {
  margin: 0 0 15px 0;
  color: #1976d2;
  font-size: 1.1rem;
}

.contador-display {
  margin: 20px 0;
}

.valor {
  font-size: 2rem;
  font-weight: bold;
  color: #1976d2;
}

.maximo {
  font-size: 1rem;
  color: #666;
  margin-left: 8px;
}

.contador-botones {
  display: flex;
  gap: 8px;
  justify-content: center;
}

.btn {
  min-width: 60px;
  padding: 8px 16px;
  font-size: 14px;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

.btn-primary {
  background: #1976d2;
  color: white;
}

.btn-secondary {
  background: #757575;
  color: white;
}

.btn-outline {
  background: transparent;
  color: #1976d2;
  border: 2px solid #1976d2;
}

.btn:disabled {
  opacity: 0.5;
  cursor: not-allowed;
}

.btn:not(:disabled):hover {
  opacity: 0.8;
}
```

### 4.5. Usar el componente en la aplicación principal

Edita `src/app/app.ts`:

```typescript
import { Component, signal } from '@angular/core';
import { ContadorComponent } from './contador/contador';

@Component({
  selector: 'app-root',
  imports: [ContadorComponent],
  templateUrl: './app.html',
  styleUrl: './app.css'
})
export class App {
  title = '¡Hola Mundo con Angular 20!';
  mensaje = 'Mi primera aplicación Angular';
  contador = 0;
  totalClicks = 0;

  cambiarMensaje() {
    this.mensaje = this.mensaje === 'Mi primera aplicación Angular' 
      ? '¡Angular 20 es genial!' 
      : 'Mi primera aplicación Angular';
    this.contador++;
  }
  onContadorCambio(nuevoValor: number) {
    this.totalClicks++;
    console.log('Contador cambió a:', nuevoValor);
  }
}
```

### 4.6. Actualizar el template principal

Edita `src/app/app.html`:

```html
<div class="container">
  <header>
    <h1>{{ title }}</h1>
    
  </header>
  
  <main>
    <p class="mensaje">{{ mensaje }}</p>
    <p>Total de interacciones: {{ totalClicks }}</p>
    <button class="btn-primary" (click)="cambiarMensaje()">
      Cambiar mensaje
    </button>
    <h2>🧩 Demo de Componentes</h2>
    
    <div class="componentes-grid">
      <!-- Componente 1: Contador Básico -->
      <app-contador 
        titulo="Contador Básico"
        [valorInicial]="0"
        [maximo]="5"
        (cambioValor)="onContadorCambio($event)">
      </app-contador>
      
      <!-- Componente 2: Contador Avanzado -->
      <app-contador 
        titulo="Contador Avanzado"
        [valorInicial]="3"
        [maximo]="15"
        (cambioValor)="onContadorCambio($event)">
      </app-contador>
    </div>
  
  <footer>
    <p>Desarrollado con ❤️ usando Angular 20</p>
  </footer>
```

### 4.7. Revisar avances, si esta todo bien, commit y push

---

## Paso 5: Versión avanzada con Signals

### 5.1. ¿Qué son los Signals?

Los **Signals** son una nueva característica de Angular que proporciona:

- **Reactividad automática**: Los cambios se propagan automáticamente
- **Mejor rendimiento**: Solo se actualizan las partes que cambiaron
- **Sintaxis más simple**: Menos código boilerplate
- **Detección de cambios optimizada**: Angular sabe exactamente qué cambió

### 5.2. Crear componente contador con Signals

```bash
# Crear nuevo componente con signals
ng g c contador-signals
```

### 5.3. Implementar contador con Signals

Edita `src/app/contador-signals/contador-signals.ts`:

```typescript
import { Component, signal, input, output, computed, effect } from '@angular/core';

@Component({
  selector: 'app-contador-signals',
  standalone: true,
  imports: [],
  templateUrl: './contador-signals.html',
  styleUrl: './contador-signals.css'
})
export class ContadorSignalsComponent {
  // Inputs usando signals (Angular 20 sintaxis correcta)
  readonly titulo = input('Contador con Signals');
  readonly valorInicial = input(0);
  readonly maximo = input(10);
  
  // Output usando signals (Angular 20 sintaxis correcta)
  readonly cambioValor = output<number>();
  
  // Estado interno con signals
  valor = signal(0);
  
  // Computed signals (se calculan automáticamente)
  porcentaje = computed(() => {
    return Math.round((this.valor() / this.maximo()) * 100);
  });
  
  estado = computed(() => {
    const porcentaje = this.porcentaje();
    if (porcentaje === 0) return 'Inicial';
    if (porcentaje < 50) return 'Bajo';
    if (porcentaje < 80) return 'Medio';
    if (porcentaje < 100) return 'Alto';
    return 'Máximo';
  });
  
  colorEstado = computed(() => {
    const estado = this.estado();
    switch (estado) {
      case 'Inicial': return '#666';
      case 'Bajo': return '#4caf50';
      case 'Medio': return '#ff9800';
      case 'Alto': return '#f44336';
      case 'Máximo': return '#9c27b0';
      default: return '#666';
    }
  });
  
  constructor() {
    // Effect: se ejecuta cuando cambian los signals
    effect(() => {
      console.log(`Contador ${this.titulo()}: ${this.valor()} (${this.estado()})`);
    });
    
    // Inicializar valor cuando cambie valorInicial
    effect(() => {
      this.valor.set(this.valorInicial());
    }, { allowSignalWrites: true });
  }
  
  incrementar() {
    if (this.valor() < this.maximo()) {
      this.valor.update(v => v + 1);
      this.cambioValor.emit(this.valor());
    }
  }
  
  decrementar() {
    if (this.valor() > 0) {
      this.valor.update(v => v - 1);
      this.cambioValor.emit(this.valor());
    }
  }
  
  reiniciar() {
    this.valor.set(this.valorInicial());
    this.cambioValor.emit(this.valor());
  }
}
```

### 5.4. Template del contador con Signals

Edita `src/app/contador-signals/contador-signals.html`:

```html
<div class="contador-card">
  <h3>{{ titulo() }}</h3>
  
  <div class="contador-display">
    <span class="valor">{{ valor() }}</span>
    <span class="maximo">/ {{ maximo() }}</span>
  </div>
  
  <div class="progreso">
    <div class="progreso-bar" [style.width.%]="porcentaje()"></div>
  </div>
  
  <div class="estado" [style.color]="colorEstado()">
    Estado: {{ estado() }} ({{ porcentaje() }}%)
  </div>
  
  <div class="contador-botones">
    <button 
      class="btn btn-outline" 
      (click)="decrementar()"
      [disabled]="valor() <= 0">
      -
    </button>
    
    <button 
      class="btn btn-primary" 
      (click)="incrementar()"
      [disabled]="valor() >= maximo()">
      +
    </button>
    
    <button 
      class="btn btn-secondary" 
      (click)="reiniciar()">
      Reset
    </button>
  </div>
</div>
```

### 5.5. Estilos del contador con Signals

Edita `src/app/contador-signals/contador-signals.css`:

```css
.contador-card {
  background: white;
  border: 2px solid #e0e0e0;
  border-radius: 8px;
  padding: 20px;
  text-align: center;
  margin: 10px;
  box-shadow: 0 2px 4px rgba(0,0,0,0.1);
}

.contador-card h3 {
  margin: 0 0 15px 0;
  color: #1976d2;
  font-size: 1.1rem;
}

.contador-display {
  margin: 20px 0;
}

.valor {
  font-size: 2rem;
  font-weight: bold;
  color: #1976d2;
}

.maximo {
  font-size: 1rem;
  color: #666;
  margin-left: 8px;
}

.progreso {
  width: 100%;
  height: 8px;
  background: #e0e0e0;
  border-radius: 4px;
  margin: 15px 0;
  overflow: hidden;
}

.progreso-bar {
  height: 100%;
  background: linear-gradient(90deg, #4caf50, #ff9800, #f44336);
  transition: width 0.3s ease;
}

.estado {
  font-weight: bold;
  margin: 10px 0;
  font-size: 0.9rem;
}

.contador-botones {
  display: flex;
  gap: 8px;
  justify-content: center;
  margin-top: 15px;
}

.btn {
  min-width: 60px;
  padding: 8px 16px;
  font-size: 14px;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  transition: all 0.2s ease;
}

.btn-primary {
  background: #1976d2;
  color: white;
}

.btn-secondary {
  background: #757575;
  color: white;
}

.btn-outline {
  background: transparent;
  color: #1976d2;
  border: 2px solid #1976d2;
}

.btn:disabled {
  opacity: 0.5;
  cursor: not-allowed;
}

.btn:not(:disabled):hover {
  transform: translateY(-1px);
  box-shadow: 0 2px 4px rgba(0,0,0,0.2);
}
```

### 5.6. Actualizar la aplicación principal para usar Signals

Edita `src/app/app.ts`:

```typescript
import { Component, signal, computed } from '@angular/core';
import { ContadorComponent } from './contador/contador';
import { ContadorSignalsComponent } from './contador-signals/contador-signals';

@Component({
  selector: 'app-root',
  standalone: true,
  imports: [ContadorComponent, ContadorSignalsComponent],
  templateUrl: './app.html',
  styleUrl: './app.css'
})
export class App {
  title = signal('¡Angular 20 con Signals!');
  mensaje = signal('Mi primera aplicación Angular');
  contador = signal(0);
  totalClicks = signal(0);
  
    cambiarMensaje() {
    this.mensaje = this.mensaje === 'Mi primera aplicación Angular' 
      ? '¡Angular 20 es genial!' 
      : 'Mi primera aplicación Angular';
    this.contador++;
  }
  // Computed signal para estadísticas
  estadisticas = computed(() => {
    const clicks = this.totalClicks();
    if (clicks === 0) return 'Sin interacciones';
    if (clicks < 10) return 'Explorando...';
    if (clicks < 25) return 'Aprendiendo...';
    if (clicks < 50) return 'Progresando...';
    return '¡Dominando Angular!';
  });
  
  onContadorCambio(nuevoValor: number) {
    this.totalClicks++;
    console.log('Contador cambió a:', nuevoValor);
  }
}
```

### 5.7. Template final con ambos tipos de contadores

Edita `src/app/app.html`:

```html
<div class="container">
  <header>
    <h1>{{ title() }}</h1>
    <p class="estadisticas">{{ estadisticas() }} - Total: {{ totalClicks() }} interacciones</p>
  </header>
  
  <main>
    <section class="seccion">
      <h2>🧩 Componentes Tradicionales</h2>
      <div class="componentes-grid">
        <app-contador 
          titulo="Contador Básico"
          [valorInicial]="0"
          [maximo]="5"
          (cambioValor)="onContadorCambio($event)">
        </app-contador>
        
        <app-contador 
          titulo="Contador Avanzado"
          [valorInicial]="2"
          [maximo]="8"
          (cambioValor)="onContadorCambio($event)">
        </app-contador>
      </div>
    </section>
    
    <section class="seccion">
      <h2>⚡ Componentes con Signals</h2>
      <div class="componentes-grid">
        <!-- Sintaxis correcta para Angular 20 con signals -->
        <app-contador-signals 
          titulo="Contador con Signals"
          [valorInicial]="0"
          [maximo]="10"
          (cambioValor)="onContadorCambio($event)">
        </app-contador-signals>
        
        <app-contador-signals 
          titulo="Contador Avanzado"
          [valorInicial]="5"
          [maximo]="20"
          (cambioValor)="onContadorCambio($event)">
        </app-contador-signals>
      </div>
    </section>
    
    <div class="comparacion">
      <h3>🎯 Diferencias entre Componentes Tradicionales y Signals</h3>
      <div class="comparacion-grid">
        <div class="comparacion-item">
          <h4>Componentes Tradicionales</h4>
          <ul>
            <li><code>@Input()</code> y <code>@Output()</code></li>
            <li>Detección de cambios manual</li>
            <li><code>ngOnInit</code> para inicialización</li>
            <li>Más código boilerplate</li>
            <li>Property binding: <code>[propiedad]="valor"</code></li>
          </ul>
        </div>
        <div class="comparacion-item">
          <h4>Componentes con Signals (Angular 20)</h4>
          <ul>
            <li><code>readonly input()</code> y <code>readonly output()</code></li>
            <li>Reactividad automática</li>
            <li><code>computed()</code> para valores derivados</li>
            <li><code>effect()</code> para efectos secundarios</li>
            <li>Mejor rendimiento</li>
            <li>String inputs: <code>propiedad="valor"</code></li>
            <li>Numeric inputs: <code>[propiedad]="numero"</code></li>
          </ul>
        </div>
      </div>
      
      <div class="sintaxis-angular20">
        <h4>📝 Sintaxis clave de Angular 20</h4>
        <div class="sintaxis-ejemplos">
          <div class="ejemplo">
            <h5>Declaración de Inputs/Outputs:</h5>
            <pre><code>// ✅ Correcto en Angular 20
readonly titulo = input('Valor por defecto');
readonly cambioValor = output&lt;number&gt;();

// ❌ Incorrecto (Angular 19 y anteriores)
titulo = input('Valor por defecto');
cambioValor = output&lt;number&gt;();</code></pre>
          </div>
          <div class="ejemplo">
            <h5>Uso en Templates:</h5>
            <pre><code>&lt;!-- ✅ String inputs (sin corchetes) --&gt;
&lt;app-contador titulo="Mi Contador"&gt;&lt;/app-contador&gt;

&lt;!-- ✅ Numeric/Boolean inputs (con corchetes) --&gt;
&lt;app-contador [valorInicial]="5" [maximo]="10"&gt;&lt;/app-contador&gt;</code></pre>
          </div>
        </div>
      </div>
    </div>
  </main>
  
  <footer>
    <p>Desarrollado con ❤️ usando Angular 20 y Signals</p>
  </footer>
</div>
```

### 5.8. Estilos finales

Actualiza `src/app/app.css`:

```css
.container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 20px;
  font-family: Arial, sans-serif;
}

header {
  text-align: center;
  background: linear-gradient(135deg, #1976d2, #42a5f5);
  color: white;
  padding: 30px;
  border-radius: 12px;
  margin-bottom: 30px;
  box-shadow: 0 4px 8px rgba(0,0,0,0.1);
}

header h1 {
  margin: 0 0 10px 0;
  font-size: 2.5rem;
}

.estadisticas {
  font-size: 1.1rem;
  margin: 10px 0 0 0;
  opacity: 0.9;
}

.seccion {
  margin: 40px 0;
}

.seccion h2 {
  color: #1976d2;
  border-bottom: 2px solid #e0e0e0;
  padding-bottom: 10px;
  margin-bottom: 20px;
}

.componentes-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(350px, 1fr));
  gap: 20px;
  margin: 20px 0;
}

.comparacion {
  background: #f8f9fa;
  padding: 30px;
  border-radius: 12px;
  margin: 40px 0;
}

.comparacion h3 {
  color: #1976d2;
  text-align: center;
  margin-bottom: 20px;
}

.comparacion-grid {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 30px;
}

.comparacion-item {
  background: white;
  padding: 20px;
  border-radius: 8px;
  box-shadow: 0 2px 4px rgba(0,0,0,0.1);
}

.comparacion-item h4 {
  color: #1976d2;
  margin-top: 0;
  margin-bottom: 15px;
}

.comparacion-item ul {
  margin: 0;
  padding-left: 20px;
}

.comparacion-item li {
  margin: 8px 0;
  line-height: 1.4;
}

footer {
  text-align: center;
  margin-top: 50px;
  padding: 20px;
  background: #f0f0f0;
  border-radius: 8px;
}

@media (max-width: 768px) {
  .comparacion-grid {
    grid-template-columns: 1fr;
  }
  
  .componentes-grid {
    grid-template-columns: 1fr;
  }
  
  header h1 {
    font-size: 2rem;
  }
}
```

---

Hacer commit y terminamos

## 🎉 Conclusión

¡Felicidades! Has completado tu primer tutorial de Angular 20. Has aprendido:

### ✅ Lo que lograste:
- **Proyecto básico**: Creaste una aplicación Angular 20 desde cero
- **Hola Mundo**: Implementaste tu primer componente personalizado
- **Componentes tradicionales**: Creaste un contador con @Input() y @Output()
- **Signals avanzados**: Implementaste la nueva API de signals con reactividad automática
- **Nomenclatura Angular 20**: Usaste la nueva sintaxis simplificada de archivos
- **Comparación práctica**: Viste las diferencias entre ambos enfoques

### 🆕 Características clave de Angular 20 que usaste:
- **Nomenclatura simplificada**: `app.ts` en lugar de `app.component.ts`
- **Signals con `readonly`**: Sintaxis más estricta y segura
- **Componentes standalone**: Sin necesidad de módulos
- **Templates externos**: Separación clara de responsabilidades

### 🚀 Próximos pasos:
- Explora más sobre **Signals** y **computed()**
- Aprende sobre **routing** en Angular 20
- Investiga **formularios reactivos** con signals
- Practica con **servicios** y **dependency injection**
- Experimenta con **animaciones** y **directivas**

### 📚 Recursos adicionales:
- [Documentación oficial de Angular 20](https://angular.dev)
- [Guía de Signals](https://angular.dev/guide/signals)
- [Angular CLI Reference](https://angular.dev/cli)
- [Migración a Angular 20](https://angular.dev/update-guide)

¡Sigue practicando y construyendo aplicaciones increíbles con Angular 20! 🎯