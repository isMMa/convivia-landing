# Landing de Convivia

Landing estática (sin build, sin frameworks) optimizada para SEO, lista para GitHub Pages.

## Estructura
```
index.html          → versión en español (idioma por defecto)
en/index.html        → versión en inglés
assets/style.css      → estilos
assets/main.js         → menú móvil
sitemap.xml            → mapa del sitio (ES + EN con hreflang)
robots.txt             → permite indexación, apunta al sitemap
CNAME                 → dominio personalizado (convivia.devodelight.com)
```

## Desplegar en GitHub Pages
1. Crea un repositorio nuevo (o usa uno existente) y sube todos estos archivos a la raíz de la rama `main`.
2. En GitHub → Settings → Pages, selecciona "Deploy from a branch" → rama `main` → carpeta `/root`.
3. En tu proveedor DNS, crea un registro **CNAME** apuntando `convivia` (subdominio) a `<tu-usuario>.github.io`.
   - El archivo `CNAME` ya incluido en este proyecto configura automáticamente el dominio personalizado en GitHub Pages; no lo borres.
4. Espera a que el certificado HTTPS se emita (unos minutos) y activa "Enforce HTTPS" en Settings → Pages.

## Antes de publicar — pendientes recomendados
- **Imagen Open Graph**: las etiquetas `og:image`/`twitter:image` apuntan a `assets/og-image.png`, que aún no existe. Genera una imagen de 1200×630px (puedes usar una captura real de la app) y guárdala en `assets/og-image.png`.
- **Favicon**: se usa un icono SVG generado en línea (la "C" verde). Si quieres un icono más elaborado, sustitúyelo por un archivo real y añade el `<link rel="icon">` correspondiente.
- **Enlace a App Store**: no encontré una versión de Convivia en iOS. En cuanto exista, añade el enlace en el hero y en el footer de ambos idiomas.
- **Google Search Console**: da de alta el dominio, envía `sitemap.xml` y verifica la propiedad.

## Por qué esta landing está optimizada para SEO
- HTML semántico (un único `<h1>`, jerarquía de encabezados correcta, `<details>/<summary>` nativos para el FAQ sin JavaScript).
- `title` y `meta description` únicos por idioma, ambos con las palabras clave reales del producto (alquiler de habitaciones, pisos compartidos).
- `hreflang` cruzado ES/EN + `x-default`, y páginas 100% estáticas por idioma (nada de contenido inyectado por JS, que Google indexa peor).
- Datos estructurados JSON-LD: `MobileApplication` y `FAQPage` (esto último puede generar rich snippets de preguntas frecuentes en Google).
- `sitemap.xml` con anotaciones `hreflang` y `robots.txt` apuntando a él.
- Cero frameworks, cero peticiones innecesarias: cero JavaScript salvo un menú móvil de 15 líneas, iconografía en SVG inline (sin imágenes que descargar), una sola fuente externa (Google Fonts) con `preconnect`. Esto favorece Core Web Vitals (LCP/CLS), que es señal de ranking.
- `rel="noopener"` en enlaces externos, contraste de color accesible y foco visible (accesibilidad también pesa indirectamente en SEO vía experiencia de usuario).
