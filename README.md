# 📊 Análise Estatística e Classificação de Tráfego de Rede

Este projeto apresenta uma abordagem completa de Ciência de Dados aplicada a fluxos de rede. O objetivo principal é extrair insights sobre o comportamento do tráfego, prever a duração de conexões e classificar a natureza dos pacotes (normal vs. anomalia/ataque) utilizando algoritmos de Machine Learning.

# Dataset:

[Dataset](https://archive.ics.uci.edu/dataset/942/rt-iot2022)

## 📑 Índice
- [Visão Geral do Projeto](#-visão-geral-do-projeto)
- [Estrutura de Arquivos](#-estrutura-de-arquivos)
- [Instalação e Uso](#-instalação-e-uso)
- [Internacionalização](#-internacionalização-traducaopy)
- [Resultados: Regressão](#-resultados-regressão-previsão-de-duração)
- [Resultados: Classificação](#-resultados-classificação-detecção-de-tipos)
- [Conclusão e Diagnósticos](#-conclusão-e-diagnósticos)

---

## 🔭 Visão Geral do Projeto

A análise divide-se em duas frentes principais:

1.  **Regressão (Previsão Contínua):** Tentativa de prever a variável `duracao_fluxo` baseada em métricas volumétricas (total de pacotes enviados/recebidos). Comparamos abordagens lineares simples com abordagens polinomiais para capturar a complexidade da rede.
2.  **Classificação (Categórica):** Comparação entre modelos probabilísticos (Naive Bayes) e determinísticos (Regressão Logística) para categorizar o tráfego com alta precisão.

## 🗂 Estrutura de Arquivos

A organização do repositório é direta para facilitar a reprodução dos experimentos:

- **`main`**: O "cérebro" do projeto. Notebook Jupyter contendo a limpeza de dados, análise exploratória (EDA), treino dos modelos e plotagem de gráficos.
- **`traducao.py`**: *[Novo]* Módulo utilitário contendo dicionários de mapeamento para traduzir as colunas técnicas do inglês para o português, facilitando a leitura dos gráficos por stakeholders não-técnicos.
- **`requirements.txt`**: Arquivo para baixar as dependencias

## 🛠 Instalação e Uso

Para reproduzir este estudo, certifique-se de ter um ambiente Python configurado.

**1. Instale as dependências:**
```bash
pip install -r requirements.txt
```
2. Execute a análise: Abra o arquivo main.ipynb no Jupyter Notebook ou VS Code e execute as células sequencialmente.

## Licença:

This dataset is licensed under a Creative Commons Attribution 4.0 International (CC BY 4.0) license.

This allows for the sharing and adaptation of the datasets for any purpose, provided that the appropriate credit is given.