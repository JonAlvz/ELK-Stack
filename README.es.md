# Proyecto ELK Stack (Elasticsearch, Logstash, Kibana)

> También disponible en: [English](README.md)

Este proyecto implementa un stack ELK completo utilizando Docker Compose, configurado para procesamiento y visualización de datos. El stack incluye Elasticsearch, Logstash, Kibana, Filebeat y Metricbeat para proporcionar una solución completa de monitoreo y análisis de datos.

## Características

- **Elasticsearch 8.15.2**: Base de datos distribuida para búsqueda y análisis.
- **Logstash**: Procesamiento de datos.
- **Kibana**: Interfaz de visualización y exploración de datos.
- **Filebeat**: Recolección y envío de datos de logs.
- **Metricbeat**: Monitoreo de métricas del sistema y servicios.
- **Seguridad**: Autenticación TLS/SSL con certificados autogenerados.

## Requisitos previos

- Docker y Docker Compose
- Al menos 8GB de RAM disponible (recomendado)
- Puertos disponibles: 9204 (Elasticsearch) y 5604 (Kibana)

## Estructura del proyecto

```
.
├── .env                      # Variables de entorno y configuración
├── docker-compose.yml        # Configuración de servicios Docker
├── logstash.conf             # Configuración principal de Logstash
├── filebeat.yml              # Configuración de Filebeat
├── metricbeat.yml            # Configuración de Metricbeat
├── datos_logstash/           # Configuraciones adicionales de Logstash
│   ├── log_filter.conf       # Filtros para procesamiento de logs
│   ├── log_input.conf        # Configuración de entrada de datos
│   └── log_output.conf       # Configuración de salida de datos
└── logstash_ingest_data/     # Directorio para datos de ingesta
    └── logs.log              # Archivo de logs para procesamiento
```

## Configuración

> [!NOTE]
> Renombrar y modificar el `.env.example` a `.env`

El proyecto utiliza variables de entorno definidas en el archivo `.env`:

- `ELASTIC_PASSWORD`: Contraseña para el usuario elastic
- `KIBANA_PASSWORD`: Contraseña para el usuario kibana_system
- `STACK_VERSION`: Versión del stack ELK (actualmente 8.15.2)
- `CLUSTER_NAME`: Nombre del cluster de Elasticsearch
- `ES_PORT`: Puerto para Elasticsearch (9204)
- `KIBANA_PORT`: Puerto para Kibana (5604)
- `ES_MEM_LIMIT`, `KB_MEM_LIMIT`, `LS_MEM_LIMIT`: Límites de memoria para servicios

## Iniciar el stack

```bash
# Clonar el repositorio
git clone https://github.com/JonAlvz/ELK.git
cd ELK

# Iniciar los servicios
docker-compose up -d
```

## Acceso a los servicios

Una vez que los servicios estén en funcionamiento:

- **Kibana**: https://localhost:5604
  - Usuario: elastic
  - Contraseña: admin123 (o la configurada en .env)

- **Elasticsearch**: https://localhost:9204
  - Usuario: elastic
  - Contraseña: admin123 (o la configurada en .env)

## Procesamiento de datos

El proyecto está configurado para procesar dos tipos de datos:

1. **Datos de F1**: Información de carreras y eventos de Fórmula 1.
2. **Datos de RTVE**: Noticias y contenido multimedia.

Los datos se procesan a través de Logstash y se almacenan en Elasticsearch para su posterior análisis en Kibana.

## Funcionalidades específicas

- **Transformación de datos**: Procesamiento avanzado con Logstash para estructurar datos complejos
- **Monitoreo de Docker**: Metricbeat está configurado para recopilar métricas de contenedores Docker
- **Seguridad integrada**: Certificados SSL/TLS generados automáticamente

## Solución de problemas

- Si los servicios no inician correctamente, verifique los logs con `docker-compose logs -f`
- Asegúrese de tener suficiente memoria disponible para ejecutar todo el stack
- Compruebe que los puertos configurados (9204, 5604) no estén siendo utilizados por otras aplicaciones

## Licencia

Este proyecto utiliza la licencia básica de Elastic Stack.
