# Solucionando problema de Blocksize com Hive 

- Resolvendo problemas de pequenos dados no HDFS

Sabemos que o Hadoop foi projetado para processar volumes de Big Data, sendo assim, o Bloczize do HDFS é de 128MB (https://hadoop.apache.org/docs/r2.6.0/hadoop-project-dist/hadoop-hdfs/hdfs-default.xml) 

Um cenário muito comum ainda é recebermos diariamente arquivos pequenos e cada arquivo pequeno inserido no HDFS consome um bloco de 128MB.

Existem muitas formas de resolvermos esse problema, mas apresentarei nessa PoC como resolvermos no Hadoop utilizando Hive.


