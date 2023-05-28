.. post:: 2023-03-20
   :tags: tutorial, jupyter notebook, docker
   :category: blog, pt
   :author: me
   :language: pt_BR

Executando Jupyter Notebook com Docker
**************************************

Nesta postagem, mostrarei um tutorial passo-a-passo para a execução de um Jupyter Notebook com o uso do Docker. O tutorial abordará desde a instalação do Docker até a execução de um notebook com Python. O objetivo é demonstrar como o Docker pode ser uma solução útil para a execução de aplicativos de ciência de dados em diferentes ambientes e sistemas operacionais.

Introdução
==========

Python e ciência de dados
-------------------------

`Python <https://www.python.org/>`_ é uma das linguagens de programação mais populares no mundo da ciência de dados. É amplamente utilizado por cientistas de dados, engenheiros e pesquisadores por causa de sua facilidade de uso e grande variedade de bibliotecas disponíveis. A biblioteca pandas, por exemplo, é uma das mais importantes para manipulação de dados e análise exploratória, enquanto a biblioteca scikit-learn é usada para machine learning e modelagem estatística.

Jupyter Notebook
----------------

A programação em REPL (Read-Eval-Print Loop) é uma técnica de programação interativa que é amplamente utilizada na ciência de dados. Ela permite que os usuários escrevam e executem códigos de maneira incremental, possibilitando a avaliação rápida e fácil dos resultados. Ferramentas como `Jupyter Notebook <https://jupyter.org/>`_ permitem que a programação em REPL seja utilizada com recursos adicionais, como visualização de gráficos e exportação de arquivos em diferentes formatos.

Ambientes virtuais
------------------

O manejo de dependências de um aplicativo Python pode ser complicado e pode causar conflitos entre diferentes bibliotecas. Para solucionar esse problema, é comum o uso de ambientes virtuais (muitas vezes através da bilbioteca `**venv** <https://docs.python.org/3/library/venv.html>`_), que permitem a instalação e gerenciamento de pacotes Python em um ambiente isolado do sistema operacional. Isso evita conflitos entre versões de pacotes e permite a reprodutibilidade de resultados em diferentes máquinas.

Docker
------

O [Docker](https://www.docker.com/) é uma plataforma de contêineres que permite a execução de aplicativos em diferentes ambientes. É amplamente utilizado na ciência de dados para o gerenciamento de dependências e para a execução de aplicativos em diferentes máquinas e sistemas operacionais. O uso do Docker para a execução de um Jupyter Notebook pode simplificar o processo de configuração e garantir a compatibilidade entre diferentes bibliotecas e dependências.

Linguagens Julia e R
--------------------

Embora Python seja a linguagem mais utilizada na ciência de dados, outras linguagens como `Julia <https://julialang.org/>`_ e `R <https://www.r-project.org/>`_ também são amplamente utilizadas. Felizmente, o Jupyter Notebook é compatível com essas linguagens e permite a execução de códigos e visualizações em um único ambiente interativo. Isso permite que os usuários possam escolher a linguagem mais adequada para o problema em questão sem a necessidade de mudar de ambiente ou plataforma.

Container
=========

Imagem
------

Uma maneira fácil de executar um Jupyter Notebook com o Docker é utilizando a imagem docker `jupyter/datascience-notebook <https://hub.docker.com/r/jupyter/datascience-notebook>`_ , que já vem pré-configurada com o Jupyter Notebook e as principais bibliotecas de ciência de dados. Esta imagem pode ser baixada diretamente do `Docker Hub <https://hub.docker.com/>`_ e executada em um container, que expõe o servidor Jupyter para ser acessado por um navegador.

Arquivos locais
---------------

Uma vantagem do uso do Docker é a possibilidade de montar um diretório local no container, permitindo o acesso a arquivos locais e a persistência de dados gerados pelo notebook. Isso pode ser feito através da opção "-v" no momento da execução do container, especificando o diretório local a ser montado e o diretório no container onde ele deve ser montado.

Dependências
------------

Para automatizar o manejo de dependências, é possível criar uma nova imagem Docker a partir da imagem 'jupyter/datascience-notebook' utilizando um `Dockerfile <https://docs.docker.com/engine/reference/builder/>`_. Neste arquivo, é possível copiar um arquivo de requisitos contendo as dependências necessárias e instalar essas dependências utilizando o pip. Após o build desta imagem personalizada, é possível executá-la em um container que já terá todas as dependências necessárias instaladas. Isso torna o processo de configuração e instalação de bibliotecas muito mais fácil e automatizado.

Exemplo
=======

Para ilustrar o uso do Docker para execução de um Jupyter Notebook, neste tutorial vamos criar um projeto de exemplo que utiliza a biblioteca pandas para análise de dados.

Estrutura do diretório
----------------------

A estrutura do diretório do projeto será a seguinte:

.. code-block::

    projeto_exemplo/
    ├── Dockerfile
    ├── notebooks/
    │   └── exemplo.ipynb
    └── requirements.txt


O arquivo ``exemplo.ipynb`` contém o código do Jupyter Notebook. O arquivo ``requirements.txt`` lista as dependências necessárias para executar o notebook.

Dockerfile
----------

O Dockerfile para a criação da imagem personalizada a partir da imagem 'jupyter/datascience-notebook' será o seguinte:

.. code-block:: Dockerfile

    FROM jupyter/datascience-notebook

    COPY requirements.txt /tmp/
    RUN pip install --upgrade pip && \
        pip isntall --requirement /tmp/requirements.txt

    WORKDIR /home/jovyan/work/


Neste Dockerfile, estamos copiando o arquivo de requisitos para o diretório ``/tmp/`` e instalando as dependências com o pip. Em seguida, selecionamos o diretório padrão do Jupyter Notebook ``/home/jovyan/work/``.

Criação da imagem
-----------------

Para criar a imagem personalizada a partir do Dockerfile, é necessário utilizar o comando ``docker build``. O comando deve ser executado no diretório onde se encontra o Dockerfile e o contexto do build, que contém os arquivos necessários para construir a imagem.

O comando para criar a imagem personalizada a partir do Dockerfile no nosso exemplo seria o seguinte:

.. code-block:: bash

    docker build --tag jupyter-exemplo .


Execução do container
---------------------

Após a construção da imagem, podemos executá-la em um container utilizando o seguinte comando ``docker run``:

.. code-block:: bash
    
    docker run -it --rm -p 8888:8888 -v $(pwd)/notebooks:/home/jovyan/work/ jupyter-exemplo


.. note::

    Na configuração padrão, o container é executado com o usuário **jovyan**, o que impossibilita a execução de comandos com privilégios de superusuário (já que a senha do usuário é necessária). Para executar este tipo de comandos, é necessário criar um usuário e desabilitar a necessidade de prover a senha ao executar comandos com **sudo**.

    .. code-block:: bash

        docker run -it --rm  \
        -p 8888:8888 \
        --user root \
        -e NB_USER="myuser" \
        -e CHOWN_HOME=yes \
        -e GRANT_SUDO=yes \
        -w "/home/${NB_USER}" \
        -v $(pwd)/notebooks:/home/myuser \
        jupyter-exemplo


Este comando executa o container a partir da imagem personalizada, mapeia a porta do servidor Jupyter no host para a porta ``8888`` do container e monta o diretório de notebooks local no diretório padrão do Jupyter Notebook dentro do container.

Com isso, podemos acessar o notebook pelo navegador utilizando a URL fornecida pelo Docker no terminal, e começar a trabalhar com os dados utilizando a biblioteca pandas.

Conclusão
=========

Neste tutorial, vimos como utilizar o Docker para facilitar o manejo de dependências e execução de um Jupyter Notebook em um projeto de ciência de dados. Com o uso de uma imagem personalizada a partir da imagem **jupyter/datascience-notebook**, podemos automatizar o processo de instalação de bibliotecas e configuração do ambiente de trabalho.

Além disso, mostramos um como criar uma imagem personalizada com dependências instaladas, além de como utilizar o Docker para executar um container e editar arquivos locais diretamente no Jupyter Notebook.

Espero que este tutorial prático tenha sido útil e possa ajudar na produtividade de quem está trabalhando com ciência de dados em Python. Tanto Jupyter Notebook quanto Docker são ferramentas poderosas para a criação de soluções de análise de dados mais eficientes e precisas.