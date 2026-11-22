# Plexiweb España

Landing page de Plexiweb para vender webs en España. Sitio estático (HTML/CSS/JS), sin build y sin backend.

Es la versión para España de la web argentina (`../plexiweb/plexiweb`): español de España (tú), precios en euros, textos legales para RGPD/LOPDGDD/LSSI-CE y banner de cookies conforme a la AEPD.

## Estructura

```
index.html          punto de entrada
aviso-legal.html    aviso legal (LSSI-CE art. 10)
privacidad.html     política de privacidad y cookies (RGPD + LOPDGDD)
terminos.html       términos y condiciones
css/style.css       estilos
css/legal.css       estilos de las páginas legales
js/script.js        carrusel/parallax, menú, banner de cookies (carga GTM solo con consentimiento)
assets/             logo, fondos y capturas del portfolio
```

## Antes de publicar: pendientes

Busca estos marcadores y sustitúyelos (`grep -rn "XXXXXXXXX\|legal-dato\|plexiweb.es" .`):

| Marcador | Dónde | Qué poner |
|---|---|---|
| `34XXXXXXXXX` | `index.html` (enlaces `wa.me`) | Tu WhatsApp con prefijo, sin `+` ni espacios |
| `+34XXXXXXXXX` | `index.html` (JSON-LD) | Tu teléfono en formato `+34600111222` |
| `<span class="legal-dato">…` | `aviso-legal.html`, `privacidad.html`, `terminos.html` | Titular, NIF/CIF, domicilio, email, ciudad de jurisdicción, datos del Registro Mercantil si eres sociedad |
| `plexiweb.es` | `index.html`, legales, `robots.txt`, `sitemap.xml` | Tu dominio definitivo |
| `GTM_ID = ''` | `js/script.js` → `initCookieBanner()` | ID de tu contenedor de Google Tag Manager. Vacío = no se carga analítica |
| `assets/og-image.png` | `index.html` (Open Graph) | Imagen 1200×630 de la web de España |

Los textos legales son una plantilla de partida, no asesoría legal: conviene que los revise un profesional.

## Previsualizar en local

```bash
npx serve .
# o
python -m http.server 8000
```

## Cookies

Google Tag Manager no está en el `<head>`: `js/script.js` lo inyecta solo si la persona acepta la analítica. La elección se guarda en `localStorage` (`plexiweb-es-cookie-consent`) y caduca a los 24 meses. "Aceptar" y "Rechazar" tienen el mismo peso visual y la analítica parte desactivada.

## Agregar un proyecto al portfolio

Añade otra `<a class="portfolio-card">` dentro de cualquier `.portfolio-col` de `index.html` (imagen en `assets/home/`). No hace falta tocar CSS ni JS.
