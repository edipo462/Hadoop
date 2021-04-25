# Solucionando problema de Blocksize com Hive 

- Resolvendo problemas de pequenos dados no HDFS

Sabemos que o Hadoop foi projetado para processar volumes de Big Data, sendo assim, o Bloczize do HDFS é de 128MB (https://hadoop.apache.org/docs/r2.6.0/hadoop-project-dist/hadoop-hdfs/hdfs-default.xml) 

Um cenário muito comum ainda é recebermos diariamente arquivos pequenos e cada arquivo pequeno inserido no HDFS consome um bloco de 128MB.

Existem muitas formas de resolvermos esse problema, mas apresentarei nessa PoC como resolvermos no Hadoop utilizando Hive.

Na imagem abaixo, temos muitos arquivos parquet consumindo um bloco de 128MB, isso a longo prazo gerará um problema de performance e espaço em disco.

![image](https://user-images.githubusercontent.com/50892034/116010879-17850c80-a5f8-11eb-99b3-004615ec04f0.png)

Há uma maneira de resolvermos isso utilzando o Hive para realizar um merge desses arquivos.

Primeiro vamos copiar o nosso arquivo de cadastro no HDFS

![image](https://user-images.githubusercontent.com/50892034/116011016-038dda80-a5f9-11eb-944e-0cb65ef63ac0.png)

Após a criação do arquivo, seguir os passos abaixo no Hive.

![image](https://user-images.githubusercontent.com/50892034/116011050-549dce80-a5f9-11eb-857a-2451e273e19e.png)

Pronto!!! O cenário para o problema está criado, cada vez que houver uma rotina para inserir os dados em uma tabela parquet e os dados forem poucos, vamos consumir pouco por bloco no HDFS, vide primeira imagem.

Para a solução desse problema criei o step abaixo, com ele podemos criar uma rotina semanal/mensal para reorganização dos blocos de tal modo que nao impacte o usuário final:


![image](https://user-images.githubusercontent.com/50892034/116011127-d1c94380-a5f9-11eb-8a05-3f4b54657194.png)

Apos o final da rotina acima, temos que limpar o HDFS:

![image](https://user-images.githubusercontent.com/50892034/116011150-ef96a880-a5f9-11eb-8cdd-c9735a5f6aaf.png)

Após Rotina acima, os arquivos foram agrupados em um só bloco no HDFS:

![image](https://user-images.githubusercontent.com/50892034/116011260-75b2ef00-a5fa-11eb-805b-82b2a2f02787.png)

Os scripts e dados utilizados estao anexos...

abraços.

