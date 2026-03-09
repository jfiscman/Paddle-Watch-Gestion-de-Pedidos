# 🕐 Paddle Watch — Sistema de Pedidos

Aplicación web de gestión de pedidos para **Paddle Watch**, construida como un único archivo HTML sin dependencias externas ni servidor. Funciona 100% en el navegador.

---

## ✨ Funcionalidades

### 📦 Catálogo de productos
- +200 modelos organizados por categoría: Caballero Análogo, Dama, Digital, Infantil, Unisex y más
- Cada producto muestra código, nombre, precio, material, diámetro, medida de muñeca y características
- Secciones colapsables con contador de modelos por categoría
- Búsqueda en tiempo real por nombre o código

### 🛒 Gestión de pedidos
- Agregar/quitar unidades de cada producto
- Resumen de pedido con subtotal y total
- Generación automática de mensaje de pedido formateado
- Envío directo por **WhatsApp** o **Email** con un clic

### 👥 Base de clientes (62.630 registros)
- Base de datos completa importada desde el sistema de gestión
- Campos: Nombre/Negocio, Código de cliente, Teléfono, CUIT, Condición de IVA
- **Autocompletado** al tipear el nombre del cliente en el formulario de pedido
- Navegación con teclado (↑↓ flechas, Enter, Escape)
- Búsqueda por nombre, código o CUIT

### 📋 Gestión de la base de clientes
- Agregar clientes manualmente
- **Importar desde Excel (.xlsx) o CSV** — detecta columnas automáticamente por encabezado
- **Exportar a CSV** para backup o edición en Excel
- Eliminar clientes individuales con confirmación
- Buscador interno con contador de resultados

---

## 🗂 Estructura del proyecto

```
paddle-pedidos/
└── paddle_pedidos.html    # Aplicación completa (archivo único, ~5 MB)
```

Todo está contenido en un solo archivo HTML que incluye:
- CSS con tema oscuro (dark mode)
- JavaScript con toda la lógica de la app
- Logo de Paddle en formato Base64 embebido
- Base de clientes completa pre-cargada

---

## 🚀 Cómo usar

1. Descargar `paddle_pedidos.html`
2. Abrirlo en cualquier navegador moderno (Chrome, Safari, Firefox)
3. No requiere instalación, servidor ni conexión a internet

> La base de clientes se guarda en el `localStorage` del navegador, por lo que los cambios (agregar/eliminar clientes vía importación) persisten entre sesiones en el mismo dispositivo.

---

## 📥 Formato para importar clientes

El archivo Excel o CSV debe tener una fila de encabezado. Las columnas se detectan automáticamente por nombre (no importa el orden):

| Columna esperada | Variantes reconocidas |
|---|---|
| Nombre | `nombre`, `negocio`, `razon`, `cliente` |
| Teléfono | `telefono`, `tel`, `celular`, `mail`, `contacto` |
| CUIT | `cuit`, `cuil` |
| Condición IVA | `iva`, `condicion`, `situacion` |
| Código | `codigo`, `cod`, `clave`, `id` |

---

## 🛠 Tecnologías

- HTML5 / CSS3 / JavaScript vanilla (sin frameworks)
- [SheetJS](https://sheetjs.com/) cargado dinámicamente para leer archivos Excel
- `localStorage` para persistencia de datos del cliente
- Diseño responsivo con tema oscuro

---

## 📌 Pendientes / Próximas mejoras

- [ ] Historial de pedidos
- [ ] Filtros por precio en el catálogo
- [ ] Notas internas por cliente
- [ ] Soporte multi-divisa (ARS / USD)
- [ ] Vista de impresión del pedido

---

*Desarrollado para uso interno de Paddle Watch.*
