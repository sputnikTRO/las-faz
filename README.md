# las Faz — sitio oficial

Sitio web estático (HTML + CSS + JavaScript vanilla, sin frameworks ni backend) para el artista musical **las Faz**. Mobile-first, blanco y negro, minimalista.

Tiene dos vistas en una sola página, sin recargar:

- **Home** — landing a pantalla completa con la portada del álbum *PESCANDO EN ALASKA* (clic → abre el streaming).
- **Shop** — tienda con el merch. El producto se compra vía **Mercado Pago** (clic → abre el link de pago en una pestaña nueva). No hay carrito ni cuentas de usuario: es un sitio estático.

---

## 1. Correr en local

No requiere instalación ni build. Dos opciones:

**Opción A — abrir el archivo directamente**

Haz doble clic en `index.html` (o ábrelo desde el navegador con `Archivo → Abrir`).

**Opción B — servidor estático simple** (recomendado, evita restricciones de algunos navegadores)

```bash
cd las-faz
python3 -m http.server 8000
```

Luego abre <http://localhost:8000> en el navegador.

---

## 2. Qué reemplazar (lo único que se edita)

### a) Imágenes — carpeta `assets/`

| Archivo            | Qué es                                   |
|--------------------|------------------------------------------|
| `assets/album.jpg` | Portada de *PESCANDO EN ALASKA* (cuadrada)|
| `assets/tshirt.jpg`| Foto de la playera / merch (cuadrada)    |

Sustituye los archivos manteniendo **el mismo nombre**. Idealmente cuadradas (1:1) y optimizadas para web (~1000–1500 px de lado, JPG).

> Las imágenes actuales son **placeholders** generados automáticamente. Reemplázalas por las reales antes de publicar.

### b) Nombre y precio del producto

En `index.html`, dentro del bloque `<a class="product product-buy" …>`:

```html
<p class="product-name">T-Shirt</p>
<p class="product-price">$000 MXN</p>
```

Cambia el texto del nombre y del precio.

### c) Constantes de configuración — al inicio del `<script>` en `index.html`

```js
const STREAMING_LINK   = "https://awal.uk/pescandoenalaksa";
const MERCADOPAGO_LINK = "PEGAR_AQUI_LINK_DE_PAGO";
const CONTACT_EMAIL    = "correo@placeholder.com";
const SOCIALS = {
  instagram: "#",
  tiktok:    "#",
  youtube:   "#",
  twitter:   "#"   // X / Twitter
};
```

- **`STREAMING_LINK`** — smart link del álbum (AWAL). Es a donde lleva la portada en Home.
- **`MERCADOPAGO_LINK`** — link de pago del producto. Se genera dentro de la app de **Mercado Pago**: *Herramientas para vender → Link de pago →* crear el link del producto y pegarlo aquí. Mientras diga `PEGAR_AQUI_LINK_DE_PAGO`, el botón de compra no llevará a ningún lado.
- **`CONTACT_EMAIL`** — correo real de contacto. Aparece como *mailto* en el footer.
- **`SOCIALS`** — URL de cada red social. Reemplaza cada `"#"` por el perfil real (abre el perfil y copia la URL del navegador).

### d) Agregar más productos (opcional, a futuro)

Duplica el bloque `<a class="product product-buy">…</a>` dentro de `.shop-grid`. El grid se acomoda solo (centrado con un item, en cuadrícula con varios) sin tocar el CSS.

---

## 3. Deploy en Cloudflare Pages

El sitio es 100% estático: **sin build, sin comando de compilación**.

1. **Sube el repo a GitHub** (crea un repo nuevo y haz `git push`).
2. En el panel de **Cloudflare Pages**, entra a **Workers & Pages → Create application → Pages → Connect to Git** y conecta tu repo de GitHub.
3. Configura el proyecto:
   - **Framework preset:** `None` (sitio estático).
   - **Build command:** *(vacío)*.
   - **Build output directory:** la raíz → `/`.
4. **Deploy.** Cloudflare publica el sitio. A partir de ahí, **cada `git push` vuelve a desplegar automáticamente**.

### Conectar un dominio propio (ej. `lasfaz.com`)

1. En el proyecto de Pages, ve a la pestaña **Custom domains → Set up a custom domain**.
2. Escribe el dominio (`lasfaz.com`) y sigue las instrucciones.
3. Cloudflare te indicará los **registros DNS** a configurar:
   - Si el dominio ya está en Cloudflare, los agrega casi automáticamente.
   - Si está en otro proveedor, copia los registros (CNAME / A) que te muestre Cloudflare al panel DNS de tu proveedor.
4. Espera la propagación (suele ser minutos) y el dominio quedará activo con HTTPS automático.

---

## Estructura del repo

```
las-faz/
├── index.html        # Todo el sitio (HTML + CSS + JS en un archivo)
├── assets/
│   ├── album.jpg     # Portada de PESCANDO EN ALASKA
│   └── tshirt.jpg    # Producto de merch
└── README.md
```
