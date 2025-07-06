# Librería Enlace de repositorio: ComponenteGeneradorContrase-as

<div align="center">

**TECNOLOGICO NACIONAL DE MEXICO**  
**INSTITUTO TECNOLÓGICO DE OAXACA**

Departamento de Ingeniería en Sistemas Computacionales  

Materia: Programación Web  
“Componente Enlace de repositorio de Github y/o GitHub Pages”  
Profesor: Martínez Nieto Adelina

Equipo 10:  
López Cruz David Eduardo  
Salinas Montesinos Cintia Yadai  
Grupo: VSI  

Oaxaca, Oaxaca, a 04 de julio de 2025.

</div>


**ComponenteGeneradorContrase-as** 
- Componente web para generar contraseñas seguras con validación de seguridad, botón de mostrar/ocultar y estilos personalizados.
  
## Descripción General
-Su propósito principal es generar contraseñas seguras que cumplan con criterios de seguridad recomendados, evitando el uso de claves débiles o predecibles.

-El componente GeneradorContraseñaSegura ofrece una interfaz intuitiva para ingresar contraseñas manualmente o generarlas automáticamente con un clic.

-Incluye funciones como mostrar/ocultar la contraseña, validación visual de seguridad y recomendaciones sobre el uso de caracteres variados.

-Este componente resuelve el problema común de usuarios que crean contraseñas inseguras, brindando una herramienta fácil de integrar en cualquier formulario web.

-Se puede utilizar en formularios de registro, inicio de sesión, restablecimiento de contraseña o cualquier sistema donde se requiera una clave segura, sin necesidad de frameworks externos.


## ¿Qué problema resuelve?
Previene errores al generar e ingresar contraseñas.
Problema: Los usuarios suelen crear contraseñas débiles, repetidas o fáciles de adivinar. Esto representa un riesgo para la seguridad de sus cuentas.

Solución: El componente sugiere automáticamente contraseñas seguras y proporciona validación visual para garantizar que cumplan con criterios como longitud, uso de mayúsculas, minúsculas, números y símbolos.
Además, evita errores como campos de contraseña vacíos o mal ingresados gracias a su diseño claro y funciones accesibles.

---
## 📦 INSTALACIÓN

Puedes integrar el componente Generador de Contraseña Segura en tu proyecto HTML de la siguiente manera:

1. Descarga los archivos necesarios:
   - `componente.js`
   - `componente.css`

2. Coloca ambos archivos en las carpetas correspondientes de tu proyecto (por ejemplo: `/js/` y `/css/`).

3. En tu archivo HTML, enlaza los archivos así:

```html
<link rel="stylesheet" href="css/componente.css">
<script src="js/componente.js" defer></script>
```

4. Asegúrate de tener en el cuerpo (`<body>`) la estructura HTML del componente. Por ejemplo:

```html
<div class="contenedor">
  <h2>Generador Contraseña Segura</h2>

  <label for="password">Contraseña:</label>
  <div class="input-group">
    <input type="password" id="password" oninput="evaluarPassword(this.value)" placeholder="Ingrese su contraseña" />
    <button onclick="togglePassword()">👁️</button>
  </div>

  <p class="recomendacion">Para mayor seguridad, usa al menos 10 caracteres incluyendo mayúsculas, minúsculas, números y símbolos.</p>

  <div class="input-group">
    <button onclick="generarPassword()">Generar contraseña segura</button>
  </div>

  <div class="barra-seguridad" id="barraSeguridad">
    <div class="nivel" id="nivelSeguridad"></div>
  </div>

  <p id="textoSeguridad"></p>
</div>
```

---

### Nota:
No necesitas instalar ningún paquete externo ni usar librerías de terceros. Este componente fue creado usando únicamente HTML, CSS y JavaScript puro, por lo que es **ligero, rápido y fácilmente integrable** en cualquier proyecto.


---

## USO⚙️
El componente GeneradorContraseñaSegura proporciona funciones simples que puedes llamar directamente desde JavaScript para generar y mostrar contraseñas seguras.

Incluye una función principal para generar contraseñas aleatorias que cumplan con requisitos de seguridad (longitud mínima, uso de símbolos, números y letras).

También permite mostrar u ocultar la contraseña con un solo clic, mejorando la experiencia del usuario en formularios.

El componente se puede integrar fácilmente en formularios HTML sin depender de frameworks externos.

  
Ejemplo de implementación en HTML/JS (con código embebido):
```HTML
<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Formulario Validado</title>
  <script src="https://cdn.jsdelivr.net/npm/just-validate@4.2.0/dist/just-validate.production.min.js"></script>
</head>
```
---
## Captura de pantalla del codigo HTML
![image](https://github.com/user-attachments/assets/9d8c9511-0a60-4877-ac63-2492ab893a1e)

## Captura de pantalla de JavaScript
![image](https://github.com/user-attachments/assets/31cacec2-2a77-4da1-b62c-a617b748208d)
![image](https://github.com/user-attachments/assets/fd31c9cd-d808-4f9a-8799-4343ed257922)

## Explicación detallada de funciones

### togglePassword()

Esta función permite alternar entre mostrar y ocultar la contraseña en el campo de entrada.

- **Paso 1:** Se accede al campo de contraseña usando `document.getElementById("password")`.
- **Paso 2:** Se verifica el tipo del campo: si es `"password"`, se cambia a `"text"` para mostrar la contraseña; si es `"text"`, se cambia de nuevo a `"password"` para ocultarla.

Esto mejora la usabilidad al permitir que el usuario vea lo que está escribiendo si lo desea.

```js
function togglePassword() {
  const passwordInput = document.getElementById("password");
  const type = passwordInput.type === "password" ? "text" : "password";
  passwordInput.type = type;
}
```

---

### generarPassword()

Función encargada de generar una nueva contraseña aleatoria segura y asignarla al campo de entrada.

- **Paso 1:** Se llama a `generarContrasenaSegura()` para crear la contraseña.
- **Paso 2:** Se coloca en el campo de texto automáticamente.
- **Paso 3:** Se ejecuta `evaluarPassword()` para analizar el nivel de seguridad de la nueva contraseña.

```js
function generarPassword() {
  const passwordInput = document.getElementById("password");
  const pwd = generarContrasenaSegura();
  passwordInput.value = pwd;
  evaluarPassword(pwd);
}
```

---

### generarContrasenaSegura()

Esta función crea una contraseña fuerte de al menos 12 caracteres. La contraseña siempre contiene como mínimo:

- Una letra mayúscula
- Una letra minúscula
- Un número
- Un símbolo especial

**Funcionamiento:**

- Se crean strings con diferentes tipos de caracteres.
- Se selecciona un carácter de cada tipo para garantizar variedad.
- Luego se agregan caracteres aleatorios hasta alcanzar al menos 12.
- Finalmente, se mezclan todos los caracteres para evitar patrones.

```js
function generarContrasenaSegura() {
  const mayus = "ABCDEFGHIJKLMNOPQRSTUVWXYZ";
  const minus = "abcdefghijklmnopqrstuvwxyz";
  const numeros = "0123456789";
  const especiales = "!@#$%^&*()-_=+";
  const allChars = mayus + minus + numeros + especiales;

  let pwd = [
    mayus[Math.floor(Math.random() * mayus.length)],
    minus[Math.floor(Math.random() * minus.length)],
    numeros[Math.floor(Math.random() * numeros.length)],
    especiales[Math.floor(Math.random() * especiales.length)]
  ];

  for (let i = pwd.length; i < 12; i++) {
    pwd.push(allChars[Math.floor(Math.random() * allChars.length)]);
  }

  return pwd.sort(() => Math.random() - 0.5).join('');
}
```

---

### evaluarPassword(password)

Evalúa el nivel de seguridad de la contraseña en tiempo real y actualiza visualmente una barra y un mensaje.

**Criterios evaluados (1 punto cada uno):**
- Longitud mínima de 10 caracteres
- Contiene mayúsculas
- Contiene minúsculas
- Contiene números
- Contiene símbolos

**Resultado:**
- Se calcula un porcentaje (20% por cada criterio cumplido).
- Se actualiza el color y tamaño de la barra.
- Se muestra un mensaje: "Débil", "Regular", "Buena" o "Muy segura".

```js
function evaluarPassword(password) {
  const barra = document.getElementById("nivelSeguridad");
  const texto = document.getElementById("textoSeguridad");
  let nivel = 0;

  if (password.length >= 10) nivel++;
  if (/[A-Z]/.test(password)) nivel++;
  if (/[a-z]/.test(password)) nivel++;
  if (/[0-9]/.test(password)) nivel++;
  if (/[\W_]/.test(password)) nivel++;

  const porcentaje = nivel * 20;
  barra.style.width = `${porcentaje}%`;

  if (nivel <= 2) {
    barra.style.backgroundColor = "red";
    texto.textContent = "Débil";
  } else if (nivel === 3) {
    barra.style.backgroundColor = "orange";
    texto.textContent = "Regular";
  } else if (nivel === 4) {
    barra.style.backgroundColor = "gold";
    texto.textContent = "Buena";
  } else {
    barra.style.backgroundColor = "green";
    texto.textContent = "Muy segura";
  }
}
```

---




## FORMULARIO VALIDADO
consola del navegador mostrando resultados 

Imagen1: formulario mostrando todos los campos

![image](https://github.com/user-attachments/assets/5c04d9bd-35b0-4c9c-b335-10f727c6e9dc)

Formulario con capus rellenados

![image](https://github.com/user-attachments/assets/3481afab-f67a-4450-8301-4498d8ecda2a)


## VIDEO EXPLICADO DE LA LIBRERIA
https://youtu.be/WOUJ4MwsG3c

## GitHub Pages
https://david-eduardolc.github.io/mi-componente-js/


