# Documentación del Proyecto CRUD

## 1. Resumen

Este documento describe el proceso realizado para crear y configurar el proyecto CrudLab en Laravel utilizando el entorno WAMP. Además, se incluye la configuración de la base de datos, las migraciones y la generación del módulo CRUD para la administración de productos.

## 2. Entorno de trabajo

* Entorno local: WAMP
* Framework: Laravel
* Base de datos: MySQL
* Administrador de base de datos: phpMyAdmin
* Paquete utilizado: ibex/crud-generator

## 3. Desarrollo del proyecto

### 3.1 Creación del proyecto

Se creó una nueva aplicación Laravel llamada CrudLab dentro del directorio de trabajo de WAMP.

Comando utilizado:

```bash
composer create-project laravel/laravel Laboratorio-con-Crud-main
```

### 3.2 Configuración de la base de datos

Se configuró el archivo `.env` para establecer la conexión con MySQL. La base de datos `crudlab` fue creada previamente desde phpMyAdmin.

Configuración principal:

```env
DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=crudlab
DB_USERNAME=root
DB_PASSWORD=
```

### 3.3 Limpieza de caché de configuración

Después de modificar el archivo `.env`, se limpió la caché de configuración para que Laravel reconociera correctamente los nuevos parámetros.

```bash
php artisan config:clear
```

### 3.4 Creación del modelo y migración

Se generó el modelo `Product` junto con su migración para crear la estructura de la tabla principal.

```bash
php artisan make:model Product -m
```

### 3.5 Definición de la tabla products

En la migración se definieron los campos principales de la tabla `products`:

* descripcion
* precio
* stock
* created_at
* updated_at

### 3.6 Ejecución de migraciones

Se ejecutaron las migraciones para crear la tabla correctamente dentro de MySQL.

```bash
php artisan migrate:fresh
```

### 3.7 Instalación del generador CRUD

Para agilizar el desarrollo del sistema se instaló el paquete `ibex/crud-generator`.

```bash
composer require ibex/crud-generator --dev
```

### 3.8 Publicación de archivos del paquete

Se publicaron los archivos necesarios del paquete CRUD.

```bash
php artisan vendor:publish --tag=crud
```

### 3.9 Generación del CRUD de productos

Se generó automáticamente el CRUD de productos utilizando Bootstrap para la interfaz visual.

```bash
php artisan make:crud products
```

### 3.10 Configuración de rutas

Se agregó la ruta de recurso en `routes/web.php` para habilitar todas las operaciones CRUD.

```php
Route::resource('products', ProductController::class);
```

Esta ruta habilita automáticamente las acciones:

* index
* create
* store
* show
* edit
* update
* destroy

### 3.11 Integración en el dashboard

Se añadió un botón de acceso en el dashboard principal para redirigir al módulo de productos.

### 3.12 Ejecución del proyecto

Finalmente, se inició el servidor local para verificar el funcionamiento del sistema.

```bash
php artisan serve
```

## 4. Comandos utilizados durante el desarrollo

```bash
php artisan config:clear
php artisan migrate:fresh
php artisan vendor:publish --tag=crud
php artisan make:crud products
php artisan serve
```

## 5. Verificación del funcionamiento

Se comprobó que el sistema cumpliera correctamente con los siguientes puntos:

* Conexión exitosa a la base de datos `crudlab`.
* Creación correcta de la tabla `products`.
* Acceso al módulo de productos desde la interfaz.
* Funcionamiento completo de las operaciones CRUD:

  * Crear registros
  * Listar productos
  * Editar información
  * Eliminar registros

## 6. Consideraciones de operación

Todos los comandos de Laravel deben ejecutarse desde la terminal (CMD o PowerShell) ubicándose en la carpeta raíz del proyecto:

```bash
C:\wamp64\www\Laboratorio-con-Crud-main
```

Para acceder a la carpeta desde la terminal:

```bash
cd C:\wamp64\www\Laboratorio-con-Crud-main
```

Antes de ejecutar el proyecto, se debe verificar que los siguientes servicios de WAMP estén activos:

* Apache → necesario para el servidor web.
* MySQL → requerido para la base de datos.

Si el puerto por defecto se encuentra ocupado al ejecutar el servidor, se puede utilizar otro puerto:

```bash
php artisan serve --port=8001
```

Luego, el proyecto podrá visualizarse desde el navegador ingresando a:

```text
http://127.0.0.1:8001
```
