

Documentación del Proyecto Crud
1. Resumen
Este documento describe el proceso realizado para crear y configurar el proyecto CrudLab en Laravel dentro del entorno WAMP, incluyendo la conexión a base de datos, migraciones y generación del módulo CRUD de productos.
2. Entorno de trabajo

Sistema local con WAMP
Framework: Laravel
Base de datos: MySQL
Gestor visual de BD: phpMyAdmin
Paquete de apoyo: ibex/crud-generator

3. Pasos realizados
3.1 Creación del proyecto
Se inició el proyecto creando una nueva aplicación Laravel llamada CrudLab dentro del entorno de trabajo de WAMP.
Comando de referencia:
composer create-project laravel/laravel Laboratorio-con-Crud-main
3.2 Configuración de base de datos
Se configuró el archivo .env para establecer la conexión con MySQL. La base de datos fue creada previamente en phpMyAdmin con el nombre crudlab.
Variables principales:
DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=crudlab
DB_USERNAME=root
DB_PASSWORD=
3.3 Limpieza de configuración en caché
Se limpió la caché de configuración para que Laravel reconociera los nuevos parámetros de conexión.
php artisan config:clear
3.4 Creación del modelo y migración
Se generó el modelo Product junto con su migración para estructurar la tabla principal del sistema.
php artisan make:model Product -m
3.5 Definición de la tabla products
En la migración se definieron los campos principales de la tabla products, incluyendo:

descripcion
precio
stock
Timestamps automáticos (created_at, updated_at)

3.6 Ejecución de migraciones
Se ejecutó la migración para crear correctamente la tabla dentro de la base de datos.
php artisan migrate:fresh
3.7 Instalación del generador CRUD
Para agilizar el desarrollo se instaló el paquete ibex/crud-generator.
composer require ibex/crud-generator --dev
3.8 Publicación de archivos del paquete
Se publicaron los archivos necesarios del paquete mediante:
php artisan vendor:publish --tag=crud
3.9 Generación del CRUD de productos
Se generó el CRUD de productos utilizando Bootstrap como tecnología para la interfaz visual.
php artisan make:crud products
3.10 Definición de rutas
Se agregó la ruta de recurso en routes/web.php para habilitar las operaciones CRUD:
Route::resource('products', ProductController::class);
Esto habilita automáticamente las acciones:

index
create
store
show
edit
update
destroy

3.11 Integración en dashboard
Se agregó un botón de acceso en el dashboard principal para redirigir al usuario al módulo de productos.
3.12 Ejecución del proyecto
Finalmente se inició el servidor para verificar el funcionamiento del sistema:
php artisan serve
4. Comandos útiles usados durante el desarrollo
php artisan config:clear
php artisan migrate:fresh
php artisan vendor:publish --tag=crud
php artisan make:crud products
php artisan serve
5. Verificación funcional esperada

Conexión correcta a la base de datos crudlab.
Tabla products creada en MySQL.
Módulo de productos disponible desde la interfaz.
Operaciones CRUD funcionando correctamente (crear, listar, editar y eliminar).

6. Nota de operación
Todos los comandos php artisan deben ejecutarse desde la terminal (CMD o PowerShell) dentro de la carpeta raíz del proyecto:
C:\wamp64\www\Laboratorio-con-Crud-main
Para navegar hasta esa ruta desde la terminal, utiliza:
cd C:\wamp64\www\Laboratorio-con-Crud-main
Asegúrate de que los siguientes servicios estén activos en WAMP antes de ejecutar cualquier comando:

Apache — necesario para el entorno web.
MySQL — requerido para la conexión a la base de datos.

Si al ejecutar php artisan serve obtienes un error de puerto ocupado, puedes especificar un puerto alternativo:
php artisan serve --port=8001
Luego accede al proyecto desde tu navegador en: http://127.0.0.1:8001
