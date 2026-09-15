# Distribuidora--Control-Stock
# 📦 Distribuidora — Control de Stock

> **⚠️ Nota sobre el código fuente:** Para proteger la propiedad intelectual, los derechos de autor y el modelo de negocio, el código fuente de este proyecto se mantiene en un **repositorio privado**. En este espacio público se detalla su documentación, arquitectura, decisiones técnicas y manual de usuario.

Una aplicación de escritorio robusta y ligera diseñada para gestionar el inventario de distribuidoras y comercios. Permite administrar el stock, registrar compras/ventas y visualizar el inventario en tiempo real. **Funciona 100% offline y no requiere instalación de software adicional.**

---

## 🛠️ Arquitectura y Estructura del Sistema

El sistema está desarrollado en **Python 3.9+** utilizando la biblioteca nativa para la interfaz gráfica y **SQLite** para la persistencia de datos. Se compone de tres módulos principales:

*   `interfaz.py`: El punto de entrada de la aplicación. Gestiona la ventana principal, eventos de usuario y vistas.
*   `db.py`: El motor del sistema. Se encarga de la conexión, creación automática de la base de datos (`stock.db`) y la ejecución de consultas SQL seguras.
*   `cargar_datos_demo.py`: Módulo opcional para poblar la base de datos con productos de prueba y facilitar demostraciones.

---

## ✨ Características Principales y Funcionamiento

### 1. Gestión Integral de Inventario
*   **Alta de Productos:** Registro con nombre, precio de compra, precio de venta, stock inicial y **stock mínimo** configurable (umbral de alerta).
*   **Control de Flujo:** Al registrar compras el stock se incrementa automáticamente; al registrar ventas se reduce. El sistema bloquea ventas si el stock disponible es insuficiente.
*   **Interfaz Dinámica:** Tabla general con buscador en vivo, ordenamiento por columnas y alertas visuales en rojo para productos que alcanzaron su stock mínimo. Doble clic abre edición rápida.

### 2. Venta Rápida por Código de Barras (Plug & Play)
*   Diseñado para funcionar con cualquier lector de códigos de barras USB del mercado sin necesidad de instalar drivers o configurar código adicional. 
*   Resta stock al instante con un solo escaneo y acumula los datos en un resumen de sesión activo.

### 3. Historial Inteligente y Modificaciones Seguras
*   **Filtro por Años Dinámico:** Para evitar la degradación del rendimiento visual al cargar miles de registros, la tabla muestra por defecto el año actual. Los nuevos años se añaden solos al historial con el primer movimiento.
*   **Anulación con Trazabilidad:** Los movimientos no se borran de la base de datos. Al anular, el stock se reajusta, el registro original se tacha y se crea un nuevo movimiento de "Anulación" para mantener una auditoría limpia.

### 4. Seguridad y Resiliencia de Datos
*   **Respaldos Manuales:** Botón accesible desde cualquier pantalla para exportar copias a pendrives o nubes (Google Drive, OneDrive, etc.).
*   **Respaldos Automáticos:** Al cerrar la app, realiza un backup silencioso en la carpeta `/backups`. Aplica una política de rotación automática conservando solo las últimas 10 copias para optimizar el almacenamiento.

---

## ⚙️ Mantenimiento y Solidez Técnica

Detrás de la interfaz, el sistema cuenta con optimizaciones diseñadas para asegurar un ciclo de vida largo y sin errores:

*   **Rutas Absolutas a Prueba de Fallos:** La base de datos, los logs y los backups se generan siempre en relación al directorio del ejecutable. El programa no se rompe si se ejecuta desde accesos directos o rutas inusuales.
*   **Optimización de Base de Datos:** Cada vez que la app se cierra, ejecuta un comando `VACUUM` para compactar y desfragmentar el archivo `stock.db`.
*   **Manejo de Errores Silencioso:** Si un backup automático falla (por ejemplo, por disco lleno), se registra en `distribuidora_errores.log` y la interfaz muestra de forma clara la fecha del último backup exitoso.
*   **Indexación SQL:** La base de datos cuenta con índices específicos para mantener las consultas de historial rápidas a lo largo de los años.
*   **Localización:** Formato de moneda e importes adaptado al estándar argentino (`$1.500,00`).

---

## 📈 Próximos Pasos (Roadmap)
- [ ] Módulo de exportación de inventario a formatos Excel (.xlsx) y CSV.
- [ ] Panel de reportes financieros y cálculo de ganancias netas (`Precio Venta - Precio Compra`) por períodos de tiempo.
- [ ] Implementación de categorías de productos y gestión de múltiples usuarios con permisos.

---
📫 **Contacto:** Si sos reclutador o cliente y estás interesado en conocer más sobre la lógica interna del código fuente o adquirir una solución similar, no dudes en contactarme a través de mis canales de comunicación en mi perfil de GitHub.
