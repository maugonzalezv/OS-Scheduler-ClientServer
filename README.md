# Sistema de Eventos y Scheduling OS - Funcionalidad Completa Detallada

## Descripción General

Este es un sistema distribuido complejo que combina conceptos de sistemas operativos, procesamiento de archivos, y simulación de algoritmos de planificación. El sistema implementa una arquitectura cliente-servidor que demuestra concurrencia real en el servidor y simulación visual de scheduling en el cliente.

## Arquitectura del Sistema

### 1. Servidor Central (`server.py`)

El servidor actúa como el núcleo del sistema, manejando múltiples responsabilidades:

#### Gestión de Conectividad

- **Socket TCP**: Escucha en `127.0.0.1:65432` para conexiones de clientes
- **Manejo de Múltiples Clientes**: Cada cliente se maneja en un hilo separado
- **Identificación Única**: Cada cliente recibe un ID único al conectarse
- **Tolerancia a Fallos**: Manejo robusto de desconexiones inesperadas

#### Sistema de Eventos

- **Suscripción por Eventos**: Los clientes pueden suscribirse a eventos específicos
- **Cola FIFO**: Cada evento mantiene una cola de clientes suscritos
- **Activación Manual**: Los eventos se activan manualmente desde la consola del servidor
- **Distribución Equitativa**: Los archivos se distribuyen entre clientes de manera equitativa

#### Procesamiento Real de Archivos

- **Concurrencia Configurable**: Cada cliente puede especificar:
  - **Modo**: `threads` (hilos) o `forks` (procesos)
  - **Cantidad**: Número de workers concurrentes
- **ThreadPoolExecutor/ProcessPoolExecutor**: Implementación real de concurrencia
- **Logging Detallado**: Registro completo en `server_processing.log`
- **Monitoreo de PIDs**: Tracking de procesos/hilos trabajadores

#### Extracción de Datos con Regex

- **Procesamiento de Texto**: Análisis de archivos `.txt` usando expresiones regulares
- **Extracción de Patrones**:
  - **Nombres**: Detección de nombres propios (ej: "John Smith", "Anna Karlsson")
  - **Fechas**: Múltiples formatos (textual y numérico)
  - **Lugares**: Lista de ciudades predefinidas en múltiples idiomas
  - **Conteo de Palabras**: Análisis estadístico del contenido
- **Manejo de Errores**: Recuperación robusta ante archivos corruptos

### 2. Cliente con Interfaz Gráfica (`client_gui.py`)

Una aplicación GUI completa desarrollada en Tkinter con funcionalidades avanzadas:

#### Interfaz de Usuario Avanzada

- **Tema Personalizado**: Esquema de colores profesional y consistente
- **Diseño Responsivo**: Interfaz adaptable con scroll automático
- **Navegación por Pestañas**: Organización lógica de funcionalidades
- **Validación de Entrada**: Controles robustos para entrada de datos

#### Gestión de Conexión

- **Configuración de Red**: IP y puerto configurables
- **Estado de Conexión**: Indicadores visuales del estado
- **Reconexión Automática**: Manejo de pérdida de conexión
- **Timeout Configurable**: Control de tiempos de espera

#### Configuración del Cliente

- **Modo de Procesamiento**: Selección entre hilos y procesos
- **Cantidad de Workers**: Control deslizante para configurar concurrencia
- **Aplicación en Tiempo Real**: Configuración se envía inmediatamente al servidor

#### Sistema de Suscripción a Eventos

- **Suscripción Múltiple**: Un cliente puede suscribirse a varios eventos
- **Gestión Visual**: Lista de eventos suscritos con opción de desuscripción
- **Notificaciones**: Alertas cuando se activan eventos

#### Simulación Visual de Scheduling

- **Algoritmos Implementados**:
  - **FCFS (First-Come, First-Served)**: Orden de llegada
  - **SJF (Shortest Job First)**: Trabajo más corto primero
  - **SRTF (Shortest Remaining Time First)**: Tiempo restante más corto
  - **Round Robin**: Quantum configurable
  - **HRRN (Highest Response Ratio Next)**: Mayor ratio de respuesta
  - **Prioridad No Preemptiva**: Basado en prioridades
- **Configuración de Parámetros**:
  - **Tiempo de Llegada**: Cuándo llega cada proceso
  - **Tiempo de Ráfaga**: Duración de ejecución del proceso
  - **Prioridad**: Para algoritmos basados en prioridad
  - **Quantum**: Para Round Robin

#### Visualización Avanzada

- **Tabla de Procesos**: Estado detallado de cada proceso
- **Diagrama de Gantt Animado**: Representación visual de la ejecución
- **Métricas de Rendimiento**:
  - **Tiempo de Turnaround**: Tiempo total desde llegada hasta terminación
  - **Tiempo de Espera**: Tiempo esperando en cola
  - **Fórmulas Mostradas**: Cálculos transparentes
  - **Promedios Calculados**: Estadísticas de rendimiento

### 3. Motor de Scheduling (`scheduler.py`)

Implementación académica de algoritmos de planificación:

#### Clase Base Abstracta

- **Interfaz Común**: Método `schedule()` estándar
- **Parámetros Estandarizados**: Cola de listos, tiempo actual, procesos en ejecución
- **Flexibilidad**: Soporte para algoritmos preemptivos y no preemptivos

#### Algoritmos Específicos

- **FCFS**: Implementación básica FIFO
- **SJF**: Selección por menor tiempo de ráfaga
- **SRTF**: Preempción basada en tiempo restante
- **Round Robin**: Quantum configurable con preempción por tiempo
- **HRRN**: Cálculo de ratio de respuesta dinámico
- **Prioridad**: Selección basada en prioridades numéricas

### 4. Modelo de Datos (`process.py`)

Representación completa de procesos para simulación:

#### Atributos del Proceso

- **Identificación**: PID único y nombre de archivo asociado
- **Tiempos**: Llegada, ráfaga, inicio, terminación
- **Estado**: New, Ready, Running, Terminated
- **Métricas**: Tiempo de espera, turnaround, ratio de respuesta
- **Metadatos**: Prioridad, tiempo de ráfaga restante

#### Funcionalidades

- **Representación Textual**: Métodos `__str__` y `__repr__`
- **Cálculos Automáticos**: Actualización de métricas
- **Fórmulas Documentadas**: Transparencia en cálculos

### 5. Extractor de Datos (`extractor_regex.py`)

Motor de procesamiento de texto con expresiones regulares:

#### Patrones de Extracción

- **Nombres Propios**: Regex para detectar nombres completos
- **Fechas Múltiples Formatos**:
  - Textuales: "12 de enero de 1945"
  - Numéricas: "12/03/1945", "1945-03-12"
  - Multiidioma: Español, inglés, sueco
- **Ubicaciones Geográficas**: Lista curada de ciudades
- **Análisis Estadístico**: Conteo de palabras y caracteres

#### Robustez

- **Manejo de Errores**: Recuperación ante archivos corruptos
- **Codificación**: Soporte UTF-8 con manejo de errores
- **Deduplicación**: Eliminación de duplicados automática
- **Ordenamiento**: Resultados ordenados alfabéticamente

## Flujo de Trabajo Completo

### 1. Inicialización del Sistema

1. **Servidor**: Se inicia y busca archivos `.txt` en `text_files/`
2. **Cliente**: Se conecta al servidor y recibe confirmación
3. **Configuración**: Cliente envía configuración de concurrencia
4. **Suscripción**: Cliente se suscribe a eventos específicos

### 2. Procesamiento de Archivos (Servidor)

1. **Activación de Evento**: Administrador activa evento desde consola
2. **Distribución**: Archivos se distribuyen equitativamente entre clientes
3. **Procesamiento Concurrente**:
   - Creación de ThreadPool/ProcessPool según configuración
   - Procesamiento paralelo de archivos
   - Extracción de datos con regex
   - Logging detallado de cada operación
4. **Consolidación**: Resultados se consolidan y envían al cliente

### 3. Simulación Visual (Cliente)

1. **Selección de Archivos**: Usuario selecciona archivos para simular
2. **Configuración de Parámetros**: Entrada manual de tiempos y prioridades
3. **Selección de Algoritmo**: Elección del algoritmo de scheduling
4. **Ejecución de Simulación**:
   - Inicialización de procesos
   - Ejecución paso a paso del algoritmo
   - Actualización de visualizaciones
   - Cálculo de métricas en tiempo real

### 4. Visualización y Análisis

1. **Tabla de Procesos**: Estado actual de cada proceso
2. **Diagrama de Gantt**: Representación visual temporal
3. **Métricas**: Cálculo de promedios y estadísticas
4. **Exportación**: Guardado de resultados en CSV

## Casos de Uso Específicos

### Caso 1: Análisis de Documentos Históricos

- **Escenario**: Procesamiento de testimonios históricos (como los archivos LS\_\*)
- **Funcionalidad**: Extracción de nombres, fechas y lugares mencionados
- **Concurrencia**: Procesamiento paralelo de múltiples documentos
- **Resultado**: Base de datos estructurada de información histórica

### Caso 2: Educación en Sistemas Operativos

- **Escenario**: Enseñanza de algoritmos de scheduling
- **Funcionalidad**: Simulación visual interactiva
- **Comparación**: Análisis de rendimiento entre algoritmos
- **Resultado**: Comprensión práctica de conceptos teóricos

### Caso 3: Análisis de Rendimiento

- **Escenario**: Comparación de concurrencia (hilos vs procesos)
- **Funcionalidad**: Medición de tiempos de procesamiento
- **Métricas**: Throughput, latencia, uso de recursos
- **Resultado**: Datos empíricos sobre rendimiento

## Características Técnicas Avanzadas

### Concurrencia y Paralelismo

- **Hilos (Threads)**: Compartición de memoria, menor overhead
- **Procesos (Forks)**: Aislamiento de memoria, mayor robustez
- **Pool Management**: Gestión eficiente de recursos
- **Load Balancing**: Distribución equitativa de trabajo

### Manejo de Errores

- **Excepciones Granulares**: Manejo específico por tipo de error
- **Recuperación Automática**: Continuación ante fallos parciales
- **Logging Comprensivo**: Registro detallado para debugging
- **Notificación al Usuario**: Feedback claro sobre errores

### Optimizaciones de Rendimiento

- **Lazy Loading**: Carga de datos bajo demanda
- **Caching**: Almacenamiento temporal de resultados
- **Batch Processing**: Procesamiento en lotes eficiente
- **Memory Management**: Gestión cuidadosa de memoria

### Escalabilidad

- **Multi-Cliente**: Soporte para múltiples clientes simultáneos
- **Configuración Flexible**: Adaptación a diferentes capacidades
- **Monitoreo de Recursos**: Vigilancia de uso de CPU y memoria
- **Throttling**: Control de carga para evitar sobrecarga

## Métricas y Análisis

### Métricas de Scheduling

- **Tiempo de Turnaround**: `Tiempo_Terminación - Tiempo_Llegada`
- **Tiempo de Espera**: `Tiempo_Turnaround - Tiempo_Ráfaga`
- **Tiempo de Respuesta**: `Tiempo_Primer_Ejecución - Tiempo_Llegada`
- **Ratio de Respuesta**: `(Tiempo_Espera + Tiempo_Ráfaga) / Tiempo_Ráfaga`

### Métricas de Rendimiento

- **Throughput**: Procesos completados por unidad de tiempo
- **CPU Utilization**: Porcentaje de tiempo de CPU ocupado
- **Fairness**: Distribución equitativa de recursos
- **Starvation**: Detección de procesos sin atención

## Configuración y Personalización

### Configuración del Servidor

- **HOST/PORT**: Dirección y puerto de escucha
- **TEXT_FILES_DIR**: Directorio de archivos de entrada
- **LOG_LEVEL**: Nivel de detalle en logs
- **MAX_CLIENTS**: Límite de clientes simultáneos

### Configuración del Cliente

- **SIMULATION_SPEED**: Velocidad de animación
- **COLORS**: Esquema de colores para visualización
- **EXPORT_FORMAT**: Formato de exportación de datos
- **AUTO_SAVE**: Guardado automático de configuraciones

### Personalización de Algoritmos

- **QUANTUM**: Tiempo de quantum para Round Robin
- **PRIORITY_LEVELS**: Niveles de prioridad disponibles
- **PREEMPTION_POLICY**: Política de preempción
- **AGING_FACTOR**: Factor de envejecimiento para evitar starvation

## Extensibilidad

### Nuevos Algoritmos de Scheduling

1. Heredar de `SchedulerBase`
2. Implementar método `schedule()`
3. Agregar a `AVAILABLE_SCHEDULERS`
4. Configurar parámetros específicos

### Nuevos Patrones de Extracción

1. Definir regex en `extractor_regex.py`
2. Agregar función de procesamiento
3. Integrar en `parse_file_regex()`
4. Actualizar formato de salida

### Nuevas Visualizaciones

1. Crear widget de visualización
2. Integrar con datos de simulación
3. Agregar a interfaz de pestañas
4. Configurar actualización en tiempo real

## Consideraciones de Seguridad

### Validación de Entrada

- **Sanitización**: Limpieza de datos de entrada
- **Validación de Tipos**: Verificación de tipos de datos
- **Rangos Permitidos**: Límites en valores numéricos
- **Escape de Caracteres**: Prevención de inyección

### Manejo de Archivos

- **Path Traversal**: Prevención de acceso a archivos no autorizados
- **Límites de Tamaño**: Control de tamaño de archivos
- **Codificación Segura**: Manejo robusto de encodings
- **Permisos**: Verificación de permisos de lectura

### Comunicación de Red

- **Timeout**: Límites de tiempo en comunicaciones
- **Buffer Overflow**: Prevención de desbordamiento
- **Denial of Service**: Protección contra ataques DoS
- **Validación de Protocolo**: Verificación de formato de mensajes

## Casos de Prueba

### Pruebas Unitarias

- **Algoritmos de Scheduling**: Verificación de correctitud
- **Extracción de Datos**: Validación de patrones regex
- **Modelo de Datos**: Integridad de estructura Process
- **Cálculos de Métricas**: Precisión matemática

### Pruebas de Integración

- **Cliente-Servidor**: Comunicación end-to-end
- **Concurrencia**: Comportamiento bajo carga
- **Manejo de Errores**: Recuperación ante fallos
- **Persistencia**: Guardado y carga de datos

### Pruebas de Rendimiento

- **Carga Múltiple**: Múltiples clientes simultáneos
- **Archivos Grandes**: Procesamiento de archivos extensos
- **Memoria**: Uso eficiente de recursos
- **Latencia**: Tiempos de respuesta

## Conclusión

Este sistema representa una implementación completa y educativa que combina:

- **Conceptos Teóricos**: Algoritmos de scheduling académicos
- **Implementación Práctica**: Concurrencia real con hilos/procesos
- **Visualización Interactiva**: Interfaz gráfica avanzada
- **Análisis de Datos**: Procesamiento inteligente de texto
- **Arquitectura Distribuida**: Sistema cliente-servidor robusto

El sistema es ideal para:

- **Educación**: Enseñanza de sistemas operativos
- **Investigación**: Análisis de algoritmos de scheduling
- **Procesamiento de Datos**: Extracción de información de texto
- **Demostración**: Conceptos de concurrencia y paralelismo
