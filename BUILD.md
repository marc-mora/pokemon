# Guía de Build - Pokemon Web App

Este documento describe cómo construir y ejecutar el proyecto Pokemon Web App.

## Requisitos Previos

- Docker
- Docker Compose

## Estructura del Proyecto

```
pokemon/
├── Dockerfile              # Configuración de contenedor PHP + Apache
├── docker-compose.yml      # Orquestación de servicios
├── pokewebapp.sql         # Base de datos inicial
├── php/                   # Scripts PHP backend
├── html/                  # Páginas web
├── css/                   # Hojas de estilo
├── js/                    # JavaScript
└── img/                   # Imágenes
```

## Servicios

El proyecto incluye 3 servicios:

1. **web** - Servidor PHP + Apache (puerto 8080)
2. **db** - MySQL 8.0 (puerto 3306)
3. **phpmyadmin** - Administrador de base de datos (puerto 8081)

## Instrucciones de Build

### 1. Construir las imágenes

```bash
docker compose build
```

### 2. Iniciar los servicios

```bash
docker compose up -d
```

### 3. Importar la base de datos

```bash
docker exec -i mysql_db mysql -uroot -p12345 Pokewebapp < pokewebapp.sql
```

### 4. Verificar que todo funciona

- Aplicación web: http://localhost:8080
- PhpMyAdmin: http://localhost:8081
  - Usuario: root
  - Contraseña: 12345

## Comandos Útiles

### Ver logs
```bash
docker compose logs -f
```

### Detener servicios
```bash
docker compose down
```

### Reiniciar servicios
```bash
docker compose restart
```

### Eliminar todo (incluyendo volúmenes)
```bash
docker compose down -v
```

## Configuración de Base de Datos

- Host: db
- Database: Pokewebapp
- Usuario: root
- Contraseña: 12345
- Puerto: 3306

## Notas

- Los archivos del proyecto se montan en `/var/www/html` dentro del contenedor
- Los cambios en el código se reflejan inmediatamente (sin necesidad de rebuild)
- La base de datos persiste en un volumen Docker
