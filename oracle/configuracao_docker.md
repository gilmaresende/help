# Instalar Oracle Database no Docker

_Processo considera que já tenha o Docker instalado e executando em sua máquina!_

## Download

Para realizar a instalação do banco de dados Oracle deve-se entrar no GitHub e realizar o download dos arquivos docker-images-master.zip ou fazer um clone do repositório.

```
https://github.com/oracle/docker-images
```

O próximo passo é realizar o download do `Oracle Database 19c para Linux x86-64`:

_Independente do sistema que estiver usando, deve baixar para Linux, Docker executa um Linux no core!_

```
https://www.oracle.com/database/technologies/oracle-database-software-downloads.html
```

## Preparar ambiente

### Criando imagem

Após o download, copie o arquivo `LINUX.X64_193000_db_home.zip` para o diretório:

```
 .../docker-images/OracleDatabase/SingleInstance/dockerfiles/19.3.0/
```

Agora precisamos acessar o diretório onde esta o arquivo `buildDockerImage.sh`:

```
.../docker-images/OracleDatabase/SingleInstance/dockerfiles/
```

Para gerar a imagem, em um terminal neste diretório vamos executar o comando:

```
./buildDockerImage.sh -v 19.3.0 -e
```

Este comando começará o processo de criar a imagem do oracle para o docker, é um processo demorado, pode parecer que travou, mas realmente demorar para processar.

Quando o comando terminar, a ultima mensagem será algo assim:

```
Build completed in ${XY} seconds.
```

### Criando container e banco de dados

Em um terminal, com o comando abaixo, podemos ver as imagens disponiveis ao docker:

```
docker images
```

O resultado deverá mostrar um repository `oracle/database`, na mesma linha que este repository, vai ter um o `id` da imagem criada, precisaremos copiar este id.

Tendo este id, executaremos o comando:

```
docker  run --name ${nome_container} -p ${porta_acesso_ao_container}:${porta_interna_aplicacao_container} ${id_image}
```

O do nome_container, porta_acesso_ao_container, porta_interna_aplicacao_container, podemos alterar de acordo com nossa necessidade. O id_image é o id que foi identificado no comando anterior.

Exemplo de como o comando deve ser executado:

```
docker  run --name oracle19c -p 1521:1521 08f07eab6285
```

O processo de criação do container e instalação do banco de dados irá começar, esse processo pode demorar e parecer que esta travado em alguma % do processo, mas não cancele, é demorado mesmo.

## Definindo senha para o banco de dados

Para definir uma senha para o usuário `sysadm` devemos executar o comando abaixo:

```
docker exec ${nome_container} ./setPassword.sh ${nova_senha}
```

exemplo

```
docker exec oracle19c ./setPassword.sh A1b2c3
```

## Informações do banco de dados

Se verificarmos no terminal da instalação vamos encontrar informações sobre o banco de dados, como no modelo abaixo:

```
Database Information:
Global Database Name:ORCLCDB
System Identifier(SID):ORCLCDB
```

## Termino

Apos toda esta configuração o oracle estara rodando no container criado, preso ao terminal em aberto. Se fecharmos o terminal, encerraremos o processo do oracle.

Para executar o container sem vicnulo ao terminal após a instalação, execute o comando:

```
docker start  ${nome_container}
```

exemplo:

```
docker start oracle19c
```

### Uso

Para usar o banco de dados, apenas faça a configuração no SGDB de sua escolha e na aplicação que este o banco de dados!
