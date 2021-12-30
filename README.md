# CONVERSÃO DISTÂNCIA

Esse repositório é referente ao código para gerar a imagem da aplicação escrita em Python + Flask que pertence ao desafio Docker da Formação Kubedev.

## Passos para criar a imagem:

**1- Indicar a versão da imagem do Python que usaremos para rodar a nossa aplicação.**

```docker
FROM python:3.8-slim-buster
```
**2-Informar o nosso diretório de trabalho na imagem.**

```docker
WORKDIR /app
```
**3-Copiar o arquivo requirements.txt que possui a versão das bibliotecas necessárias para rodar a nossa aplicação para dentro do nosso diretório de trabalho.**

```docker
COPY requirements.txt /app/requirements.txt
```
**4-Rodar o pip, gerenciador de pacotes do Python para instalar as bibliotecas descritas no arquivo requirements.txt.**

```docker
RUN pip install -r requirements.txt
```
**5-Copiar os arquivos da aplicação para dentro do diretório de trabalho da nossa imagem**

```docker
COPY . .
```
**6-Executar o comando para iniciar a nossa aplicação como um módulo flask e permitir que ela possa ser acessível via navegador.**

```docker
CMD [ "python3", "-m" , "flask", "run", "--host=0.0.0.0"]
```
**7-Expor a porta 5000 para que possamos ter uma porta de acesso a aplicação no navegador.**

```docker
EXPOSE 5000
```
Uma boa prática é criarmos um arquivo **.dockerignore** para descrevermos os arquivos que não desejamos copiar para dentro da nossa imagem. Para a nossa aplicação, o arquivo **.dockerignore** ficou com o seguinte conteúdo:

```docker
.git
.gitignore
README.md
Dockerfile
```
Para rodar um container a partir da nossa imagem. Podemos usar o seguinte comando:

```docker
docker container run -d -p 5000:5000 --name conversao-distancia <seu-repositorio>/conversao-distancia:<tag>
```
