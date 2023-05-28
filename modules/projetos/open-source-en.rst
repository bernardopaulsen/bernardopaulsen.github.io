Open-Source Libraries
=======================

Welcome to the open-source projects page!

I am a firm believer in the power of open-source projects as a means to contribute to the developer and data science
community. They allow others to benefit from and build upon the work we do. Moreover, open-source projects are an
excellent way of learning, as they enable us to study, analyze, and collaborate with others on innovative solutions.

Currently, I have three open-source projects:

- **almgren_chriss**, a Python package implementing the Almgren-Chriss model for optimal execution of portfolio transactions.
- **log_decor**, which provides logging decorators for functions, classes, and methods in Python.
- **banco_central_ts**, which provides a function for easily collecting open data from the Central Bank of Brazil.

I am always working on new open-source projects and look forward to sharing them with you as they are developed.
Feel free to explore my current projects and don't hesitate to contact me if you have any questions or suggestions.

Thank you for visiting my open-source projects page, and I hope you find something useful and interesting here.

almgren_chriss
--------------

**almgren_chriss** is a Python package that implements the Almgren-Chriss model for optimal execution of portfolio
transactions. The Almgren-Chriss model is a mathematical model used in financial markets to determine the optimal way
to execute large orders. It considers factors such as risk tolerance, trading duration, volatility, and permanent and
temporary market impact.

The package provides functions for calculating the expected cost and variance of the cost of trading,
the trade decay rate, and the trading trajectory and list of trades.
These functions can be used to analyze and optimize trading strategies.

Here is an example of how to use the package to calculate the trading trajectory:

.. code-block:: python

    from almgren_chriss import trade_trajectory

    # Risk tolerance, interval between trades, volatility, permanent impact slope, temporary impact slope
    lambda_, tau, sigma, gamma, eta = 2e-6, 1, 0.95, 2.5e-7, 2.5e-6
    # Total number of shares, trading duration
    X, T = 1e06, 5.0

    trajectory = trade_trajectory(lambda_, tau, sigma, gamma, eta, X, T)

.. image:: assets/almgren-chriss-trade_trajectory.png

**almgren_chriss** is available on the official PyPI repository, and the entire source code of the project is
available on the GitHub repository. Also, the documentation is available on GitHub Pages.

- `almgren_chriss - PyPI <https://pypi.org/project/almgren-chriss/>`_
- `almgren_chriss - Code <https://github.com/bernardopaulsen/almgren-chriss>`_
- `almgren_chriss - Documentation <https://bernardopaulsen.github.io/almgren-chriss/>`_

log_decor
---------

**log_decor** is an open-source project written in Python that provides logging decorators for functions, classes, and methods. With these decorators, you can easily add logs to an application, providing useful information about the code's execution.

Class decorators add a logger to the class, allowing specific events of the class to be logged, as well as useful information about its execution. Function and method decorators create log messages whenever the decorated object is called, and these messages can have various formats, from simple pre-defined messages to detailed information about the method's execution.

The following example uses the library to add logging functionality to a function:

.. code-block:: python

    from log_decor import log_info


    # logs at DEBUG level by default
    @log_info()
    def f():
        pass


>>> logging.basicConfig(level=logging.DEBUG)
>>> f()
DEBUG:root:f() [0.0001s] -> None

**log_decor** is available on the official PyPI repository, where you can easily install it in your application. Additionally, the entire source code of the project is available on the GitHub repository, allowing you to contribute to the project and customize the package for your specific needs.

To facilitate the use of **log_decor**, the project has comprehensive documentation on the GitHub Pages project page, including usage examples and installation guides. This makes **log_decor** an ideal choice for developers who want to quickly and easily add logging to their applications.

- `log_decor - PyPI <https://pypi.org/project/log-decor/>`_
- `log_decor - Code <https://github.com/bernardopaulsen/log_decor>`_
- `log_decor - Documentation <https://bernardopaulsen.github.io/log_decor/>`_


banco_central_ts
----------------

**banco_central_ts** is a simple Python package that offers a function for data collection through the `Central Bank of Brazil's Time Series Manager API <https://www3.bcb.gov.br/sgspub>`_.

The following example uses the library to collect all data from the daily inter-bank deposits rate (CDI) time series, which has the code 12.

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

- `banco_central_ts - Code <https://github.com/bernardopaulsen/banco_central_ts>`_
- `banco_central_ts - Documentation <https://bernardopaulsen.github.io/banco_central_ts/>`_
