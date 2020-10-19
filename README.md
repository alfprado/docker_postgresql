# Docker PostgreSQL

## Roteiro de criação de um docker com PostgreSQL 

Crie um diretório onde será mapeado o volume do docker

```sudo mkdir -p /docker/volumes/postgres```

Faça um pull da imagem no docker hub

```sudo docker pull postgres```

Execute o container

```sudo docker run --name NOME_DO_CONTAINER -e POSTGRES_PASSWORD=postgres -d -p 5432:5432 -v $HOME/docker/volumes/postgres:/var/lib/postgresql/data NOME_DO_DATABASE```

## Para fazer um backup de um database no docker

Acesse o docker 

```sudo docker exec -it CONTAINER_ID bash```

Gere o arquivo de backup

```pg_dump -U postgres -d NOME_DO_DATABASE > ARQUIVO.sql```

Saia do docker

```exit```

Copie o arquivo para o host

```sudo docker cp 76fcbc37b8d8:/ARQUIVO.sql .```

## Para subir um backup de um database no docker

Copia o arquivo backup para dentro do container

```sudo docker cp ARQUIVO.dump CONTAINER_ID:/var/lib/postgresql/data```

Restaura o backup .dump

```sudo docker exec CONTAINER_ID pg_restore -U postgres -d NOME_DO_DATABASE /var/lib/postgresql/data/ARQUIVO.dump```

Restaura o backup .sql

```sudo docker exec CONTAINER_ID psql -U postgres -d NOME_DO_DATABASE -f /var/lib/postgresql/data/ARQUIVO.sql```
