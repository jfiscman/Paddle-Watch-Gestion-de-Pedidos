# PaddleWatch · Catálogo Interactivo de Vendedores

Catálogo digital offline-first para el equipo de ventas de PaddleWatch. Funciona como aplicación instalable en tablets y computadoras (PWA), sin necesidad de conexión a internet una vez instalado.

---

## Características

### Catálogo de Productos
- Grilla y lista de productos con imagen, SKU, precio y stock
- Búsqueda en tiempo real por nombre, SKU, descripción y tags
- Filtros por categoría, género y rango de precio
- Ordenamiento por nombre, precio ascendente/descendente
- 9 categorías: Smartwatch · Clásico · Alta Gama · Auriculares · Deportivo · Despertador · Promo 2×1 · Gift Card · Otros
- Ficha de producto con detalle completo

### Presupuestos
- Armado de presupuesto con múltiples productos
- Control de cantidades, descuento porcentual y notas
- SKU visible en cada ítem del presupuesto
- Vinculación de cliente desde la base de datos
- Exportar como **PDF** (imprimible), **WhatsApp** y **Email**

### Base de Clientes
- Búsqueda con autocompletar al armar un presupuesto
- Creación rápida de cliente desde el buscador
- Campos: Nombre · Teléfono · Email · CUIT · Dirección · Notas
- Importar desde CSV (compatible con Excel y Google Sheets)
- Exportar a CSV para backup
- Plantilla de ejemplo descargable

### Sincronización con Google Sheets
- El encargado actualiza precios, stock y productos en una planilla compartida
- Los vendedores sincronizan con un toque desde el catálogo
- Compatible con cualquier formato de URL de Google Sheets
- Columnas detectadas automáticamente (acepta nombres en español e inglés)

### Imágenes de Productos
- Soporte para imágenes hosteadas en GitHub Pages (recomendado)
- URL base configurable: solo se escribe el nombre del archivo en la planilla
- Fallback automático al emoji de categoría cuando no hay imagen o conexión

### Offline (PWA)
- Funciona sin internet una vez instalado
- Datos guardados en el dispositivo (localStorage)
- Imágenes cacheadas al primer uso con conexión
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
| 16011 | Smartwatch Negro | smartwatch | unisex | 175500 | | 4 | imagenes/sw-negro.jpg | Pantalla táctil... | bluetooth, llamadas |

**Categorías válidas:** `smartwatch` · `clasico` · `alta_gama` · `auriculares` · `deportivo` · `despertador` · `promo_2x1` · `gift_card` · `otros`

**Géneros válidos:** `mujer` · `hombre` · `unisex` · `nino`

### Pasos para conectar

1. Crear la planilla en Google Sheets (descargar la plantilla desde ⚙ Ajustes en el catálogo)
2. Ir a **Compartir → Cualquiera con el link puede ver**
3. En el catálogo: **⚙ Ajustes → pegar la URL del Sheet → Guardar**
4. Tocar **↻ Sincronizar** (o el botón dentro de Ajustes)

---

## Configuración de Imágenes

### Opción A — GitHub Pages (recomendada para uso con internet)

1. Crear una carpeta `imagenes/` en el repositorio
2. Subir las fotos de productos
3. En el catálogo: **⚙ Ajustes → URL base de imágenes:**
   ```
   https://jfiscman.github.io/Paddle-Watch-Gestion-de-Pedidos/imagenes
   ```
4. En la planilla, columna "Imagen URL": solo el nombre del archivo
   ```
   smartwatch-negro.jpg
   ```

### Opción B — Servidor local (para uso offline en PC/Mac)

Estructura de carpetas:
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

### Importar desde CSV

El archivo CSV puede exportarse desde Excel, Google Sheets o cualquier sistema de gestión. Las columnas son detectadas automáticamente.

**Columnas aceptadas:**

| Dato | Nombres de columna aceptados |
|------|------------------------------|
| Nombre | Nombre, name, cliente, empresa, razón social |
| Teléfono | Teléfono, tel, phone, celular, móvil |
| Email | Email, mail, correo |
| CUIT | CUIT, DNI, RUC, documento |
| Dirección | Dirección, address, domicilio, dir |
| Notas | Notas, notes, observaciones, comentarios |

Para ver el formato exacto: **👥 Clientes → 📄 Plantilla**

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

Todos los datos (productos, clientes, presupuestos) se guardan **localmente en el dispositivo** usando `localStorage` del navegador. No se envía ningún dato a servidores externos salvo:

- La sincronización con Google Sheets (lectura de la planilla configurada)
- La carga de imágenes desde GitHub Pages

---

## Soporte de Dispositivos

| Dispositivo | Estado |
|-------------|--------|
| Android (Chrome) | ✅ Instalable como app, offline completo |
| iPhone / iPad (Safari) | ✅ Agregar a pantalla de inicio |
| Windows (Chrome/Edge) | ✅ Instalable como app |
| macOS (Chrome/Safari) | ✅ Instalable como app |
| Cualquier navegador moderno | ✅ Funciona sin instalar |

---

*Desarrollado para el equipo de ventas de PaddleWatch · Argentina*
