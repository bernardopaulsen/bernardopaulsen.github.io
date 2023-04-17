.. post:: 2023-04
   :category: projeto
   :author: me
   :language: pt_BR

Estratégia de Momentum para Contratos Futuros
*********************************************

Neste projeto, criei um aplicativo de análise de retornos de contratos futuros e definição de pesos ótimos para uma estratégia de negociação baseada na ideia de *momentum*.

Estratégia
==========

A estratégia leva em conta o *momentum* em contratos futuros de ativos de diversas classes, criando uma carteira de contratos futuros em que existem ativos comprados e ativos vendidos. O rebalancemanto da estratégia é mensal.

Contratos Futuros
=================

Os contratos futuros considerados dizem respeito a ativos financeiros de diversas classes, como ações, títulos de dívida, moedas e *commodities*.

Fatores Considerados
====================

A estratégia considera apenas os retornos e a volatilidade dos contratos futuros.

Análise Econométrica
====================

Os contratos futuros são analisados por meio de modelos autoregressivos que consideram tanto os retornos quanto a volatilidade dos contratos futuros.

Análise de Performance da Estratégia
====================================

A performance das diferentes especificações da estratégia (tanto considerando cada ativo individualmente quanto a carteira com *n* ativos) é calculada a partir dos dados históricos, e comparada à performance de *benchmarks*.

Contrução do Portfolio
======================

A partir dos resultados da análise de performance histórica, são definidos o peso de cada ativo e se a estratégia estará comprada ou vendida em cada ativo.

Sobre o Aplicativo
==================

O aplicativo foi desenvolvido em Python e executado por meio de um container Docker. As bibliotecas **numpy**, **pandas** e **statsmodels** foram utilizadas para as análises e contrução do portfolio.
