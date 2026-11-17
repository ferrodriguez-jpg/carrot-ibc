# Carrot IBC: sitio web en código (fuera de Wix)

Sitio estático en HTML, CSS y JavaScript, sin frameworks ni dependencias. Reproduce el contenido de carrotibc.com y mantiene **las mismas URLs**, así que no pierdes SEO al migrar.

## Estructura

```
index.html                              → /
work/index.html                         → /work
work/beaconlogistics/index.html         → /work/beaconlogistics
work/lyrbausa/index.html                → /work/lyrbausa
work/disuco/index.html                  → /work/disuco
work/conekta/index.html                 → /work/conekta
work/aduanapp/index.html                → /work/aduanapp
newsletter/index.html                   → /newsletter
newsletter/thanks/index.html            → página de gracias del formulario
marketingbuiltforb2bbusinesses/index.html → /marketingbuiltforb2bbusinesses
404.html, sitemap.xml, robots.txt
css/styles.css   ← colores, tipografías y todo el diseño (variables al inicio)
js/main.js       ← menú móvil y animaciones
assets/img/      ← imágenes (se descargan con el script)
files/           ← playbook PDF
```

## 1. Descarga las imágenes (una sola vez)

Las imágenes siguen en los servidores de Wix. Antes de cancelar Wix, descárgalas al proyecto:

- **Mac / Linux:** `bash download-assets.sh`
- **Windows:** `powershell -ExecutionPolicy Bypass -File download-assets.ps1`

Descarga las versiones originales en alta resolución a `assets/img/` y el playbook a `files/`.
Si quieres cambiar alguna imagen, reemplaza el archivo con el mismo nombre.

## 2. Pruébalo en tu computadora

Abre una terminal en la carpeta y ejecuta:

```
python3 -m http.server 8000
```

Luego abre http://localhost:8000. Hazlo con un servidor y no con doble clic, porque las rutas tipo `/work/` así funcionan igual que en producción.

## 3. Publícalo (recomendado: Netlify)

1. Crea una cuenta en netlify.com → **Add new site → Deploy manually** → arrastra la carpeta.
2. El formulario del newsletter ya está preparado para **Netlify Forms**: los correos te llegan a Netlify → Forms. Desde ahí puedes conectarlo a Mailchimp, HubSpot, etc.
   Si usas otro hosting (Vercel, Cloudflare Pages), cambia el `action` del `<form>` en `newsletter/index.html` por la URL de tu herramienta de email (Mailchimp, Beehiiv, Brevo…).
3. En Netlify → Domain settings, agrega `carrotibc.com` y `www.carrotibc.com`.

## 4. Mueve el dominio

- Si el dominio está **comprado en Wix**: Wix → Dominios → *Transferir fuera de Wix* → copia el código de autorización y úsalo en el nuevo registrador (Cloudflare, Namecheap, etc.).
- Si el dominio está **en otro registrador**: cambia los DNS a los que te dé Netlify.
- Cancela el plan de Wix **hasta que** el sitio nuevo esté funcionando en tu dominio.

## Pendientes antes de publicar

- **Newsletter:** agrega las ediciones anteriores en `newsletter/index.html` (sección "Catch up on our latest newsletters"; hay un bloque `<a class="issue">` de ejemplo).
- **Book a Call / Let's Talk:** ahora abren un correo a andresmorales@carrotibc.com. Si usas Calendly o HubSpot Meetings, reemplaza los `href="mailto:..."`.
- **Analytics:** pega el código de Google Analytics / Tag Manager antes de `</head>` en cada página.
- Revisa que las imágenes de la galería, los servicios y los logos de clientes sean las que quieres en cada lugar.

## Cómo editar

- **Textos:** directamente en cada `index.html`.
- **Colores y tipografía:** en las variables al inicio de `css/styles.css` (`--teal`, `--blue`, `--head`, `--body`).
- **Página nueva:** copia una carpeta existente (por ejemplo `work/disuco/`), renómbrala y cambia el contenido. Agrega la URL a `sitemap.xml`.
