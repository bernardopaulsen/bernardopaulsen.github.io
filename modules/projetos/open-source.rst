Bibliotecas Open-Source
=======================

Bem-vindo à página de projetos *open-source*! Aqui, compartilho o meu trabalho em projetos *open-source*, que considero de extrema importância para o desenvolvimento de *software* e para a ciência de dados.

Acredito que projetos *open-source* são uma forma de contribuir para a comunidade de desenvolvedores e cientistas de dados, permitindo que outros possam aproveitar e aprimorar o trabalho que realizamos. Além disso, projetos *open-source* são uma excelente forma de aprendizado, pois nos permitem estudar, analisar e colaborar com outras pessoas em soluções inovadoras.

Atualmente, tenho dois projetos *open-source* desenvolvidos inteiramente por mim:

- **log_decor**, que fornece decoradores de *logging* para funções, classes e métodos em Python;
- **banco_central_ts**, que fornece uma função para coletar facilmente dados abertos do Banco Central do Brasil.

Estou sempre trabalhando em novos projetos *open-source*, e estou ansioso para compartilhá-los com você à medida que forem desenvolvidos. Sinta-se à vontade para explorar meu projeto atual e não hesite em entrar em contato comigo se tiver alguma dúvida ou sugestão.

Obrigado por visitar minha página de projetos open-source, e espero que você encontre algo útil e interessante aqui.

log_decor
---------

O **log_decor** é um projeto *open-source* escrito em Python que fornece decoradores de *logging* para funções, classes e métodos. Com esses decoradores, é possível adicionar facilmente *logs* em uma aplicação, fornecendo informações úteis sobre a execução do código.

Os decoradores de classe adicionam um *logger* à classe, permitindo que sejam registrados eventos específicos da classe, bem como informações úteis sobre a sua execução. Os decoradores de funções e métodos criam mensagens de *log* sempre que o objeto decorado é chamado, e essas mensagens podem ter diversos formatos, desde simples mensagens pré-definidas até informações detalhadas sobre a execução do método.

O exemplo a seguir utiliza a biblioteca para adicionar funcionalidade de logging a uma função:

.. code-block:: python

    from log_decor import log_info


    # logs no nível DEBUG
    @log_info()
    def f():
        pass


>>> logging.basicConfig(level=logging.DEBUG)
>>> f()
DEBUG:root:f() [0.0001s] -> None

O **log_decor** está disponível no repositório oficial PyPI, onde você pode facilmente instalá-lo em sua aplicação. Além disso, todo o código-fonte do projeto está disponível no repositórioGitHub, permitindo que você contribua para o projeto e personalize o pacote para suas necessidades específicas.

Para facilitar o uso do **log_decor**, todo o projeto tem documentação completa na página do projeto no GitHub Pages, incluindo exemplos de uso e guias de instalação. Isso torna o **log_decor** uma opção ideal para desenvolvedores que desejam adicionar *logging* em suas aplicações de forma rápida e fácil.

- `log_decor - PyPI <https://pypi.org/project/log-decor/>`_
- `log_decor - Código <https://github.com/bernardopaulsen/log_decor>`_
- `log_decor - Documentação <https://bernardopaulsen.github.io/log_decor/>`_

Postagens sobre log-decor no blog 'Dados: Apenas o Começo'
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. postlist::
   :category: log-decor
   :date: %d/%m/%Y
   :format: {title}, {date}
   :excerpts:
   :expand: Leia mais ...

banco_central_ts
----------------

O **banco_central_ts** é um pacote Python bastante simples.
Ela apenas oferece uma função que realiza coleta de dados pela API do `Sistema Gerenciador de Séries Temporais do Banco Central do Brasil <https://www3.bcb.gov.br/sgspub>`_.

o exemplo a seguir utiliza a biblioteca para coletar todos os dados da série temporal de valores diários da taxa CDI,
que possui código o 12.

.. code-block:: python

   from banco_central_ts import get as bacen_ts


   cdi_rate = bacen_ts(12)


>>> type(cdi_rate)
pandas.core.frame.DataFrame
>>> cdi_rate.head()
               valor
data
1986-03-06  0.068111
1986-03-10  0.069028
1986-03-12  0.067417
1986-03-14  0.064584
1986-03-17  0.068222

- `banco_central_ts - Código <https://github.com/bernardopaulsen/banco_central_ts>`_
- `banco_central_ts - Documentação <https://bernardopaulsen.github.io/banco_central_ts/>`_
