# Laboratorio 7. Validación de formularios y manipulación de objetos DOM con JavaScript

¡Bienvenido! En este laboratorio implementarás validación de formularios usando JavaScript y manipularás elementos del DOM para mejorar la experiencia del usuario en un formulario de registro bancario.

- Nivel: Intermedio
- Tecnologías: HTML, CSS y JavaScript
- Objetivo: Validar campos de formulario con JavaScript y manipular el DOM para mostrar errores visuales
- Tiempo estimado: 60–90 minutos

## ¿Qué está hecho y qué debes hacer?

### ✅ Ya está implementado (NO necesitas hacer esto):
- El formulario HTML completo con todos los campos
- Los estilos CSS (formulario bonito y responsivo)
- Las clases CSS `.no-valid` y `.error-message` listas para usar

### 🎯 Tu trabajo (LO QUE DEBES IMPLEMENTAR):
- Crear el archivo JavaScript `scripts.js`
- Conectar el JavaScript al HTML
- Implementar la función `validateForm()`
- Validar cada campo del formulario
- Aplicar/remover la clase `.no-valid` según el estado del campo
- Prevenir el envío del formulario si hay errores
- Mostrar mensajes al usuario

## Lo que vas a construir
Un formulario de registro bancario con validación en JavaScript que incluye:

**Campos del formulario:**
1. Nombre
2. Apellido Paterno
3. Apellido Materno
4. Número de cédula (con validación de formato ecuatoriano)
5. Motivo de apertura de cuenta
6. Tipo de cuenta (Ahorros, Corriente)
7. Dirección de domicilio (Calle, número e intersección)
8. Foto (subir archivo)
9. Botón de confirmar

**Funcionalidades JavaScript a implementar:**
- Crear una función `validateForm()` que valide todos los campos
- Validación del número de cédula (debe tener exactamente 10 dígitos)
- Validación de campos de texto (no deben estar vacíos)
- Aplicación de la clase `.no-valid` a campos inválidos (borde rojo, fondo rosa)
- Prevención del envío del formulario si hay errores
- Mostrar un mensaje de éxito cuando todos los campos sean válidos

Al final, tu formulario no solo se verá bien (CSS ya incluido), sino que validará los datos antes de permitir el envío.

## Requisitos previos
- Un editor de texto (por ejemplo, Visual Studio Code)
- Un navegador web moderno (Chrome, Edge, Firefox o Safari)
- Conocimientos básicos de HTML, CSS y JavaScript
- Familiaridad con el DOM (Document Object Model)
- Comprensión de eventos en JavaScript

## Construcción paso a paso

El formulario HTML y los estilos CSS ya están implementados. Tu tarea es agregar JavaScript para validar el formulario.

### Paso 1: Crear y conectar el archivo JavaScript

**¡IMPORTANTE!** Esta es la parte fundamental: conectar tu JavaScript con el HTML.

1. Crea una carpeta `assets/js/` en tu proyecto (si no existe)
2. Dentro de esa carpeta, crea el archivo `scripts.js`
3. **Conecta el JavaScript al HTML**: Abre `index.html` y agrega esta línea ANTES del cierre de `</body>`:

```html
        <button type="submit">Confirmar</button>
    </form>
    
    <!-- ⬇️ AGREGA ESTA LÍNEA AQUÍ ⬇️ -->
    <script src="assets/js/scripts.js"></script>
</body>
</html>
```

**¿Por qué antes del cierre de `</body>`?** Porque necesitamos que el HTML cargue primero antes de que el JavaScript intente acceder a los elementos del formulario.

**💡 Verificación rápida:** 
Después de crear el archivo y conectarlo, agrega esto en `scripts.js` para verificar la conexión:
```javascript
console.log('✅ JavaScript conectado correctamente');
```
Abre `index.html` en el navegador, presiona F12, y deberías ver el mensaje en la consola.

### Paso 2: Estructura básica del JavaScript

En tu archivo `scripts.js`, necesitas:

1. **Esperar a que el DOM cargue**: Usa `DOMContentLoaded` para asegurarte de que todos los elementos HTML estén disponibles
2. **Capturar el evento submit**: Evita que el formulario se envíe de la forma tradicional
3. **Llamar a tu función de validación**: Ejecuta `validateForm()` cuando se intente enviar

```javascript
document.addEventListener('DOMContentLoaded', function() {
    const form = document.querySelector('form');
    
    form.addEventListener('submit', function(event) {
        event.preventDefault(); // Evita que el formulario se envíe
        
        // Llamar a la función de validación
        if (validateForm()) {
            alert('¡Formulario válido! Registro exitoso.');
        } else {
            alert('Por favor, corrija los errores en el formulario.');
        }
    });
});
```

**📋 Plantilla completa de `scripts.js` para empezar:**

```javascript
// Esperar a que el DOM esté completamente cargado
document.addEventListener('DOMContentLoaded', function() {
    const form = document.querySelector('form');
    
    // Escuchar el evento submit del formulario
    form.addEventListener('submit', function(event) {
        event.preventDefault(); // Prevenir envío por defecto
        
        if (validateForm()) {
            alert('✅ ¡Formulario válido! Registro exitoso.');
            // Opcional: limpiar el formulario
            // form.reset();
        } else {
            alert('❌ Por favor, corrija los errores en el formulario.');
        }
    });
});

// Función principal de validación
function validateForm() {
    let isValid = true;
    
    // Aquí debes implementar todas las validaciones
    // Por cada campo inválido, cambiar isValid a false
    
    return isValid;
}
```

### Paso 3: Crear la función validateForm()

Esta es la función principal que debes implementar. Debe:

```javascript
function validateForm() {
    let isValid = true; // Asume que todo es válido al inicio
    
    // TODO: Obtener todos los campos del formulario
    // Pista: usa document.getElementById('id-del-campo')
    
    // TODO: Validar cada campo
    // Si algún campo es inválido, cambiar isValid a false
    
    // TODO: Aplicar la clase .no-valid a campos inválidos
    // TODO: Remover la clase .no-valid de campos válidos
    
    return isValid; // Retorna true si todo está bien, false si hay errores
}
```

### Paso 4: Validaciones necesarias

Implementa validaciones para cada tipo de campo. Aquí te damos las **reglas de validación**:

#### Campos de texto (nombre, apellidos, dirección):
- No deben estar vacíos
- Deben tener al menos 2 caracteres
- **Pista**: Usa `.value` para obtener el valor y `.trim()` para quitar espacios

#### Campo cédula:
- Debe tener exactamente 10 dígitos
- Solo debe contener números
- **Pista**: Usa una expresión regular `/^\d{10}$/` o verifica la longitud y que sean solo números

#### Textarea (motivo):
- No debe estar vacío
- Debe tener al menos 10 caracteres

#### Select (tipo de cuenta):
- Debe tener un valor seleccionado (diferente de la opción vacía)
- **Pista**: Verifica que `select.value !== ''`

### Paso 5: Aplicar estilos de error

Cuando un campo sea **inválido**, debes:
```javascript
campo.classList.add('no-valid');
```

Cuando un campo sea **válido**, debes:
```javascript
campo.classList.remove('no-valid');
```

### Paso 6: Probar tu código

1. Abre `index.html` en tu navegador
2. Abre la consola del navegador (F12)
3. Intenta enviar el formulario vacío
4. Intenta con datos inválidos (nombre muy corto, cédula incorrecta)
5. Verifica que los campos se marquen en rojo cuando son inválidos
6. Completa correctamente y verifica que aparezca el mensaje de éxito

## Consejos y pistas

### Para obtener valores de campos:
```javascript
const nombre = document.getElementById('nombre');
const valorNombre = nombre.value.trim(); // trim() quita espacios al inicio/final
```

### Para validar longitud:
```javascript
if (valorNombre.length < 2) {
    // Es inválido
}
```

### Para validar solo números (cédula):
```javascript
// Opción 1: Expresión regular
if (!/^\d{10}$/.test(cedula.value)) {
    // Inválido: no son 10 dígitos
}

// Opción 2: Verificar longitud y que sean números
if (cedula.value.length !== 10 || isNaN(cedula.value)) {
    // Inválido
}
```

### Para validar select:
```javascript
const tipoCuenta = document.getElementById('tipoCuenta');
if (tipoCuenta.value === '') {
    // No ha seleccionado nada
}
```

## Estructura sugerida para validateForm()

```javascript
function validateForm() {
    let isValid = true;
    
    // 1. Validar nombre
    const nombre = document.getElementById('nombre');
    if (/* condición de invalidez */) {
        nombre.classList.add('no-valid');
        isValid = false;
    } else {
        nombre.classList.remove('no-valid');
    }
    
    // 2. Validar apellido paterno
    // ... similar al nombre
    
    // 3. Validar apellido materno
    // ... similar al nombre
    
    // 4. Validar cédula (10 dígitos)
    const cedula = document.getElementById('cedula');
    if (/* condición para 10 dígitos */) {
        cedula.classList.add('no-valid');
        isValid = false;
    } else {
        cedula.classList.remove('no-valid');
    }
    
    // 5. Validar motivo
    // ... al menos 10 caracteres
    
    // 6. Validar tipo de cuenta
    // ... debe tener valor seleccionado
    
    // 7. Validar calle
    // ... similar al nombre
    
    // 8. Validar número
    // ... no vacío
    
    // 9. Validar intersección
    // ... similar al nombre
    
    return isValid;
}
```

## Desafío adicional (opcional)

Si terminas pronto, intenta agregar **mensajes de error** personalizados:

```javascript
function mostrarError(campo, mensaje) {
    campo.classList.add('no-valid');
    
    // Crear elemento para el mensaje
    const errorDiv = document.createElement('div');
    errorDiv.className = 'error-message';
    errorDiv.textContent = mensaje;
    
    // Insertar después del campo
    campo.parentNode.insertBefore(errorDiv, campo.nextSibling);
}
```

## ¿Cómo probarlo?
1. Abre `index.html` en tu navegador
2. Abre la **Consola de Desarrollador** (presiona F12) para ver posibles errores
3. Intenta enviar el formulario vacío → Deberías ver campos marcados en rojo
4. Llena los campos con datos inválidos:
   - Nombres muy cortos (menos de 2 caracteres)
   - Cédula con menos o más de 10 dígitos, o con letras
   - Motivo muy corto (menos de 10 caracteres)
   - Sin seleccionar tipo de cuenta
5. Llena correctamente todos los campos y verifica el mensaje de éxito

### Datos de prueba sugeridos:
- **Nombre**: Juan
- **Apellidos**: Pérez García
- **Cédula**: 1234567890 (10 dígitos)
- **Motivo**: Necesito abrir una cuenta para gestionar mis ahorros personales
- **Tipo de cuenta**: Ahorros
- **Calle**: Av. Amazonas
- **Número**: 123
- **Intersección**: Calle Colón

## Calificación y Entrega

Este laboratorio será calificado manualmente por el profesor. Asegúrate de completar todos los requisitos antes de la entrega.

### Criterios de evaluación:

#### Implementación de JavaScript (10 puntos total)

**1. Conexión del archivo JavaScript (1 punto)**
- Archivo `scripts.js` creado en la ubicación correcta
- Correctamente enlazado en el HTML antes del cierre de `</body>`

**2. Estructura básica y eventos (2 puntos)**
- Uso correcto de `DOMContentLoaded`
- Captura del evento `submit` del formulario
- Prevención del envío por defecto con `event.preventDefault()`

**3. Función validateForm() (2 puntos)**
- Función implementada correctamente
- Retorna `true` cuando todo es válido
- Retorna `false` cuando hay errores
- Se llama correctamente desde el event listener

**4. Validaciones de campos (3 puntos)**
- Validación de campos de texto (nombre, apellidos, dirección)
- Validación de cédula (10 dígitos numéricos)
- Validación de textarea (motivo)
- Validación de select (tipo de cuenta)

**5. Manipulación del DOM (2 puntos)**
- Aplicación correcta de la clase `.no-valid` a campos inválidos
- Remoción correcta de la clase `.no-valid` de campos válidos
- Mensajes apropiados al usuario (alert u otro método)

### Formato de entrega

Sube tu proyecto a tu repositorio de GitHub con:
- El archivo `assets/js/scripts.js` completamente implementado
- Código comentado apropiadamente
- Formulario funcionando correctamente

**Fecha de entrega:** [Definida por el profesor]

## Lista de verificación (Checklist)

### Estructura HTML y CSS (ya implementada)
- [x] Todos los campos del formulario están presentes
- [x] CSS con estilos atractivos y responsivos
- [x] Clase `.no-valid` disponible para marcar errores
- [x] Clase `.error-message` disponible para mensajes

### Tu trabajo en JavaScript (lo que debes implementar)
- [ ] Crear archivo `assets/js/scripts.js`
- [ ] Conectar el JavaScript al HTML con `<script>`
- [ ] Usar `DOMContentLoaded` para asegurar que el DOM esté cargado
- [ ] Capturar el evento `submit` del formulario
- [ ] Prevenir el envío por defecto con `event.preventDefault()`
- [ ] Crear la función `validateForm()` que retorne `true` o `false`
- [ ] Validar campos de texto (nombre, apellidos, dirección) - no vacíos, mínimo 2 caracteres
- [ ] Validar cédula - exactamente 10 dígitos numéricos
- [ ] Validar textarea (motivo) - no vacío, mínimo 10 caracteres
- [ ] Validar select (tipo de cuenta) - debe tener un valor seleccionado
- [ ] Aplicar clase `.no-valid` a campos inválidos
- [ ] Remover clase `.no-valid` de campos válidos
- [ ] Mostrar mensaje de éxito cuando todo esté correcto
- [ ] Mostrar mensaje de error cuando haya campos inválidos

## Retos opcionales (para practicar más)
1. **Mensajes de error personalizados**: En lugar de solo marcar el campo en rojo, muestra un mensaje específico debajo de cada campo indicando qué está mal
2. **Validación en tiempo real**: Valida los campos mientras el usuario escribe (eventos `blur` o `input`)
3. **Contador de caracteres**: Muestra cuántos caracteres lleva el usuario en el textarea del motivo
4. **Vista previa de imagen**: Muestra la foto seleccionada antes de enviar el formulario
5. **Botón para limpiar errores**: Agrega un botón que limpie todos los campos y remueva las marcas de error
6. **Deshabilitar botón**: Deshabilita el botón de envío hasta que todos los campos sean válidos
7. **Animación shake**: Cuando un campo sea inválido, agrégale una animación de "sacudida"
8. **Validar formato de nombre**: Asegúrate de que los nombres solo contengan letras (sin números ni caracteres especiales)

## Conceptos clave que aprenderás

### JavaScript:
- **Manipulación del DOM**: Seleccionar elementos con `getElementById()` y `querySelector()`
- **Eventos**: Escuchar eventos como `submit`, `blur`, `change`
- **Validación**: Crear lógica para verificar datos antes de procesarlos
- **Clases CSS dinámicas**: Agregar/remover clases con `classList.add()` y `classList.remove()`
- **Condicionales**: Tomar decisiones con `if/else`
- **Funciones**: Crear funciones reutilizables

### Expresiones Regulares (Regex):
- `/^\d{10}$/` - Verifica exactamente 10 dígitos
- `\d` - Representa cualquier dígito (0-9)
- `^` - Inicio de la cadena
- `$` - Final de la cadena
- `{10}` - Exactamente 10 repeticiones

### Buenas Prácticas:
- Validar datos en el cliente (JavaScript) para mejor experiencia de usuario
- Siempre validar también en el servidor (en aplicaciones reales)
- Dar retroalimentación visual clara al usuario
- Prevenir el envío de datos inválidos

---
¡Éxito en tu laboratorio! Recuerda: la programación se aprende practicando. Si algo no funciona, revisa la consola del navegador (F12) para ver los errores y usa `console.log()` para depurar tu código.

## Resumen rápido de lo que debes hacer

1. ✅ Crear `assets/js/scripts.js`
2. ✅ Conectar el script al HTML con `<script src="assets/js/scripts.js"></script>`
3. ✅ Implementar la función `validateForm()` que:
   - Obtenga los valores de todos los campos
   - Valide cada campo según las reglas especificadas
   - Aplique la clase `.no-valid` a campos inválidos
   - Remueva la clase `.no-valid` de campos válidos
   - Retorne `true` si todo es válido, `false` si hay errores
4. ✅ Capturar el evento submit y llamar a `validateForm()`
5. ✅ Mostrar mensajes apropiados al usuario

### Reglas de validación rápidas:
- **Textos**: No vacíos, mínimo 2 caracteres
- **Cédula**: Exactamente 10 dígitos numéricos
- **Motivo**: No vacío, mínimo 10 caracteres
- **Select**: Debe tener un valor seleccionado (no vacío)