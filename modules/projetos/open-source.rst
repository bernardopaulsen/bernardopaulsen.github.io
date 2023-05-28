Bibliotecas de Código Aberto
============================

Bem-vindo à página de projetos de código aberto!

Eu acredito firmemente no poder dos projetos de código aberto como uma maneira de contribuir para a comunidade de
desenvolvedores e cientistas de dados. Eles permitem que outros se beneficiem e construam sobre o trabalho que fazemos.
Além disso, projetos de código aberto são uma excelente maneira de aprender, pois nos permitem estudar, analisar e
colaborar com outros em soluções inovadoras.

Atualmente, tenho três projetos de código aberto:

- **almgren_chriss**, um pacote Python que implementa o modelo Almgren-Chriss para execução ideal de transações de portfólio.
- **log_decor**, que fornece decoradores de registro para funções, classes e métodos em Python.
- **banco_central_ts**, que fornece uma função para coletar facilmente dados abertos do Banco Central do Brasil.

Estou sempre trabalhando em novos projetos de código aberto e espero compartilhá-los à medida que são desenvolvidos.
Sinta-se à vontade para explorar meus projetos atuais e não hesite em me contatar se tiver alguma pergunta ou sugestão.

Obrigado por visitar minha página de projetos de código aberto, e espero que você encontre algo útil e interessante aqui.

almgren_chriss
--------------

**almgren_chriss** é um pacote Python que implementa o modelo Almgren-Chriss para execução ideal de transações de
portfólio. O modelo Almgren-Chriss é um modelo matemático usado nos mercados financeiros para determinar a maneira
ideal de executar grandes ordens. Ele considera fatores como tolerância ao risco, duração da negociação, volatilidade
e impacto permanente e temporário no mercado.

O pacote fornece funções para calcular o custo esperado e a variância do custo de negociação, a taxa de decaimento
da negociação, a trajetória de negociação e lista de negociações. Essas funções podem ser usadas para analisar e
otimizar estratégias de negociação.

Aqui está um exemplo de como usar o pacote para calcular a trajetória de negociação:

.. code-block:: python

    from almgren_chriss import trade_trajectory

    # Tolerância ao risco, intervalo entre negociações, volatilidade, inclinação de impacto permanente, inclinação de impacto temporário
    lambda_, tau, sigma, gamma, eta = 2e-6, 1, 0.95, 2.5e-7, 2.5e-6
    # Número total de ações, duração da negociação
    X, T = 1e06, 5.0

    trajectory = trade_trajectory(lambda_, tau, sigma, gamma, eta, X, T)

.. image:: assets/almgren-chriss-trade_trajectory.png

**almgren_chriss** está disponível no repositório oficial PyPI, e todo o código-fonte do projeto está disponível no repositório GitHub. Isso permite que você contribua para o projeto e personalize o pacote para suas necessidades específicas.

- `almgren_chriss - PyPI <https://pypi.org/project/almgren-chriss/>`_
- `almgren_chriss - Código <https://github.com/bernardopaulsen/almgren-chriss>`_
- `almgren_chriss - Documentação <https://bernardopaulsen.github.io/almgren-chriss/>`_


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
