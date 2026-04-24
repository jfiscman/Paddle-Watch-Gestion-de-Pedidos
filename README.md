# PaddleWatch · Catálogo Interactivo de Vendedores

Catálogo digital offline-first para el equipo de ventas de PaddleWatch. Funciona como aplicación instalable en tablets y computadoras (PWA), sin necesidad de conexión a internet una vez instalado.

---

## Características

### Catálogo de Productos
- Grilla y lista de productos con imagen, SKU, precio y stock
- Búsqueda en tiempo real por nombre, SKU, descripción y tags
- Filtros por categoría, género y rango de precio
- Ordenamiento por nombre, precio ascendente/descendente
- 8 categorías: Smartwatch · Clásico · Alta Gama · Auriculares · Deportivo · Despertador · Promo 2×1 · Otros
- Ficha de producto con detalle completo

### Presupuestos
- Armado de presupuesto con múltiples productos
- Control de cantidades, descuento porcentual y notas
- SKU visible en cada ítem del presupuesto
- Vinculación de cliente desde la base de datos
- Exportar como **PDF** (imprimible), **WhatsApp** y **Email**
- El PDF y WhatsApp incluyen todos los datos del cliente: nombre, CUIT, condición de pago, dirección y observaciones
- **Historial de presupuestos guardados**: guardar, reabrir y reenviar presupuestos anteriores sin perder el activo

### Base de Clientes
- Búsqueda con autocompletar al armar un presupuesto
- Creación rápida de cliente desde el buscador
- Campos: N° de Cliente · Nombre · Teléfono · Email · CUIT · Dirección · **Condición de pago** · Notas
- **Condición de pago** con tres opciones:
  - `x50` — Sin IVA / Exento
  - `x000` — IVA 10.5%
  - `100` — IVA 21%
- Importar desde CSV (compatible con Excel y Google Sheets)
- Exportar a CSV para backup
- Plantilla de ejemplo descargable (incluye columna de condición de pago)

### Imágenes de Productos
- **Carga directa desde el dispositivo** (recomendado para tablets Android): seleccionás las imágenes una sola vez, quedan guardadas en la app sin necesidad de conexión ni servidor
- Soporte para imágenes hosteadas en GitHub Pages o servidor local (PC/Mac)
- URL base configurable: solo se escribe el nombre del archivo en la planilla
- Fallback automático al emoji de categoría cuando no hay imagen

### Offline (PWA)
- Funciona sin internet una vez instalado
- Datos guardados en el dispositivo (localStorage + IndexedDB para imágenes)
- Imágenes cacheadas al primer uso con conexión o cargadas desde el dispositivo
- Banner de actualización automática cuando hay nueva versión disponible
- Instalable en Android, iOS, Windows y macOS

---

## Estructura del Proyecto

```
Paddle-Watch-Gestion-de-Pedidos/
├── index.html          → Catálogo completo (app principal)
├── manifest.json       → Configuración PWA (nombre, íconos, colores)
├── sw.js               → Service Worker (caché offline)
├── icons/
│   ├── icon-192.png    → Ícono para pantalla de inicio (Android)
│   ├── icon-512.png    → Ícono de alta resolución
│   └── favicon.png     → Favicon del navegador
└── imagenes/           → (opcional) Imágenes de productos locales
    ├── smartwatch-negro.jpg
    └── reloj-clasico.jpg
```

---

## Configuración Inicial

### 1. GitHub Pages (acceso desde cualquier dispositivo)

1. Subir todos los archivos al repositorio `jfiscman/Paddle-Watch-Gestion-de-Pedidos`
2. Ir a **Settings → Pages → Source → Deploy from branch → `main` → `/ (root)`**
3. En ~2 minutos el catálogo queda disponible en:

```
https://jfiscman.github.io/Paddle-Watch-Gestion-de-Pedidos/
```

### 2. Instalar en tablet Android

1. Abrir Chrome en la tablet
2. Navegar a la URL de GitHub Pages
3. Chrome muestra el banner **"Agregar a pantalla de inicio"**
   (o tocar los 3 puntos → **Instalar app**)
4. El catálogo queda instalado con el ícono de PaddleWatch

### 3. Servidor local (uso sin internet desde PC/Mac)

Desde la carpeta del proyecto, ejecutar en la terminal:

```bash
python3 -m http.server 8080
```

Luego abrir en el navegador:
```
http://localhost:8080/
```

---

## Configuración de Google Sheets

### Estructura de la planilla

| SKU | Nombre | Categoría | Género | Precio | Precio Original | Stock | Imagen URL | Descripción | Tags |
|-----|--------|-----------|--------|--------|----------------|-------|------------|-------------|------|
| 16011 | Smartwatch Negro | smartwatch | unisex | 175500 | | 4 | smartwatch-negro.jpg | Pantalla táctil... | bluetooth, llamadas |

**Categorías válidas:** `smartwatch` · `clasico` · `alta_gama` · `auriculares` · `deportivo` · `despertador` · `promo_2x1` · `otros`

**Géneros válidos:** `mujer` · `hombre` · `unisex` · `nino`

### Pasos para conectar

1. Crear la planilla en Google Sheets (descargar la plantilla desde ⚙ Ajustes en el catálogo)
2. Ir a **Compartir → Cualquiera con el link puede ver**
3. En el catálogo: **⚙ Ajustes → pegar la URL del Sheet → Guardar**
4. Tocar **↻ Sincronizar** (o el botón dentro de Ajustes)

---

## Configuración de Imágenes

### Opción A — Carga desde el dispositivo (recomendada para tablet Android)

Ideal para uso offline completo sin depender de internet:

1. En el catálogo: **⚙ Ajustes → Imágenes del catálogo → 📂 Seleccionar imágenes**
2. Elegir todas las imágenes de productos desde la galería o archivos de la tablet
3. Las imágenes quedan guardadas dentro de la app (IndexedDB) permanentemente
4. En la planilla, columna "Imagen URL": solo el nombre del archivo (ej: `smartwatch-negro.jpg`)

> El nombre del archivo debe coincidir exactamente con el valor en la planilla.

### Opción B — GitHub Pages (para uso con internet)

1. Crear una carpeta `imagenes/` en el repositorio
2. Subir las fotos de productos
3. En el catálogo: **⚙ Ajustes → URL base de imágenes:**
   ```
   https://jfiscman.github.io/Paddle-Watch-Gestion-de-Pedidos/imagenes
   ```
4. En la planilla, columna "Imagen URL": solo el nombre del archivo

### Opción C — Servidor local (para uso offline en PC/Mac)

```
Paddle-Watch-Gestion-de-Pedidos/
  index.html
  imagenes/
    smartwatch-negro.jpg
    reloj-clasico.jpg
```

URL base en Ajustes:
```
http://localhost:8080/imagenes
```

---

## Base de Clientes

### Condición de pago

Cada cliente puede tener asignada una condición de pago que aparece automáticamente en todos los presupuestos generados:

| Código | Descripción |
|--------|-------------|
| `x50`  | Sin IVA / Exento |
| `x000` | IVA 10.5% |
| `100`  | IVA 21% |

Se asigna desde la ficha del cliente o al importar el CSV.

### Importar desde CSV

El archivo CSV puede exportarse desde Excel, Google Sheets o cualquier sistema de gestión. Las columnas son detectadas automáticamente.

**Columnas aceptadas:**

| Dato | Nombres de columna aceptados |
|------|------------------------------|
| N° de cliente | N° de cliente, nro cliente, num cliente, clientnum |
| Nombre | Nombre, name, cliente, empresa, razón social |
| Teléfono | Teléfono, tel, phone, celular, móvil |
| Email | Email, mail, correo |
| CUIT | CUIT, DNI, RUC, documento |
| **Condición de pago** | Condición de pago, condicion de pago, cond pago, payment, iva |
| Dirección | Dirección, address, domicilio, dir |
| Notas | Notas, notes, observaciones, comentarios |

Para ver el formato exacto: **👥 Clientes → 📄 Plantilla**

---

## Historial de Presupuestos

Los presupuestos generados se pueden guardar para consultarlos o reenviarlos después:

1. Armar el presupuesto y completar los datos del cliente
2. Tocar **💾 Guardar presupuesto** en el panel lateral
3. Para ver los guardados: **📋 Historial** (en el panel lateral)

Desde el historial se puede:
- **📄 PDF** · **📱 WhatsApp** · **📧 Email** — reenviar sin reabrir
- **↩ Reabrir** — carga el presupuesto como activo para modificarlo
- **🗑 Eliminar** — borrarlo del historial

> Los presupuestos del historial incluyen un snapshot de los datos del cliente al momento de guardarlos, por lo que si el cliente cambia sus datos después, los presupuestos anteriores conservan la información original.

---

## Actualización del Catálogo

### Para el encargado (actualizar precios/stock)

1. Editar la planilla de Google Sheets
2. Los vendedores sincronizan tocando **↻ Sincronizar** en el catálogo

### Para el encargado (actualizar la app)

1. Modificar `index.html` y subir al repositorio de GitHub
2. En `sw.js`, incrementar el número de versión de caché:
   ```js
   const CACHE_NAME = 'pw-catalogo-v2';  // cambiar v1 → v2
   ```
3. GitHub Pages despliega automáticamente en ~2 minutos
4. Los vendedores verán el banner verde **"Nueva versión disponible → Actualizar"**

---

## Datos y Privacidad

Todos los datos (productos, clientes, presupuestos, imágenes) se guardan **localmente en el dispositivo** usando `localStorage` e `IndexedDB` del navegador. No se envía ningún dato a servidores externos salvo:

- La sincronización con Google Sheets (lectura de la planilla configurada)
- La carga de imágenes desde GitHub Pages (si se usa esa opción)

---

## Soporte de Dispositivos

| Dispositivo | Estado |
|-------------|--------|
| Android (Chrome) | ✅ Instalable como app, offline completo, carga de imágenes desde dispositivo |
| iPhone / iPad (Safari) | ✅ Agregar a pantalla de inicio |
| Windows (Chrome/Edge) | ✅ Instalable como app |
| macOS (Chrome/Safari) | ✅ Instalable como app |
| Cualquier navegador moderno | ✅ Funciona sin instalar |

---

*Desarrollado para el equipo de ventas de PaddleWatch · Argentina*
