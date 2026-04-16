# Tarea3-BigData - Análisis de Residuos RBL Marzo 2026

## Código desarrollado para análisis en batch (Spark) y streaming (Kafka + Spark)

## Problema
Analizar los datos de residuos recogidos en RBL durante Marzo 2026 para identificar:
- Total de kilos recogidos por tipo de residuo (plástico, papel, vidrio, orgánico, metal)
- Total general de residuos recolectados
- Promedio de kilos por categoría
- Procesamiento en tiempo real de la llegada de residuos

## Dataset
Datos abiertos de Colombia - Residuos Recogidos RBL Marzo 2026
https://www.datos.gov.co/dataset/Datos-Residuos-Recogidos-RBL-Marzo-2026/ia8k-c39n/about_data

## Tecnologías
- Apache Spark (Batch y Streaming)
- Apache Kafka
- Python
- Máquina Virtual Ubuntu

## Descripción de la solución

### Procesamiento Batch (Spark)
Se desarrolló un análisis por lotes donde:
1. Se carga el archivo CSV con los datos históricos de residuos
2. Se muestra la estructura del dataset y los primeros registros
3. Se calculan estadísticas: suma total de kilos por tipo de residuo
4. Se obtiene el total general de residuos recolectados
5. Se calcula el promedio de kilos por cada categoría
6. Se cuenta el número de registros por tipo de residuo

### Procesamiento en Tiempo Real (Kafka + Spark Streaming)
Se implementó un sistema de streaming que:
1. Configura un topic en Kafka llamado "residuos"
2. Un productor en Python envía datos simulados (tipo de residuo, kilos)
3. Spark Streaming consume los datos del topic en tiempo real
4. Se calculan sumas acumuladas por tipo de residuo
5. Los resultados se actualizan en consola cada 2 segundos

## Archivos del proyecto

| Archivo | Descripción |
|---------|-------------|
| `analisis_residuos.py` | Código principal (batch + streaming) |
| `productor_residuos.py` | Generador de datos para Kafka |
| `README.md` | Documentación del proyecto |

## Ejecución

### 1. Iniciar Kafka:
```bash
sudo /opt/Kafka/bin/zookeeper-server-start.sh /opt/Kafka/config/zookeeper.properties &
sudo /opt/Kafka/bin/kafka-server-start.sh /opt/Kafka/config/server.properties &
/opt/Kafka/bin/kafka-topics.sh --create --bootstrap-server localhost:9092 --replication-factor 1 --partitions 1 --topic residuos
