# Investigación: Web Components, HTML Templates y Frameworks

## Parte 1. Web Components

### 1. ¿Qué problema resuelven los Web Components y qué aporta cada tecnología: Custom Elements, Shadow DOM y HTML Templates?
Resuelven la falta de un sistema nativo en la web para crear componentes reutilizables y encapsulados sin depender de librerías externas ni sufrir conflictos de estilos o scripts globales. **Custom Elements** permite definir etiquetas HTML propias con comportamiento y ciclo de vida en JavaScript; **Shadow DOM** aísla el árbol DOM y el CSS interno del componente para que no afecten ni sean afectados por el resto de la página; y **HTML Templates** (`<template>`) permite declarar fragmentos de marcado inerte que se clonan rápidamente cuando se necesitan.

### 2. ¿En qué se diferencia un `<template>` de un `<div>` oculto con `display: none`?
Aunque ninguno es visible en pantalla, un `<div>` con `display: none` sigue formando parte activa del DOM: el navegador descarga sus imágenes, ejecuta sus scripts y `document.querySelector` puede encontrar sus elementos hijos directamente. En cambio, el contenido de un `<template>` permanece inerte en un `DocumentFragment` separado; no renderiza nada, no carga recursos multimedia ni ejecuta código hasta que se clona e inserta explícitamente mediante JavaScript, siendo invisible para `document.querySelector` normal.

### 3. ¿Qué cambia entre el Shadow DOM en modo `"open"` y en modo `"closed"`?
La diferencia radica en el nivel de acceso desde el JavaScript externo hacia el árbol interno del componente. Cuando se crea con `attachShadow({ mode: 'open' })`, cualquier script de la página puede inspeccionar y manipular su contenido accediendo a la propiedad `elemento.shadowRoot`. Por el contrario, con `mode: 'closed'`, `elemento.shadowRoot` devuelve `null` hacia el exterior, restringiendo la manipulación interna únicamente a las referencias privadas guardadas dentro de la propia clase del componente.

### 4. ¿Qué es un `<slot>` y para qué sirve en un componente reutilizable?
Un `<slot>` es un marcador de posición dentro del Shadow DOM que actúa como punto de proyección para el contenido HTML que el usuario escribe entre las etiquetas de apertura y cierre del componente personalizado. Sirve para hacer componentes flexibles y dinámicos, permitiendo inyectar texto, etiquetas o estructuras variables desde el exterior sin romper el encapsulamiento de estilos ni modificar la plantilla base del componente.

### 5. ¿Qué navegadores soportan hoy los Web Components?
Hoy en día, las especificaciones principales de Web Components (Custom Elements v1, Shadow DOM v1 y `<template>`) cuentan con soporte nativo y completo en todos los navegadores modernos de escritorio y móviles: Google Chrome, Mozilla Firefox, Apple Safari, Microsoft Edge y Opera. Según la plataforma **Can I use** (consultado el 17 de noviembre de 2026), el soporte global supera el 97% de los usuarios activos en internet sin necesidad de polyfills.

---

## Parte 2. Frameworks, librerías y Node.js

### 1. Diferencia entre estándar del navegador, librería, framework y entorno de ejecución
- **Estándar del navegador:** Especificación oficial soportada de forma nativa por los navegadores sin descargas externas. *Ejemplo:* Shadow DOM o `<template>`, que funcionan directamente en Chrome o Firefox.
- **Librería:** Conjunto de funciones o utilidades que el desarrollador invoca bajo su propio control para resolver una tarea específica. *Ejemplo:* React, que se encarga principalmente de renderizar interfaces de usuario y manejar su estado.
- **Framework:** Marco de trabajo integral que impone una arquitectura, reglas y flujo de ejecución (*inversión de control*), llamando él al código del programador. *Ejemplo:* Angular, que incluye enrutamiento, formularios, inyección de dependencias y compilación estructurada.
- **Entorno de ejecución (Runtime):** Plataforma que permite ejecutar código JavaScript fuera del navegador web, accediendo al sistema operativo, archivos o red. *Ejemplo:* Node.js, utilizado para crear servidores backend o ejecutar herramientas de desarrollo en consola.

### 2. Comparativa entre estándares y herramientas del ecosistema

| Criterio | Web Components nativos | React | Vue | Angular |
| :--- | :--- | :--- | :--- | :--- |
| **Tipo** | Estándar nativo del navegador (W3C / WHATWG). | Librería enfocada en la capa de interfaz de usuario (UI). | Framework progresivo para construir interfaces y SPAs. | Framework completo y robusto (*opinionated*). |
| **Cómo se crea un componente** | Mediante una clase ES6 que hereda de `HTMLElement` y se registra con `customElements.define()`. | Mediante funciones (o clases) en JavaScript/TypeScript que retornan sintaxis JSX. | Usando archivos de un solo componente (`.vue`) que separan `<template>`, `<script>` y `<style>`. | Mediante clases TypeScript decoradas con `@Component` vinculadas a una plantilla HTML y hoja de estilos. |
| **Necesita instalar herramientas (npm)** | No; funcionan directamente en el navegador con HTML, CSS y JS puros. | Sí, en entornos reales se usa `npm` para instalar React, Vite/Next.js y empaquetadores. | Opcional para pruebas básicas por CDN, pero necesario con `npm` para proyectos estructurados. | Sí, requiere obligatoriamente `npm` y Angular CLI para compilar TypeScript y gestionar módulos. |
| **Ventajas principales** | Cero dependencias, interoperabilidad total entre frameworks y longevidad garantizada por el navegador. | Ecosistema gigante, gran comunidad, Virtual DOM eficiente y alta demanda laboral. | Curva de aprendizaje suave, excelente documentación y reactividad intuitiva sin mucha configuración. | Arquitectura estandarizada lista para empresas grandes, TypeScript nativo y herramientas integradas. |
| **Desventajas principales** | Código más verboso (*boilerplate*), falta de enlace de datos reactivo nativo y manejo manual del DOM. | No incluye enrutamiento ni gestión de estado global oficial; exige elegir librerías de terceros. | Menor cuota de mercado empresarial frente a React o Angular en proyectos corporativos masivos. | Curva de aprendizaje pronunciada, mayor peso inicial y estructura rígida para proyectos pequeños. |

### 3. Node.js, npm y arquitectura en una tienda en línea
**Node.js** es un entorno de ejecución de JavaScript del lado del servidor construido sobre el motor V8 de Chrome. Se utiliza para desarrollar APIs, microservicios, automatizar tareas y ejecutar herramientas de compilación local. Su gestor de paquetes, **npm** (*Node Package Manager*), es fundamental para React, Vue y Angular porque permite descargar, versionar y administrar sus dependencias, además de ejecutar scripts de empaquetado (*bundling*) y transpilación de código moderno hacia JavaScript compatible con navegadores.

En una **tienda en línea** que usa React y Node.js:
- **React (Frontend):** Se ejecuta en el navegador del cliente; renderiza el catálogo de productos, gestiona los filtros, actualiza el carrito de compras de forma interactiva y envía las peticiones de pago.
- **Node.js (Backend):** Se ejecuta en el servidor; recibe las peticiones de React, valida sesiones de usuario, consulta y actualiza el inventario en la base de datos y procesa de forma segura las transacciones con la pasarela de pagos.

### 4. Elección de herramienta por caso de uso

**a. Un botón de chat que varias empresas pegan en sus propias páginas:**
Usaría **Web Components nativos**. Como el widget se incrustará en sitios web externos construidos con distintas tecnologías (WordPress, React, Angular o HTML puro), un Web Component garantiza compatibilidad universal sin obligar a los clientes a instalar librerías pesadas. Además, el Shadow DOM protege los estilos del botón de chat para que el CSS de cada empresa no altere su diseño ni viceversa.

**b. Una aplicación web grande para un banco, con muchos equipos de desarrollo:**
Usaría **Angular**. En un entorno bancario con múltiples equipos trabajando en paralelo, la arquitectura estricta y estandarizada de Angular asegura que todos sigan las mismas convenciones de código, estructura de carpetas e inyección de dependencias. Su integración nativa con TypeScript reduce errores en tiempo de compilación y ofrece herramientas oficiales para pruebas, formularios complejos y seguridad sin depender de decisiones aisladas de cada equipo.

---

## Fuentes consultadas

1. **MDN Web Docs — Web Components:** [https://developer.mozilla.org/es/docs/Web/API/Web_components](https://developer.mozilla.org/es/docs/Web/API/Web_components) (Consultado el 17 de noviembre de 2026).
2. **MDN Web Docs — Uso de plantillas y ranuras (`<template>` y `<slot>`):** [https://developer.mozilla.org/es/docs/Web/API/Web_components/Using_templates_and_slots](https://developer.mozilla.org/es/docs/Web/API/Web_components/Using_templates_and_slots) (Consultado el 17 de noviembre de 2026).
3. **Can I use — Custom Elements (v1) & Shadow DOM (v1):** [https://caniuse.com/custom-elementsv1](https://caniuse.com/custom-elementsv1) (Consultado el 17 de noviembre de 2026).
4. **React Official Documentation — Describing the UI:** [https://react.dev/learn/describing-the-ui](https://react.dev/learn/describing-the-ui) (Consultado el 17 de noviembre de 2026).
5. **Node.js Official Documentation — Introduction to Node.js:** [https://nodejs.org/en/learn/getting-started/introduction-to-nodejs](https://nodejs.org/en/learn/getting-started/introduction-to-nodejs) (Consultado el 17 de noviembre de 2026).
