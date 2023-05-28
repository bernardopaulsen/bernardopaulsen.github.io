.. post:: 2023-05-28
   :tags: optimal execution, python package
   :category: blog, en
   :author: me
   :language: en


Release of almgren_chriss 1.0 Python Package
********************************************

I am thrilled to announce the release of the almgren_chriss 1.0 Python package!
This package is designed to help financial analysts, researchers, and enthusiasts implement the Almgren-Chriss model
for optimal execution of large orders. The model is described in the paper `Optimal Execution of Portfolio Transactions - Almgren & Chriss (2000) <https://www.smallake.kr/wp-content/uploads/2016/03/optliq.pdf>`_.

The Problem of Optimal Execution of Large Orders
================================================

In financial markets, executing large orders is a complex task. A large order can significantly impact the market,
causing the price to move against the order, a phenomenon known as market impact. The challenge is to find an optimal
trading strategy that minimizes the cost of trading while considering the risk associated with the price fluctuations.

The Almgren-Chriss Model
========================

The Almgren-Chriss model is a mathematical framework that addresses this problem.
Named after Robert Almgren and Neil Chriss, who introduced it in 2000, the model is widely used in financial markets for
its simplicity and effectiveness.

The model assumes both temporary and permanent market impact.
Temporary impact affects the price only for the duration of the trade, while permanent impact changes the price indefinitely.
The model also assumes that the price follows a geometric Brownian motion with a constant volatility.

The model considers several variables, including the risk tolerance of the trader, the volatility of the stock,
the duration of the trading period, and the total number of shares to be traded.
The model then determines the optimal trading strategy that minimizes the expected cost of trading and the risk
associated with price fluctuations.

The Almgren-Chriss model presents a trade-off between market impact and risk.
Trading quickly can reduce the risk of price fluctuations but increases the market impact, while trading slowly
reduces the market impact but exposes the trader to price risk.

The almgren_chriss Python Package
=================================

The almgren_chriss Python package provides a practical implementation of the Almgren-Chriss model.
It includes functions to calculate the expected cost and variance of the cost of trading, the trade decay rate, and the
trading trajectory and list of trades. These functions can be used to analyze and optimize trading strategies.

The package is available on the official PyPI repository, and the entire source code of the project is
available on the GitHub repository. Also, the documentation is available on GitHub Pages.

- `almgren_chriss - PyPI <https://pypi.org/project/almgren-chriss/>`_
- `almgren_chriss - Code <https://github.com/yourusername/almgren_chriss>`_
- `almgren_chriss - Documentation <https://yourusername.github.io/almgren_chriss/>`_

Examples
========

You can install the package using **pip**:

.. code-block::

   pip install almgren_chriss

Here is an example of how to use the package to calculate the trading trajectory and list of trades:

.. code-block:: python

    from almgren_chriss import trade_trajectory, trade_list, cost_expectation, cost_variance

    # Risk tolerance, interval between trades, volatility, permanent impact slope, temporary impact slope, temporary impact intercept
    lambda_, tau, sigma, gamma, eta, epsilon = 2e-6, 1, 0.95, 2.5e-7, 2.5e-6, 0.0625
    # Total number of shares, trading duration
    X, T = 1e06, 5.0


>>> trade_trajectory(lambda_, tau, sigma, gamma, eta, X, T)
array([1000000.0, 428598.84574702, 182932.81426177, 76295.72161546, 27643.37739691, 0.0])

.. image:: trade_trajectory.png

>>> trade_list(lambda_, tau, sigma, gamma, eta, X, T)
array([571401.15425298, 245666.03148525, 106637.09264631, 48652.34421856, 27643.37739691])

.. image:: trade_list.png

>>> cost_expectation(lambda_, tau, sigma, gamma, eta, epsilon, X, T)
1140715.1670497851

>>> import math
>>> math.sqrt(cost_variance(lambda_, tau, sigma, gamma, eta, X, T))
449367.65254135116


I hope you find the almgren_chriss Python package useful and I look forward to hearing your feedback and suggestions.
Happy trading!