# Big_data_Engineer_Projeto_Final_Spark_Semantix

* Leitura da doc de instalação do [docker](https://docs.docker.com/engine/install/ubuntu/)

* Leitura da doc de instalação do [docker-compose](https://docs.docker.com/compose/install/)

* Leitura da [documentação do projeto](https://github.com/ronnanlimao/Big_data_Engineer_Projeto_Final_Spark_Semantix/blob/main/documentacao_projeto/projeto_final_spark.pdf)

* Anotações durante o curso [Anotações de Comandos](https://github.com/ronnanlimao/Big_data_Engineer_Projeto_Final_Spark_Semantix/blob/main/anotacoes_comandos/Comandos_BIGDATA_anotacoes.txt)

1 ) Criar diretorio do cluster big data nomeado "spark1"

```
mkdir /home/ronnan/spark1
```

2 ) Montando imagens dos containers docker e criar cluster bigdata
``` 
docker-compose -f docker-compose-parcial.yml up -d
docker-compose -f docker-compose-parcial.yml stop (caso seja necessario)
```

3 ) Copiando o arquivo jars para dentro do container spark, dependencia necessaria

3.1) Copiar o jars pra dentro da pasta do jupyter

```
docker cp parquet-hadoop-bundle-1.6.0.jar jupyter-spark:/opt/spark/jars
```

3.2) Verificar se o jars está dentro da pasta

```
docker exec -it jupyter-spark ls /opt/spark/jars | grep 'parquet-hadoop-bundle'
```

4 ) Link para baixar os arquivos que iremos trabalhar

https://mobileapps.saude.gov.br/esus-vepi/files/unAFkcaNDeXajurGB7LChj8SgQYS2ptm/04bd3419b22b9cc5c6efac2c6528100d_HIST_PAINEL_COVIDBR_06jul2021.rar

4.1) Fazer donwload do arquivo dentro do cluster no terminal

```
/home/ronnan/spark1/input/data_covid
```
```
curl -O https://mobileapps.saude.gov.br/esus-vepi/files/unAFkcaNDeXajurGB7LChj8SgQYS2ptm/04bd3419b22b9cc5c6efac2c6528100d_HIST_PAINEL_COVIDBR_06jul2021.rar
```

4.2) Extrair os arquivos para em seguia importa-los para dentro do HDFS

```
unrar x 04bd3419b22b9cc5c6efac2c6528100d_HIST_PAINEL_COVIDBR_06jul2021.rar
```

4.3) Enviar os dados para o HDFS

``` 
hdfs dfs -put input/data_covid/*csv /user/ronnan/data/data_covid
```

5 ) Para o projeto utilizamos os containers e comandos para acessar-los
```
docker exec -it namenode bash
docker exec -it hive-server bash
docker exec -it jupyter-spark bash
```
![Imagem containers rodando](https://github.com/ronnanlimao/Big_data_Engineer_Projeto_Final_Spark_Semantix/blob/main/containers_rodando.png)

6 ) Abrir o projeto dentro do container do jupyter-spark, atráves do navedador pelo endereço

https://localhost:8889

Abrir o arquivo ----> Projeto_final_spark.ipynb
