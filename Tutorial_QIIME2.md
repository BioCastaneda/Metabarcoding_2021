## Hola a tod@s!

En esta clase utilizaremos el programa gratuito QIIME 2 para analizar y visualizar análisi de diversidad de muestras microbiológicas (arqueas, bacterias y hongos) usando sequencias de ADN en formato fastq.

QIIME es un programa que está en constante actualización, así que podrían ocurrir modificaciones en los comandos aquí presentados, por lo queden estar atentos a las nuevas actualizacione y reportes de bichos (bugs!).
Más información de QIIME en su [website](https://qiime2.org/).

---

## ¿Qué es QIIME 2?
QIIME 2 es una pipeline análisis de diversidad microbiológica. QIIME 2 permite analizar secuencias "single-end" y "paired-end", asociarlas a muestras específicas, realizan control de calidad y filtrado de las secuencias, asignar taxonomía a las secuencias, obtener datos de abundancia de cada una de las secuencias y taxones asignados en cada una de las muestras analizadas (matriz de abundancia), generar árboles filogenéticos, y analizar diversidades alfa y beta.

## ¿Qué es lo que necesitamos para usar QIIME 2?

1. **Instalar el programa**
Existen diferentes formas de instalar QIIME2 dependiendo si lo van a instalar de forma nativa o usando máquinas virtuales. Las instrucciones las pueden encontrar [aquí](https://docs.qiime2.org/2021.4/install/)

2. **Un archivo metadata**
	* Este es un archivo tab-limitado que contiene toda las información de la secuenciación y las muestras. Puedes crear este archivo en excel, pero debes guardarlo como una version de texto. Aquí abajo puder ver el archivo de metadatos (normalmente nombrado como "mapping file").
	
	![Ejemplo de metadata](https://github.com/lecastaneda/Metabarcoding_2021/blob/main/metadata.png)

3. ** Archivo R1.fastq 
	* Este archivo contiene las lecturas "forward" entregadas por el secuenciador.
	
4. ** Archivo R2.fastq 
	* Este archivo contiene las lecturas "forward" entregadas por el secuenciador.	


## Manos a la obra!

1. Conectarse al servidor

`ssh -Y bioinfo1@genoma.med.uchile.cl`

2. Activar las versión 2019.4 de QIIME que está instalada en el servidor. La última versión disponible es la 2021.4

`source activate qiime2-2019.4`

3. Vayan a su carpeta de personal y creen una carpeta para el práctico e ir a ella.
Llamaremos a la carpeta "qiime2-atacama-soil" porque analizaremos la microbiota asociada a muestras de suelo obtenidas en el Desierto de Atacama.

`mkdir qiime2-atacama-soil`

`cd qiime2-atacama-soil`

## Descarga de datos

1. Descargaremos el archivo que contiene la [metadata](https://docs.google.com/spreadsheets/d/1LY3_jcLu0NeA-4jiP-7iuQQ7NCa9blAZHMgck_hyOEk/edit?usp=sharing), pero antes le daremos una mirada para ver cómo está estructurado.

2. Ahora si lo descargamos directo en nuestra carpeta.

`wget -O "sample-metadata.tsv" "https://data.qiime2.org/2021.4/tutorials/atacama-soils/sample_metadata.tsv"`

3. Ahora vamos a descargar las secuencias: forward = R1, reverse = R2, y los códigos de barras (barcodes), pero antes crearemos una carpeta y descargaremos las secuencias en ella.

`mkdir emp-paired-end-sequences`

Descargamos las secuencias R1

`wget -O "emp-paired-end-sequences/forward.fastq.gz" "https://data.qiime2.org/2021.4/tutorials/atacama-soils/10p/forward.fastq.gz"`

Descargamos las secuencias R1

`wget -O "emp-paired-end-sequences/reverse.fastq.gz" "https://data.qiime2.org/2021.4/tutorials/atacama-soils/10p/reverse.fastq.gz"`

Descargamos las secuencias de códigos de barras

`wget -O "emp-paired-end-sequences/barcodes.fastq.gz" "https://data.qiime2.org/2021.4/tutorials/atacama-soils/10p/barcodes.fastq.gz"`

## Comandos de análisis

1. QIIME 2 crea estos artefactos, los cuales contienen información acerca del tipo y procedencia de los datos. Así que lo primero que debemos hacer es crear un artefacto para analizar las secuencias. 
El tipo de artefacto que vamos a crear es EMPairedEndSequence si tenemos lecturas R1 y R2. Este tipo de artefacto contiene secuencias que están multiplexadas, es decir, que las secuencias no han sido asignadas a cada una de las muestras. El proceso de asignar las secuencias a las respectivas muestras se llama demultiplexar y para esto requerimos un archivo con las secuencias de los códigos de barras, los cuales son únicos para cada muestra.
Para este ejemplo en específico vamos a trabajar con secuencias EMPairedEndSequence, que quiere decir que están formateadas según el Earth Microbiome Project (EMP). Para ver cómo se pueden importar otros tipos de secuencias, revisa el [tutorial para importar data](https://docs.qiime2.org/2021.4/tutorials/importing/)

`qiime tools import \
   --type EMPPairedEndSequences \
   --input-path emp-paired-end-sequences \
   --output-path emp-paired-end-sequences.qza`

SSS

