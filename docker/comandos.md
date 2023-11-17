## Container

- Executar container existente

```
 docker run -d -p 3000:3000 --name
```

### Build Projeto em Imagem

Executar o comando no diretorio onde esta o arquivo `Dockerfile`

```
docker build -t ${nome_imagem} .
```

```
docker build -t phpmessages .
```

### Remover container ao para

Este comando executa o container e prepara para quando o stop ocorrer, ele sejá removido!

- Estrutura

```
docker run -d -p ${porta_pc}:${porta_interna_container} --name ${nome_container} --rm ${nome_imagem}
```

- Exemplo

```
docker run -d -p 3000:3000 --name meu_container --rm minha_imagem
```

### Copiar arquivos entre PC/Container e Container/PC

- Estrutura

```
docker cp ${nome_container}:/${caminho_arquivo/arquivo} ./${caminho_destino}
```

- Exemplo

```
docker cp meu_container:/app/arquivo.js ./pasta_destino/
```

### Informações sobre Container

- Estrutura

```
docker top ${nome_container}
```

- Exemplo

```
docker top meu_container
```

### Inspecionar Container

- Estrutura

```
docker inspect ${nome_container}
```

- Exemplo

```
docker inspect meu_container
```

### Informações consumo docker

- Estrutura e Estrutura

```
docker stats
```

### Ver volumes

```
docker volume ls
```

### Executar volumes Nomeados

exemplo

```
docker run -d -p 80:80 --name msgV2 -v ${nome_volume}:${diretorio_dentro_container} --rm phpmesssages
```

exemplo

```
docker run -d -p 80:80 --name msgV2 -v vmsgV2:/var/www/html/messages --rm phpmesssages:v1
```

### Bind mounts

```
docker run -d -p 80:80 --name msg1 -v ${diretorio_volume_host}:${diretorio_volume_container} --rm phpmesssages:v1
```

exemplo

```
docker run -d -p 80:80 --name msg1 -v C:/data-gf/projetos/help/projetos/volumes/messages:/var/www/html/messages --rm phpmesssages:v1
```

### Bind mounts para a Aplicação

```
docker run -d -p 80:80 --name msg1 -v ${caminho_raiz_projeto_host}:${caminho_raiz_projeto_container} --rm phpmesssages:v1
```

exemplo

```
docker run -d -p 80:80 --name msg1 -v C:/data-gf/projetos/help/projetos/volumes/:/var/www/html/ --rm phpmesssages:v1
```

### inspecionar volume

```
$ docker volume inspect vmsgV2
```

### remover volume

```
docker volume rm volumeTeste
```

### criar volume manual

```
docker volume create ${nome_volume}
```

exemplo

```
docker volume create volume_teste_1
```

### removendo todos os volumes não usados (Cuidado)

```
docker volume prune -a
```

### criando volume apenas leitura

deve ter o dois ponto ro no final do caminho do volume

```
docker run -d -p 80:80 --name msg1 -v volLeitura:/var/www/html/html:ro --rm phpmesssages:v1
```
