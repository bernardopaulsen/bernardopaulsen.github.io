.. post:: 2023-03-25
   :tags: python, documentação, sphinx, autodoc, read the docs
   :category: blog, pt
   :author: me
   :language: pt_BR


.. definição de box para incluir html snippets

.. raw:: html
    
    <style>
    .my-box {
    border: 1px solid #ddd;
    border-radius: 6px;
    padding: 10px;
    margin-bottom: 10px
    }
    </style>


Utilizando Sphinx para a geração de documentação de softwares escritos em Python
********************************************************************************


Documentação é um aspecto essencial em qualquer projeto de software. Ela é a fonte de informação para o usuário final, além de ser um recurso para os desenvolvedores que precisam entender como o *software* funciona. Além disso, uma documentação bem escrita ajuda a evitar problemas de manutenção no futuro (ou seja, evitar *technical debt*) e melhora a qualidade do *software* em geral.

Neste artigo, dou um exemplo prático de como criar uma documentação (seção :ref:`Exemplo <exemplo>`). Utilizo o `Sphinx`_ como a ferramenta principal para gerar a documentação, e o repositório `Read the Docs`_ para publicá-la.

Mostro como utilizar a extensão `autodoc`_ para permitir a criação automática da API, que extrai automaticamente as informações da docstring do código-fonte (seção :ref:`Criação Automática de API <criacao-automatica-API>`). Para substituição do tema padrão para outro que se propõe a ser mais agradável visualmente,  utilizo a extensão `sphinx_rtd_theme`_ (seção :ref:`Definição do tema da documentação <definicao-tema-documentacao>`). Mostro também como publicar a documentação criada no `Read the Docs`_ (seção :ref:`Publicação no Read the Docs <publicacao-read-the-docs>`), permitindo que os usuários acessem a documentação facilmente pela *web*.

Adicionalmente, menciono diversas extensões do Sphinx (seção :ref:`Outras funcionalidades do Sphinx <outras-funcionalidades-sphinx>`), tanto algumas inclusas por padrão no Sphinx quanto outras criadas por terceiros e disponibilizadas no `PyPI`_. Essas extensões oferecem funcionalidades extras para a documentação, a deixando mais versátil e útil para diferentes tipos de projeto.

Sphinx e Read the Docs
======================

Sphinx
------

Uma das ferramentas mais populares para criação de documentação em projetos Python é a biblioteca `Sphinx`_. Sphinx é uma ferramenta de documentação de código aberto que é fácil de usar e altamente configurável, que utiliza o formato de marcação `ReStructuredText`_ (ou RST), que é uma linguagem de marcação leve e fácil de aprender, para criar a documentação.

Uma das grandes vantagens do Sphinx é a capacidade de criar a documentação da API automaticamente a partir da documentação do próprio código. Isso significa que, ao escrever a documentação do código, a referência API pode ser gerada automaticamente a partir dessa documentação, economizando tempo e esforço na criação da documentação.

Outra grande vantagem do Sphinx é a sua capacidade de gerar a documentação em vários formatos, como HTML, PDF e EPUB.

Read the Docs
-------------

Sphinx também pode ser integrada facilmente com o `Read the Docs`_, um serviço de hospedagem de documentação on-line. A integração do Sphinx com o Read the Docs permite que a documentação seja facilmente publicada e acessível a todos os usuários do projeto. Além disso, o `Read the Docs for Business`_ permite que projetos privados possam utilizar a plataforma, mantendo a documentação privada e segura.

Estrutura de uma Documentação
=============================

Seções básicas
--------------

Uma documentação pode incluir diversas seções, tais como: *getting started*, *user guide*, API, e *development*. A seguir descrevo as infoamções contidas em cada seção.

- *getting started*: visão geral da biblioteca, demonstrando como utilizá-la de forma rápida e eficiente.
- *user guide*: exemplos mais detalhados de uso, com explicações passo a passo para a utilização da biblioteca.
- API: descrição detalhada as diferentes funcionalidades e métodos da biblioteca.
- *development*: informações sobre como contribuir com o desenvolvimento da biblioteca, incluindo detalhes sobre os padrões de escrita, a estrutura do código e como realizar testes.

Informações de negócio
----------------------

No caso de uma documentação interna para o time, pode ser interessante adicionar seções que tratam de aspectos de negócio do time, como objetivo do projeto, colaboradores, informações financeiras, clientes, planejamento e objetivos de longo prazo, histórico de reuniões e documentação dos requisitos. As seções variam entre projetos, cabendo ao time definir as informações necessárias à documentação, levando em conta os aspectos únicos de cada projeto.

Outros meios de documentação
----------------------------

Vale destacar que, mesmo que muitas informações sobre o andamento do projeto sejam importantes de serem documentadas, muitas delas são documentadas através das funcionalidades de gerenciamento inclusas nos repositórios de código, como GitHub e GitLab. Essas informações incluem as *issues*, o histórico de *releases*, informações referentes a cada *sprint* e cada *deliverable*, etc.

.. _exemplo:

Exemplo
=======

Neste exemplo, usarei a biblioteca `log_decor`_ - uma biblioteca de decoradores de *logging* de código aberto que desenvolvi recentemente - para apresentar como usar o Sphinx, em conjunto com o serviço de hospedagem *on-line* `Read the Docs`_, para gerar e publicar a documentação de um aplicativo Python.

Neste texto, eu gostaria de compartilhar um exemplo prático de como utilizar a biblioteca Sphinx em conjunto com o serviço de hospedagem de documentação on-line Read the Docs para criar e publicar a documentação de uma biblioteca Python. Para isso, vamos utilizar a biblioteca `log_decor`_, uma biblioteca de decoradores de *logging* de código aberto que desenvolvi recentemente.

Sugiro que, antes de acompanhar o exemplo nesta página, você explore a `documentação da log_decor no Read the Docs <https://log-decor.readthedocs.io/en/latest/index.html>`_. Assim será mais fácil de compreender os diferentes pontos que serão abordados.

Estrutura do projeto
--------------------

A estrutura de diretórios da biblioteca **log_decor** é composta por vários arquivos e pastas que são importantes para o desenvolvimento e a documentação da biblioteca. A seguir, é apresentada a estrutura e uma breve descrição de cada um dos arquivos e pastas:

.. code-block::

    log_decor/
    ├── docs/
    ├── src/
    │   └── log_decor/
    |       ├── __init__.py
    |       └── ...
    ├── pyproject.toml
    └── requirements.txt


A pasta ``docs/`` contém todos os arquivos necessários para a criação da documentação da biblioteca.

A pasta ``src/log_decor/`` contém todos os arquivos de código-fonte da biblioteca. Esses arquivos incluem os módulos Python, além de outros arquivos, como o arquivo ``__init__.py`` que indica que a pasta é um pacote Python.

O arquivo ``pyproject.toml`` é utilizado para a instalação da biblioteca. Esse arquivo contém informações importantes, como o nome da biblioteca, sua versão e suas dependências.

Por fim, o arquivo ``requirements.txt`` na raiz do projeto lista os requisitos necessários para o funcionamento da biblioteca.

Criando os aquivos base da documentação
---------------------------------------

Para criar os arquivos base da documentação, basta executar o comando

.. code-block::

    sphinx-quickstart


no diretório ``projeto_exemplo/docs/``. Durante a execução o usuário é guiado por uma série de perguntas, como o nome do projeto, a língua utilizada, os autores e a versão, entre outras opções. Essas opções são importantes para configurar a documentação de acordo com as necessidades do projeto.

Ao executar o comando ``sphinx-quickstart`` para criar a documentação da biblioteca, são gerados alguns arquivos e pastas padrão. Esses arquivos são:

- ``confl.py``: arquivo de configuração principal do Sphinx, onde são definidas as configurações gerais da documentação, como o título, a descrição, a lista de extensões e outras opções de personalização.
- ``index.rst``: arquivo principal da documentação, onde se definem os tópicos principais, como a introdução, a instalação e o uso da biblioteca. A partir desse arquivo, são criados os demais arquivos de documentação.
- ``make.bat`` (para Windows) e ``Makefile`` (para sistemas baseados em Unix): arquivos de script utilizados para compilar os arquivos ``.rst`` em arquivos HTML, PDF e outros.

Após a execução do comando, a estrutura de diretórios se torna a seguinte:

.. code-block::

    log_decor/
    ├── docs/
    |   ├── conf.py  # novo
    |   ├── index.rst  # novo
    |   ├── make.bat  # novo
    |   └── Makefile  # novo
    ├── src/
    │   └── log_decor/
    |       ├── __init__.py
    |       └── ...
    ├── pyproject.toml
    └── requirements.txt


Adicionando arquivos de conteúdo
--------------------------------

É possível escrever a documentação utilizando diversos arquivos ``.rst``. Na verdade, é uma boa prática dividir a documentação em diferentes arquivos para que cada um deles tenha um foco específico, facilitando a navegação e a leitura do conteúdo.

No caso do exemplo que estamos trabalhando, adicionamos na pasta ``docs/modules/`` diversos arquivos que correspondem a diferentes seções da documentação, que neste caso são exibidos em diferentes páginas. Cada arquivo contém informações específicas sobre o assunto abordado naquela seção, permitindo que o leitor encontre facilmente o que procura.

A estrutura de diretórios com os novos arquivos é a seguinte:

.. code-block::

    log_decor/
    ├── docs/
    |   ├── modules/  # novo
    |   |   ├── api.rst
    |   |   ├── contributing.rst
    |   |   ├── examples.rst
    |   |   ├── license.rst
    |   |   └── usage.rst 
    |   ├── conf.py
    |   ├── index.rst
    |   ├── make.bat
    |   └── Makefile
    ├── src/
    │   └── log_decor/
    |       ├── __init__.py
    |       └── ...
    ├── pyproject.toml
    └── requirements.txt


Escrevendo a página inicial da documentação
-------------------------------------------

O arquivo ``index.rst`` é o arquivo principal da documentação, nele é onde definimos a estrutura básica e a organização dos tópicos que serão abordados. Ele é responsável por importar os demais arquivos ``.rst`` que vão compor a documentação, organizando-os de forma a facilitar a navegação do usuário.

O ``index.rst`` é a página inicial da documentação, pois é o primeiro arquivo que o usuário acessa ao abrir a documentação. Nele, é comum incluir uma breve introdução do projeto e uma lista dos tópicos que serão abordados, para que o usuário possa ter uma ideia geral do que ele encontrará ao navegar pela documentação.

Além disso, é possível utilizar o ``index.rst`` para incluir informações importantes sobre o projeto, como sua licença, os créditos aos autores e colaboradores, links para a página oficial do projeto, entre outras informações relevantes. Tudo isso contribui para tornar a documentação mais completa e informativa para os usuários.

O arquivo ``index.rst`` da biblioteca **log_decor** é o seguinte:

.. code-block:: restructuredtext
    
    Welcome to log-decor's documentation!
    =====================================

    Introduction
    ############

    This package has class and method decorators that provide logging functionality.

    Getting Started
    ###############

    To install, execute the following command:

    .. code-block::

       pip install git+https://github.com/bernardopaulsen/log_decor.git


    .. toctree::
       :caption: Contents

       modules/usage
       modules/examples
       modules/api
       modules/contributing
       modules/license


    Indices and tables
    ==================

    * :ref:`genindex`
    * :ref:`modindex`
    * :ref:`search`


Os diferentes elementos do arquivo acima são:

- 'Welcome to log-decor's documentation!': Título da página inicial.
- 'Introduction': Seção onde é apresentada uma breve introdução sobre a biblioteca, destacando sua principal funcionalidade.
- 'Getting Started': Seção que apresenta as informações necessárias para que o usuário possa começar a utilizar a biblioteca. Inclui um comando de instalação utilizando o **pip** e o link do repositório no GitHub.
- ``.. toctree::``: O comando é usado para criar uma tabela de conteúdo para a documentação gerada. Ele permite que o usuário liste outros arquivos ``.rst`` que serão exibidos na tabela de conteúdo.
- ``:caption: Contents``: Título que será utilizado para a tabela de conteúdo.
- ``modules/usage``, ``modules/examples``, ``modules/contributing``, ``modules/license``: Link para os arquivos ``.rst`` que serão incluídos na tabela de conteúdo.
- ``Indices and tables``: Seção que apresenta índices e tabelas referentes à documentação.
- ``:ref:genindex``: Link para o índice geral, que contém informações sobre todos os módulos, classes e funções documentados.
- ``:ref:modindex``: Link para o índice de módulos, que contém informações sobre todos os módulos documentados.
- ``:ref:search``: Link para a tabela de pesquisa, que permite ao usuário pesquisar por qualquer palavra-chave na documentação.

Você pode conferir o resultado final desta configuração abaixo:

.. raw:: html
    :file: index-page.html

Lembre que os conteúdos da tabela de conteúdo dependem dos conteúdos de cada um dos arquivos ``.rst`` incluídos na tabela.

.. _criacao-automatica-API:

Criação automática de API
-------------------------

A extensão Sphinx `autodoc`_ permite que a documentação seja gerada automaticamente a partir do código fonte da biblioteca. No nosso exemplo, estamos utilizando essa extensão em conjunto com a biblioteca `sphinx_autodoc_typehints`_ (que adiciona suporte para documentar automaticamente tipos de argumentos e valores de retorno de funções e métodos) para documentar automaticamente as classes e funções do nosso código fonte.

Para configurar o uso do **autodoc** e **sphinx-autodoc-typehints**, é necessário incluí-los na lista de extensões do arquivo ``conf.py``. Além disso, é possível configurar diversas opções para as extesões, como incluir membros privados, documentar atributos, e mais.

Documentação escrita no código fonte
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Existem diversas formas de documentar o código fonte, todas descritas na documentação do `autodoc`_. Uma dessas formas é através das *docstrings*, que são *triple quoted strings* colocadas imediatamente após a definição de uma função, método, classe ou módulo. As *docstrings* podem ser lidas pela extensão **autodoc** do Sphinx e utilizadas para gerar a documentação.

O exemplo a seguir é o módulo ``add_logger.py`` da biblioteca **log_decor**:

.. code-block:: python

    # add_logger.py

    import functools
    import logging
    from typing import Optional, Type, TypeVar


    Class = TypeVar('Class')


    class AddLogger:
        """Class decorator that adds a logger attribute to the decorated class.

        :param name: Name of Logger. If None, the qualified name of the class
            passed to :meth:`add_logger.AddLogger.__call__` will be the name of
            the logger.
        """
        def __init__(self,
                    name: Optional[str] = None
                    ) -> None:
            self._name = name

        def __call__(self,
                    cls: Class
                    ) -> Type[Class]:
            """Add logger attribute to class.

            The name of the attribute will be '_logger'.

            :param cls: Class to which add logger. If no name was passed to
                :meth:`add_logger.AddLogger.__init__`, the qualified name of the
                class passed to this parameter will be the name of the logger.
            :return: Class with logger attribute.
            """
            @functools.wraps(cls,
                            updated=())
            class LoggedClass(cls):
                def __init__(self_,
                            *args,
                            **kwargs
                            ) -> None:
                    self_.logger = logging.getLogger(
                        name=self._name if self._name is not None else cls.__name__
                    )
                    super().__init__(*args,
                                    **kwargs)
            return LoggedClass


A *docstring* começa com uma breve descrição da função do objeto no qual ela está escrita. Em seguida, apresenta descrições dos parâmetros do objeto, e finalmente uma descrição do retorno do objeto. Vale notar que as descrições dos parâmetros do método ``__init__`` são escritas na *dosctring* da classe, não do método.

*Docstrings* podem conter mais informações além da simples descrição do objeto e seus parâmetros e valor de retorno. É uma boa prática incluir exemplos de uso do objeto, exemplos de relação entre argumentos e valores de retorno e outras informações relevantes que possam auxiliar o leitor a entender melhor como utilizar o objeto documentado.

Vale notar que os tipos dos parâmetros e valores de retorno não estão documentados nas *docstrings* do exemplo, mas isso acontece pois os tipos já estão documentados no próprio código, e estes serão lidos pela extensão **sphinx_autodoc_typehints** e adicionados automaticamente à documentação final.

Configurando o diretório do código fonte
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Primeiramente, é necessário indicar o diretório base do código fonte da biblioteca, configurando a variável ``sys.path`` no arquivo ``conf.py``. Por exemplo:

.. code-block:: python

    # -- Path setup 
    import os
    import sys

    sys.path.insert(0, os.path.abspath('../src/log_decor'))


Definindo as extensões
^^^^^^^^^^^^^^^^^^^^^^

Para adicionar as extensões **autodoc** e **sphinx_autodoc_typehints** é necessário adicioná-las na lista ``extensions`` do arquivo ``conf.py``. Por exemplo:

.. code-block:: python

    # -- General configuration 
    extensions = [
        'sphinx.ext.autodoc',
        'sphinx_autodoc_typehints',
    ]


Adicionando a documentação automática de uma classe em arquivo .rst
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Para adicionar a API de uma classe em um arquivo ``.rst``, podemos utilizar o comando ``.. autoclass::``. Por exemplo, para adicionar a documentação da classe ``AddLogger`` do módulo ``add_logger``, podemos utilizar o seguinte código:

.. code-block:: restructuredtext

    .. autoclass:: add_logger.AddLogger
       :members:
       :special-members: __call__

No código em RST acima a diretiva ``autoclass`` indica que estamos documentando uma classe automaticamente, através da extensão **autodoc**. O argumento ``add_logger.AddLogger`` indica a classe que estamos docuentando. A opção ``:members:`` indica que queremos documentar todos os membros da classe, e a opção ``:special-members: __call__`` indica que queremos documentar também o método especial ``__call__``, que por ser um método especial não é documentado por padrão pelo **autodoc**.

Abaixo você pode conferir o mesmo resultado:

.. raw:: html
    :file: api-example.html


.. _definicao-tema-documentacao:

Definição do tema da documentação
---------------------------------

O Sphinx permite a escolha de temas para personalizar a aparência da documentação. O tema padrão do Sphinx é o **classic**, mas existem diversos outros temas disponíveis, como oa **labaster**, o **sphinx_rtd_theme** e o **sphinx_bootstrap_theme**, entre outros.

No caso da biblioteca **log_decor** que está sendo utilizada como exemplo, foi escolhido o tema `sphinx_rtd_theme`_, que é um tema popular e moderno, que oferece uma aparência limpa e profissional para a documentação.

Para configurar o tema **sphinx_rtd_theme**, é necessário modificar o arquivo ``conf.py``, que é o arquivo de configuração principal do Sphinx. É preciso importar a biblioteca do tema e definir a variável **html_theme** para o nome do tema escolhido.

O código necessário para configurar o tema **sphinx_rtd_theme** no arquivo `conf.py` é o seguinte:

.. code-block:: python

    # -- Options for HTML output 
    import sphinx_rtd_theme

    html_theme = 'sphinx_rtd_theme'
    html_theme_path = [sphinx_rtd_theme.get_html_theme_path()]


Instalação das bibliotecas necessárias no ambiente de desenvolvimento
---------------------------------------------------------------------

Para criar a documentação com o Sphinx, é necessário ter tanto o Sphinx quanto as bibliotecas auxiliares instaladas no ambiente de desenvolvimento. As bibliotecas auxiliares necessárias para a geração da documentação geralmente são especificadas em um arquivo ``requirements.txt``, que deve estar localizado no diretório ``docs/``. As bibliotecas importadas pelo código fonte também devem estar instaladas já que estamos utilizando a extensão **autodoc**, mas elas são especificadas no arquivo ``requirements.txt`` na raiz do projeto.

A estrutura de diretórios será então:

.. code-block::

    log_decor/
    ├── docs/
    |   ├── modules/
    |   |   └── ...
    |   ├── conf.py
    |   ├── index.rst
    |   ├── make.bat
    |   ├── Makefile
    |   └── requirements.txt  # novo
    ├── src/
    │   └── log_decor/
    |       ├── __init__.py
    |       └── ...
    ├── pyproject.toml
    └── requirements.txt


O conteúdo do arquivo ``requirements.txt`` será:

.. code-block::

    sphinx
    sphinx_rtd_theme
    sphinx_autodoc_typehints


Esses pacotes podem ser instalados com o comando

.. code-block:: bash

    pip install --requirement docs/requirements.txt


Geração da documentação em HTML
-------------------------------

Dentro da posta ``docs/``, o comando

.. code-block:: bash

    make html


é utilizado para gerar a documentação em HTML a partir dos arquivos fonte. Os arquivos HTML serão gerados no diretório ``docs/_build/html`` por padrão. A página inicial da documentação está no arquivo ``index.html``, que é então o arquivo que deve ser aberto para acessar a documentação.

.. code-block::

    log_decor/
    ├── docs/
    |   ├── _build/  # novo
    |   |   ├── doctrees/
    |   |   └── html/
    |   |        ├── ...
    |   |        ├── index.html
    |   |        └── ...
    |   ├── modules/
    |   |   └── ...
    |   ├── conf.py
    |   ├── index.rst
    |   ├── make.bat
    |   ├── Makefile
    |   └── requirements.txt
    ├── src/
    │   └── log_decor/
    |       ├── __init__.py
    |       └── ...
    ├── pyproject.toml
    └── requirements.txt


Como citado anteriormente, a documentação completa pode ser acessada pela `página do log_decor no Read the Docs <https://log-decor.readthedocs.io/en/latest/index.html>`_.

O Sphinx também permite a geração de outros tipos de arquivos de documentação, como PDF e ePub. Para gerar um arquivo PDF, por exemplo, é necessário instalar o software LaTeX e depois usar o comando ``make latexpdf``. Já para gerar um arquivo ePub, é necessário instalar o software Calibre e usar o comando ``make epub``.

.. _publicacao-read-the-docs:

Publicação no Read the Docs
---------------------------

A integração entre Sphinx, `GitHub`_ e Read the Docs é extremamente útil para criar e manter documentação atualizada de projetos de software. Ao utilizar o Sphinx para gerar a documentação a partir do código fonte e o GitHub para armazenar o código, é possível automatizar o processo de atualização da documentação a cada nova versão do projeto. E com a integração com o Read the Docs, a documentação pode ser facilmente hospedada e compartilhada com a comunidade.

Como citado anteriormente, a documentação do projeto **log_decor** está disponibiliza pelo Read the Docs em `sua página na plataforma <https://log-decor.readthedocs.io/en/latest/index.html>`_

Configuração
^^^^^^^^^^^^

Para integrar o Sphinx com o Read the Docs, é necessário configurar um arquivo chamado ``readthedocs.yaml`` na raiz do projeto. Este arquivo permite especificar a versão do Python usada na documentação, bem como outras configurações. Por exemplo, é possível especificar os comandos a serem executados antes de construir a documentação e as extensões a serem usadas.

Abaixo, a estrutura de diretórios do projeto exemplo após a inclusao do arquivo ``readthedocs.yaml``:

.. code-block::

    log_decor/
    ├── docs/
    |   └── ...
    ├── src/
    │   └── log_decor/
    |       ├── __init__.py
    |       └── ...
    ├── pyproject.toml
    ├── readthedocs.yaml  # novo
    └── requirements.txt


O arquivo ``readthedocs.yaml`` é o seguinte:

.. code-block:: yaml

    # readthedocs.yaml
    version: 2

    sphinx:
    builder: html
    configuration: docs/conf.py
    fail_on_warning: true

    python:
    version: 3.8
    install:
    - requirements: docs/requirements.txt
        extra_requirements:
        - requirements.txt


O arquivo começa com a definição da versão do arquivo de configuração, neste caso, a versão 2.

A seção ``sphinx`` é utilizada para especificar as configurações do Sphinx. Neste caso, o *builder* definido é o *html*, o arquivo de configuração utilizado é o ``docs/conf.py`` e ``fail_on_warning`` é definido como **true**, o que faz com que o processo de construção da documentação falhe caso haja algum *warning*.

A seção ``python`` é utilizada para definir a versão do Python que será utilizada para construir a documentação, e a lista de pacotes que serão instalados antes da construção. Neste caso, é definido que a versão 3.8 será utilizada e que os arquivos ``docs/requirements.txt`` e ``requirements.txt`` serão utilizados para instalar os pacotes necessários, o primeiro definindo os pacotes utilizados pelo Sphinx e o segundo definindo os pacotes utilizados pelo código fonte da biblioteca.

Integração com Read the Docs
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

A integração do `Read the Docs`_ com o `GitHub`_ é muito simples e fácil de configurar. Para criar uma documentação no Read the Docs a partir de um repositório do GitHub, basta  criar uma conta no Read the Docs e configurar um novo projeto e vincular o projeto com o repositório do GitHub, selecionando o repositório e autorizando o acesso. Uma vez configurado, o Read the Docs irá automaticamente monitorar o repositório do GitHub para atualizações e gerar uma nova versão da documentação sempre que houver um novo *commit* ou *pull request*.

Acessando a documentação
^^^^^^^^^^^^^^^^^^^^^^^^

Uma vez que a integração esteja configurada e a documentação tenha sido construída, ela pode ser acessada pelo *link* fornecido pelo Read the Docs.

.. _outras-funcionalidades-sphinx:

Outras funcionalidades do Sphinx
================================

Sphinx oferece muitas funcionalidades além da geração de documentação. Algumas dessas funcionalidades podem tornar a documentação ainda mais útil e acessível.

ReStructuredText
----------------

O próprio formato de marcação ReStructuredText possui diversas funcionalidades não demonstradas no exemplo acima.

Uma delas é a `criação de links para seções e capítulos da documentação <https://docs.readthedocs.io/en/stable/guides/cross-referencing-with-sphinx.html>`_, incluindo links para objetos do código fonte. Esses links podem ser incluídos nas próprias docstrings do código, o que pode tornar a documentação ainda mais interconectada e fácil de usar.

Outra funcionalidade que vale a pena mencionar é o `suporte a blocos de código na documentação <https://www.sphinx-doc.org/en/master/usage/restructuredtext/directives.html#showing-code-examples>`_ (inclusive nas *docstrings*), o que permite que exemplos de utilização da biblioteca sejam expostos diretamente na documentação. Isso pode ser especialmente útil para ajudar os usuários a entender como usar a biblioteca em seus próprios projetos.

Extensões 
---------

Além das funcionalidades padrão, o Sphinx possui também diversas extensões muito úteis, tanto as inclusas na biblioteca quanto as de terceiros, que podem facilitar ainda mais o processo de documentação e tornar a documentação mais rica e completa. Algumas das extensões inclusas do Sphinx incluem:

- `doctest <https://www.sphinx-doc.org/en/master/usage/extensions/doctest.html>`_: inclusão de testes de unidade dentro da documentação, tornando-a mais interativa e facilitando a compreensão do uso da biblioteca.
- `intersphinx <https://www.sphinx-doc.org/en/master/usage/extensions/intersphinx.html>`_: inclusão de links para documentação de outras bibliotecas, facilitando o acesso à documentação de outras ferramentas.
- `viewcode <https://www.sphinx-doc.org/en/master/usage/extensions/viewcode.html>`_: inclusão de links para o código fonte de classes, funções e métodos documentados, tornando a documentação mais completa e permitindo uma compreensão mais profunda do funcionamento da biblioteca.

Algumas das extensões de terceiros que podem ser facilmente instaladas e utilizadas com o Sphinx r que estão disponíveis no repositório [PyPI] são:

- `sphinxcontrib-jupyter <https://pypi.org/project/sphinxcontrib-jupyter/>`_: inclusão de notebooks Jupyter na documentação, tornando-a mais interativa e permitindo a visualização de exemplos de uso da biblioteca de forma mais dinâmica. Vale notar que esta extensão é desenvolvida pela organização `QuantEcon <https://quantecon.org/>`_, que é uma organização dedicada à modelagem econômica, fornecendo bibliotecas e materiais educacionais sobre o tema, entre outros projetos. Recomendo fortemente que você explore os projetos da organização caso tenha interesse por modelagem econômica e finanças quantitativas.
- `sphinxcontrib-bibtex <https://pypi.org/project/sphinxcontrib-bibtex/>`_: inclusão automática de citações bibliográficas na documentação, facilitando a referência a artigos e trabalhos científicos relacionados à biblioteca.

Conclusão
=========

Em conclusão, a documentação é uma parte fundamental de qualquer projeto de software, mas, infelizmente, muitas vezes é negligenciada pelos desenvolvedores. Uma documentação clara e bem escrita não só ajuda a facilitar a compreensão do projeto, mas também facilita o processo de manutenção e a colaboração com outros desenvolvedores.

O `Sphinx`_ é uma ferramenta poderosa que torna a criação e manutenção da documentação muito mais fácil e eficiente. Além disso, a integração com o `GitHub`_ e o `Read the Docs`_ permite compartilhar a documentação de forma simples e acessível a qualquer pessoa interessada no projeto.

Espero que tenham gostado do artigo e que tenha sido útil para ajudar a melhorar a documentação de seus projetos de software. Lembre-se sempre que uma boa documentação é essencial para o sucesso de qualquer projeto!

.. definições de links

.. _Sphinx: https://www.sphinx-doc.org/en/master/
.. _sphinx_rtd_theme: https://pypi.org/project/sphinx-rtd-theme/
.. _autodoc: https://www.sphinx-doc.org/en/master/usage/extensions/autodoc.html
.. _sphinx_autodoc_typehints: https://pypi.org/project/sphinx-autodoc-typehints/
.. _Read the Docs: https://readthedocs.org/
.. _Read the Docs for Business: https://about.readthedocs.com/?ref=dotcom-homepage
.. _log_decor: https://test.pypi.org/project/log-decor/
.. _ReStructuredText: https://www.sphinx-doc.org/pt_BR/master/usage/restructuredtext/basics.html
.. _GitHub: https://github.com/
.. _PyPI: https://pypi.org/