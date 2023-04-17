.. post:: 2023-02
   :category: projeto
   :author: me
   :language: pt_BR

Engenharia e Exploração de Dados Meteorológicos
***********************************************

Neste projeto, realizei a agregação de dados distribuídos entre milhares de arquivos, além de fazer também a limpeza destes dados. Finalmente, realizei uma análise exploratória dos dados. O aplicativo foi desenvolvido em Python.

Engenharia de Dados
===================

Dados de diversos sensores, para todas as estações meteorológicas brasileiras, estavam distribuídos entre milhares de arquivos com algumas estruturas diferentes. Realizei a agregação dos dados em uma única base de dados, realizando a limpeza dos dados como parte do processo.

Análise Exploratória
====================

A análise exploratória teve duas partes, uma análise não visual de estatísticas descritivas (média, desvio padrão, etc.), e uma análise visual (gráfica) de dados faltantes, distribuição, tendências e sazonalidades.

Sobre o Aplicativo
==================

O aplicativo foi divido em três sub-aplicativos independentes (agregação e limpeza, descrição estatística, análise gráfica). Cada sub-aplicativo teve seu próprio pacote Python, e sua configuração definida por um arquivo TOML, de modo que a funcionalidade do sub-aplicativo pudesse ser modificada sem a necessidade de edição do código Python.