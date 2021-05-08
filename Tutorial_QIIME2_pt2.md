## Hola a tod@s!

En esta clase utilizaremos el programa gratuito QIIME 2 para analizar y visualizar análisis de diversidad de muestras microbiológicas (arqueas, bacterias y hongos) usando sequencias de ADN en formato fastq.

QIIME es un programa que está en constante actualización, así que podrían ocurrir modificaciones en los comandos aquí presentados, por lo queden estar atentos a las nuevas actualizacione y reportes de bichos (bugs!).
Más información de QIIME en su [website](https://qiime2.org/).

---

## Continuamos con QIIME2

## Generar un árbol para los análisis de diversidad filogenética

QIIME realiza varios análisis de diversidad genética, incluyendo la diversidad genética de Faith y las matrices UniFrac ponderadas y no-ponderadas.
Este árbol se construye alineando todas nuestras secuencias, removiendo las posiciones altamente variables. Luego, QIIME usa FastTree para generar un árbol filogenético.

```
qiime phylogeny align-to-tree-mafft-fasttree \
  --i-sequences rep-seqs.qza \
  --o-alignment aligned-rep-seqs.qza \
  --o-masked-alignment masked-aligned-rep-seqs.qza \
  --o-tree unrooted-tree.qza \
  --o-rooted-tree rooted-tree.qza
```

Artefactos resultantes:

`aligned-rep-seqs.qza`

`masked-aligned-rep-seqs.qza`

`unrooted-tree.qza`

`rooted-tree.qza`
