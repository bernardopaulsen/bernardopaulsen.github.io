.. post:: 2023-04-12
   :tags: open-source, log-decor
   :category: blog, log-decor, pt
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


log-decor 2.0
*************

Nesta postagem venho anunciar a versão 2.0 da minha biblioteca open-source, **log-decor**!

Os links referentes à biblioteca são os seguintes:

- `PyPI`_
- `GitHub`_
- `GitHub Pages`_

A **log-decor** é uma biblioteca Python que fornece decoradores para adicionar a funcionalidade de *logging* aos objetos.

Algumas novidades relacionadas ao uso da biblioteca são:

1. Antes, os decoradores só podiam ser usados em métodos de classes, mas agora eles também podem ser utilizados em funções avulsas.
2. Um novo decorador foi adicionado, em que o usuário pode fornecer funções para processar os argumentos e o resultado do objeto decorado antes que essas informações sejam logadas.

Foram realizadas também algumas melhorias internas na biblioteca, como:

1. O código foi refatorado de forma a torná-lo mais simples, compreensível e de acordo com os princípios de Código Limpo;
2. Foi adicionado um *workflow* de testes unitários para garantir a qualidade do software.
3. A documentação foi transferida do Read the Docs para o `GitHub Pages`_.

E por último, mas não menos importante, agora a biblioteca está publicada pelo `PyPI`_ e pode ser instalada facilmente com o comando

.. code-block::

    pip install log-decor

Exemplos de uso
===============


Adicionar funcionalidade de logging a uma função
------------------------------------------------

.. code-block:: python

    from log_decor import log_info


    # logs no nível DEBUG
    @log_info()
    def f():
        pass


>>> logging.basicConfig(level=logging.DEBUG)
>>> f()
DEBUG:root:f() [0.0001s] -> None
        

Adicionar logger a uma classe
-----------------------------

.. code-block:: python

    from log_decor import add_logger


    # logger com nome 'Exaxmple'
    @add_logger()
    class Example:
        pass

    # logger com nome 'LoggerName'
    @add_logger('LoggerName')
    class Example:
        pass


Adicionar funcionalidade de logging a um método
-----------------------------------------------

.. code-block:: python

    from log_decor import add_logger, log_info


    # logger com nome 'Example'
    @add_logger()
    class Example:

        # logs no nível DEBUG
        @log_info()
        def f(self):
            pass


>>> logging.basicConfig(level=logging.DEBUG)
>>> example = Example()
>>> example.f()
DEBUG:Example:f() [0.0001s] -> None


Definir as configurações de logging
-----------------------------------

.. code-block:: python

   import logging


   logging.basicConfig(filename='example.log',
                       level=logging.WARNING)






.. _GitHub: https://github.com/bernardopaulsen/log_decor
.. _PyPI: https://pypi.org/project/log-decor/
.. _GitHub Pages: https://bernardopaulsen.github.io/log_decor/