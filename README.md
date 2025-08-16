# TecHackatón 2025 - Sitio Oficial

## Descripción del Sitio
Página web estática para el evento TecHackatón 2025, organizado por el Tecnológico de Costa Rica. Contiene información sobre el evento, requisitos de participación, formulario de registro y detalles de contacto. Desarrollado exclusivamente con HTML5 semántico para el Laboratorio 2.

## Estructura Semántica
- **`<header>`**: Contiene el título principal y navegación
- **`<nav>`**: Menú principal con tabla de navegación
- **`<main>`**: Contenido principal con 5 secciones:
  - `<article id="acerca">`: Información general del evento
  - `<section id="detalles">`: Agenda y logística
  - `<section id="requisitos">`: Requisitos de participación
  - `<section id="registro">`: Formulario interactivo
  - `<section id="contacto">`: Información de contacto
- **`<aside>`**: Sección de patrocinadores
- **`<footer>`**: Derechos de autor y enlaces adicionales

## URL Pública en Netlify
[https://lab2html.netlify.app/](https://lab2html.netlify.app/)

## Validación W3C
![!\[Validación W3C exitosa\](w3c-validation.png)](imagen/W3C.png)
- **Resultado:** Documento válido sin errores

## Resultados Lighthouse
![!\[Resultados Lighthouse\](lighthouse-results.png)](imagen/ligthhouse.png)

| Categoría       | Puntuación | Observaciones |
|-----------------|------------|---------------|
| Accesibilidad   | 96         | Detallado abajo |
| SEO             | 100        | - |
| Mejores Prácticas | 100      | - |
| Rendimiento     | 100        | - |

### Análisis de Accesibilidad (96/100)
**Recomendación no implementada:**
"Los objetivos táctiles (checkboxes y radio buttons) no cumplen con el tamaño mínimo recomendado de 48x48px para dispositivos táctiles".

**Justificación:**
Los controles de formulario nativos en HTML tienen tamaños fijos que no cumplen con los estándares modernos de accesibilidad táctil. Por lo tanto la mejor solucion seria utilizar el css para cambiar su style, ya sea con un documento aparte o en la misma linea de los elementos en el html pero debido a que el laboratorio restringe el uso de css no se puede implementar la solucion necesaria.

**Codigo ejemplo de como se veria el CSS:**

```css
/* Solución (requeriría CSS) */
input[type="checkbox"], 
input[type="radio"] {
    min-width: 48px;
    min-height: 48px;
    margin: 8px;
    transform: scale(1.5); 
}
```


## Accesibilidad Aplicada

### Uso de tabindex (`tabindex`)
----------------------------------------------------
#### Implementación y justificación:

``` html
<!-- Imagen principal - Permitir foco para navegación por teclado -->
<img src="imagen/trabajoeq.jpg" tabindex="0"
     alt="Participantes trabajando..." width="750" height="500">

<!-- Logos - Excluir de navegación secuencial -->
<img src="imagen/Amd-logo.jpg" alt="Logo de AMD" width="178"
    height="100" tabindex="-1">
<img src="imagen/logo_tec.jpg" alt="Logo del TEC" width="430"
    height="100" tabindex="-1">
<img src="imagen/CPIC.png" alt="Logo CPIC" width="256" height="100"
    tabindex="-1">
```

##### Razones:

-   **tabindex="0":** Para que la imagen destacada sea accesible mediante navegación por teclado (usuarios que no usan mouse)

-   **tabindex="1":** En logos secundarios para evitar saturar el tab order, manteniendo el foco en elementos interactivos clave



### Atributos ARIA (`aria-label`, `aria-labelledby`)
----------------------------------------------------
#### Implementación en formulario:

```html
<fieldset>
    <legend>Tipo de participante:</legend>
    <input type="radio" id="estudiante" name="tipo" value="estudiante"
        aria-label="Opción: Estudiante">
    <label for="estudiante">Estudiante</label>

    <input type="radio" id="profesional" name="tipo" value="profesional"
        aria-label="Opción: Profesional">
    <label for="profesional">Profesional</label>
</fieldset>

<button type="submit" aria-label="Enviar formulario de registro">  
    Registrarse
</button>
```
#### Navegación:

```html

<nav>
  <table>
    <tr>
      <td><a href="#acerca" aria-label="Ir a sección: Acerca del evento">Acerca</a></td>
      <!-- ... otros enlaces ... -->
    </tr>
  </table>
</nav>
```
#### Razones:

-   **aria-label:** Proporciona etiquetas accesibles para:

    -   Controles de formulario sin texto visible como los botones

    -   Elementos interactivos complejos (grupos de radio buttons)

-   Mejora la experiencia para usuarios de lectores de pantalla


### Texto Alternativo (`alt`)
-----------------------------

#### Implementación:

```html

<!-- Imagen con contexto importante -->
<img src="imagen/trabajoeq.jpg"
     alt="Equipo de 4 participantes colaborando en computadores durante el hackatón anterior"
     width="750" height="500">

<!-- Logos con significado -->
<img src="imagen/logo_tec.jpg"
     alt="Logo oficial del Tecnológico de Costa Rica"
     width="430" height="100">
```
#### Razones:

-   Proporcionar contexto equivalente para:

    -   Usuarios con discapacidad visual

    -   Cuando las imágenes no cargan

    -   SEO (los motores de búsqueda analizan el texto alt)


### Enlaces Descriptivos
------------------------

#### Implementación:

```html

<!-- Enlace externo con contexto claro -->
<a href="https://www.tec.ac.cr" target="_blank" rel="noopener noreferrer"
   aria-label="Abre en nueva pestaña: Sitio oficial del TEC">
  Visitar página institucional del TEC
</a>
```
#### Razones:

-   Evitar texto genérico como "clic aquí"

-   Proporcionar contexto fuera del texto circundante

-   Indicar claramente la acción y destino

-   Cumple con WCAG 2.1 AA