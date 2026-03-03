# EduGrade Global: Un enfoque de Persistencia Políglota para la Gestión Académica

## Descripción

Este proyecto surge de la necesidad de centralizar y estandarizar el historial académico de estudiantes provenientes de diversos sistemas educativos internacionales. El sistema permite interpretar y preservar calificaciones expresadas en formatos heterogéneos (A-Levels, GPA, escalas numéricas, etc.) conservando el contexto original y permitiendo conversiones automáticas trazables.

## Stack tecnológico

* Orquestación: Docker Compose
* Frontend: React + Vite + Tailwind + HeroUI
* Backend: Node.js + Express.
* Bases de Datos: MongoDB, Neo4j, Redis, Cassandra

## Casos de Uso por Tecnología

Para resolver los desafíos del dominio, se implementó una arquitectura de persistencia políglota donde cada motor cumple un rol específico:

- **MongoDB (Registro Flexible):** Se utiliza para almacenar los perfiles de estudiantes, instituciones y materias. Su modelo documental permite manejar la naturaleza heterogénea de los datos internacionales sin forzar un esquema rígido.

- **Neo4j (Trayectorias y Relaciones):** Se encarga de representar la red compleja de trayectorias académicas, correlatividades y equivalencias transnacionales. Permite realizar consultas de transitividad y recorridos de caminos de forma eficiente.

- **Redis (Conversión en Tiempo Real):** Almacena la matriz global de reglas de conversión en memoria para garantizar latencias sub-milisegundo durante los flujos operativos. También actúa como capa de caché para las normativas más consultadas.

- **Apache Cassandra (Auditoría y Analítica):** Utilizado para el registro de auditoría inmutable (append-only) y el almacenamiento de métricas agregadas sobre grandes volúmenes de datos. Soporta ráfagas de escritura masiva y consultas analíticas pre-calculadas.

## Inicialización del Proyecto

Siga estos pasos para configurar y ejecutar el entorno de desarrollo local.

### 1. Requisitos Previos

* Tener instalado Docker Desktop.  
* Node.js instalado para la gestión de dependencias locales.

### 2. Despliegue con Docker

Abrir Docker Desktop y desde la carpeta raíz del proyecto (tpo-edu-grade), ejecute el siguiente comando para levantar todos los servicios:

```bash
docker-compose up --build
```

### 3. Inicialización de Datos (Data Seeding)

Una vez que los contenedores estén activos, debe ejecutar los scripts de inicialización para poblar las bases de datos. Abra una nueva terminal en la raíz y ejecute:

```bash
# Configurar esquemas en Cassandra
docker-compose exec backend node src/scripts/setupCassandra.js

# Cargar datos iniciales (Estudiantes, Materias, Instituciones)
docker-compose exec backend node src/scripts/seedData.js

# Cargar reglas de conversión en Redis
docker-compose exec backend node src/scripts/seedRedis.js
```

### 4. Acceso al Sistema

Frontend: http://localhost:5173

## Reglas de conversión

Como ejemplo, para cargar nuevas versiones de reglas desde el frontend, utilice el JSON ubicado en la carpeta de utils del frontend.