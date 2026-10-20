# 💰 Pocket Budget: sitio web + app

Una app de finanzas personales gratis, en español e inglés. La página de bienvenida presenta la app y pide el correo; con eso, la persona entra a la app.

```
tu-sitio/                → página de bienvenida (index.html)
tu-sitio/app/            → la app (solo abre si ya dejaron su correo)
backend/Code.gs          → guarda los correos en tu hoja de Google (no se publica)
```

## 1. Guardar los correos en una hoja de Google (5 minutos, gratis)
1. Crea una hoja nueva en [sheets.new](https://sheets.new), por ejemplo "Pocket Budget registros".
2. **Extensiones → Apps Script**. Borra lo que hay en `Code.gs` y pega el contenido de `backend/Code.gs`.
3. Arriba en el archivo, cambia `APP_LINK` por la dirección de tu app (paso 2, termina en `/app/`).
   Si no quieres enviar correo de bienvenida, pon `SEND_WELCOME_EMAIL = false`.
4. Guarda. Elige la función **setup** y presiona **▶ Ejecutar**. Acepta los permisos.
5. **Implementar → Nueva implementación → ⚙️ → Aplicación web**
   - Ejecutar como: **Yo**
   - Quién tiene acceso: **Cualquier persona**
6. Presiona **Implementar** y copia la **URL de la aplicación web** (termina en `/exec`).
7. Abre `index.html` (la página de bienvenida), busca `var SIGNUP_URL = '';` y pega tu URL entre las comillas.

Cada registro agrega una fila: fecha, correo, idioma, si acepta recibir novedades, de dónde llegó, cuántas veces volvió y la última vez. Si el mismo correo se registra otra vez, solo se actualiza su fila.

> Una cuenta normal de Gmail puede enviar unos 100 correos al día. Si recibes más registros que eso, se siguen guardando, pero el correo de bienvenida se salta cuando se acaba la cuota.

## 2. Publicar en GitHub Pages (5 minutos)
1. Crea un repositorio **público**, por ejemplo `pocket-budget`.
2. Sube **todo** el contenido de esta carpeta (incluida la carpeta `app/` y el archivo `.nojekyll`).
   La carpeta `backend/` puede subirse también; GitHub no la ejecuta.
3. **Settings → Pages → Deploy from a branch → `main` / `(root)` → Save**.
4. En un minuto estará en `https://TU-USUARIO.github.io/pocket-budget/`.

## Cómo funciona el acceso
- En la página de bienvenida la persona escribe su correo y acepta los términos de privacidad. La casilla de novedades es opcional.
- El correo se envía a tu hoja y queda guardado en su teléfono. Luego se abre la app.
- Si alguien abre `/app/` sin haberse registrado en ese navegador, la app lo regresa a la página de bienvenida.
- Quien instala la app en su pantalla de inicio entra directo.
- Si la persona elige español en la página de bienvenida, la app abre en español.

**Importante:** como todo funciona sin servidor, este acceso es para registrar a tus usuarios, no para proteger información. Alguien con conocimientos técnicos podría saltárselo. Los datos financieros de cada persona nunca salen de su teléfono, así que no hay información que exponer.

## Antes de lanzar
- **Privacidad:** la página ya explica qué haces con el correo. Si vas a enviar correos de marketing, incluye siempre una forma de darse de baja y tu dirección física (requisito de la ley CAN-SPAM en EE. UU.). Si recibes usuarios de Europa, aplica el RGPD.
- **Dominio propio:** en Settings → Pages → Custom domain puedes usar algo como `pocketbudget.app`.
- **Muchos usuarios:** GitHub Pages tiene un límite blando de 100 GB de tráfico al mes y no está pensado para servicios comerciales. Cuando crezcas, conecta el mismo repositorio a Cloudflare Pages o Netlify. Para miles de registros diarios, cambia la hoja de Google por un servicio de correo como Brevo, Mailchimp o ConvertKit.

## Actualizar la app
Cambia los archivos y súbelos. Luego abre `app/sw.js` y sube el número de `VERSION` (por ejemplo `pb-v6`), para que los teléfonos que ya la instalaron reciban la nueva versión.
