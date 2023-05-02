# Como executar um servidor HTTP com Docker

Este é um guia para criar um container Docker que executa um servidor HTTP básico e retorna um arquivo HTML.

## Pré-requisitos

- Docker instalado na sua máquina

## Passo a passo

1. Crie um arquivo `Dockerfile` com o seguinte conteúdo:

```bash
FROM python:3
COPY index.html /usr/src/app/
WORKDIR /usr/src/app
EXPOSE 9898
CMD ["python", "-m", "http.server", "9898"]
```

2. Crie um arquivo `index.html` com o conteúdo que você deseja retornar. Certifique-se de colocá-lo no mesmo diretório que o arquivo `Dockerfile`.

3. Abra um terminal na pasta onde estão os arquivos `Dockerfile` e `index.html`.

4. Execute o comando o comando a baixo para criar a imagem Docker. Certifique-se de incluir o ponto loga após o Dockerfile.

```bash
docker build -f Dockerfile . -t nome_da_imagem
```

5. Execute o comando a baixo para iniciar o container. Isso mapeará a porta do host X para a porta Y do container.

```bash
docker run -d -p 9898:9898 -it --rm --name nome_do_container nome_da_imagem
```

6. Digite no terminal:

```bash
wget http://localhost:9898
```

7. Após executar o comando `wget localhost:80`, verifique se o arquivo index.html foi baixado corretamente executando o comando `cat index.html` e verificando se o conteúdo corresponde ao seu index.html.

## Personalização

- Para usar um arquivo HTML diferente, basta substituir o arquivo `index.html` pelo seu próprio arquivo.

- Para usar uma porta diferente, basta alterar as linhas `EXPOSE 9898` e `CMD ["python", "-m", "http.server", "9898"]` no arquivo `Dockerfile` para a porta desejada. Certifique-se de usar a mesma porta em ambos os locais.

- Para parar o container, execute o comando `docker stop <nome_do_container>` no terminal.
- Para listar todos os container, digite `docker ps`.