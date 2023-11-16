# Docker Compose e Scripts para Gerenciar um Contêiner Jupyter
### Docker Compose (docker-compose.yml)
O Docker Compose é uma ferramenta que permite definir e gerenciar aplicativos Docker multi-contêiner em um único arquivo, chamado docker-compose.yml. Neste caso, utilizaremos o Docker Compose para criar um ambiente contendo o Jupyter Notebook com Python e Anaconda.

Aqui está o conteúdo do arquivo docker-compose.yml:
```
  version: '3'
  services:
    jupyter:
      image: continuumio/anaconda3:latest
      ports:
        - "8888:8888"
      volumes:
        - ./notebooks:/opt/notebooks
      environment:
        - JUPYTER_ENABLE_LAB=yes
      command: ["jupyter", "lab", "--ip='0.0.0.0'", "--port=8888", "--no-browser", "--allow-root", "--NotebookApp.token=''", "--NotebookApp.password=''"]
```

#### Explicação dos principais elementos:

- version: '3': Indica a versão do formato do arquivo Docker Compose. No exemplo, utilizamos a versão 3.

- services: Define os serviços que compõem a aplicação. No caso, temos apenas o serviço jupyter.
    jupyter:
      image: continuumio/anaconda3:latest: Indica a imagem do Docker que será utilizada, neste caso, a última versão do Anaconda com Python 3.
      ports: Mapeia a porta do host (8888) para a porta do contêiner (8888), permitindo acessar o Jupyter Notebook pelo navegador.
      volumes: Mapeia um diretório local (./notebooks) para um diretório dentro do contêiner (/opt/notebooks), permitindo persistência dos notebooks.
      environment: Configura variáveis de ambiente, como JUPYTER_ENABLE_LAB, que habilita o Jupyter Lab.
      command: Especifica o comando que será executado quando o contêiner iniciar. Neste caso, iniciamos diretamente o Jupyter Lab com as configurações desejadas.

#### Scripts para Subir e Desligar o Contêiner
Aqui estão os scripts para subir e desligar o contêiner:
Subir o Contêiner (start.sh):

#!/bin/bash
`docker-compose up -d`


###### Explicação:
`docker-compose up -d`: Inicia os serviços definidos no arquivo docker-compose.yml em modo detached (em segundo plano).

Desligar o Contêiner (stop.sh):

#!/bin/bash
`docker-compose down`

###### Explicação:
`docker-compose down`: Para e remove os serviços definidos no arquivo docker-compose.yml.
Esses scripts simplificam o processo de gerenciamento do contêiner, permitindo iniciar e parar o ambiente Jupyter com facilidade. Certifique-se de conceder permissões de execução (chmod +x start.sh stop.sh) aos scripts para torná-los executáveis.
