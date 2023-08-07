# Toggle Password

The function to toggle password. Just only need tailwindcss. No need other dependencies.

## Demo

![image](https://github.com/tmh-rc/code-snippet/assets/59432845/f022e70f-ea9e-49b8-910d-2060f6b520d2)

## Dependencies

[Tailwind CSS](https://tailwindcss.com/)

## Function
```js
// togglePassword.js
function togglePassword() {
    const passwordFields = document.querySelectorAll("input[type=password]");

    passwordFields.forEach((passwordField) => {
        const parentElement = passwordField.parentElement;
        parentElement.classList.add("relative");

        const toggleSvg = document.createElement("span");
        toggleSvg.classList.add("absolute", "right-2", "top-1/2", "-translate-y-1/2", "cursor-pointer");

        const createSvgElement = () => {
            const svg = document.createElementNS("http://www.w3.org/2000/svg", "svg");
            svg.setAttribute("xmlns", "http://www.w3.org/2000/svg");
            svg.setAttribute("viewBox", "0 0 24 24");
            svg.setAttribute("fill", "none");
            svg.setAttribute("stroke", "currentColor");
            svg.setAttribute("stroke-width", "1.5");
            svg.setAttribute("class", "w-6 h-6 text-gray-600");
            return svg;
        };

        const createEyeSvg = () => {
            const svg = createSvgElement();
            svg.innerHTML = `
            <path stroke-linecap="round" stroke-linejoin="round" d="M2.036 12.322a1.012 1.012 0 010-.639C3.423 7.51 7.36 4.5 12 4.5c4.638 0 8.573 3.007 9.963 7.178.07.207.07.431 0 .639C20.577 16.49 16.64 19.5 12 19.5c-4.638 0-8.573-3.007-9.963-7.178z" />
            <path stroke-linecap="round" stroke-linejoin="round" d="M15 12a3 3 0 11-6 0 3 3 0 016 0z" />
        `;

            return svg;
        };

        const createClosedEyeSvg = () => {
            const svg = createSvgElement();
            svg.innerHTML = `
            <path stroke-linecap="round" stroke-linejoin="round" d="M3.98 8.223A10.477 10.477 0 001.934 12C3.226 16.338 7.244 19.5 12 19.5c.993 0 1.953-.138 2.863-.395M6.228 6.228A10.45 10.45 0 0112 4.5c4.756 0 8.773 3.162 10.065 7.498a10.523 10.523 0 01-4.293 5.774M6.228 6.228L3 3m3.228 3.228l3.65 3.65m7.894 7.894L21 21m-3.228-3.228l-3.65-3.65m0 0a3 3 0 10-4.243-4.243m4.242 4.242L9.88 9.88" />
        `;

            return svg;
        };

        const updatePasswordToggle = () => {
            const svg = toggleSvg.querySelector("svg");
            if (passwordField.type === "password") {
                passwordField.type = "text";
                toggleSvg.replaceChild(createClosedEyeSvg(), svg);
            } else {
                passwordField.type = "password";
                toggleSvg.replaceChild(createEyeSvg(), svg);
            }
        };

        toggleSvg.appendChild(createEyeSvg());
        parentElement.appendChild(toggleSvg);

        toggleSvg.addEventListener("click", updatePasswordToggle);
    });
}
```
You need to export for JS framework (eg. Vue, React, etc..)
```js
// Utils/togglePassword.js
export default function togglePassword() {
    ...
}
```

## Usage

### HTML

```html
<html>
    <head>
        <script src="https://cdn.tailwindcss.com?plugins=forms"></script>
    </head>
    <body>
        <form>
            <label>Password</label>
            <div>
                <input type="password" name="password" class="w-full"/>
            </div>
        </form>

        <script src="togglePassword.js"></script>
        <script>
            togglePassword();
        </script>
    </body>
</html>
```

### Vue

```vue
<script setup>
import { onMounted } from "vue";
import togglePassword from "@/Utils/togglePassword";

onMounted(() => {
    togglePassword();
});
</script>

<template>
    <form>
        <label>Password</label>
        <div>
            <input type="password" name="password" class="w-full" />
        </div>
    </form>
</template>
```

### React

```jsx
import { useEffect } from 'react';
import togglePassword from '@/Utils/togglePassword';

export default function Login() {
    useEffect(() => {
        togglePassword();
    }, []);

    return (
        <form>
            <label>Password</label>
            <div>
                <input type="password" name="password" class="w-full"/>
            </div>
        </form>
    );
}
```
