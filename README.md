📊 Análise Estatística e Classificação de Tráfego de Rede

Este projeto apresenta uma abordagem completa de Ciência de Dados aplicada a fluxos de rede. O objetivo principal é extrair insights sobre o comportamento do tráfego, prever a duração de conexões e classificar a natureza dos pacotes (normal vs. anomalia/ataque) utilizando algoritmos de Machine Learning.

📑 Índice

Visão Geral do Projeto

Estrutura de Arquivos

Instalação e Uso

Internacionalização (traducao.py)

Resultados: Regressão

Resultados: Classificação

Conclusão e Diagnósticos

🔭 Visão Geral do Projeto

A análise divide-se em duas frentes principais:

Regressão (Previsão Contínua): Tentativa de prever a variável duracao_fluxo baseada em métricas volumétricas (total de pacotes enviados/recebidos). Comparamos abordagens lineares simples com abordagens polinomiais para capturar a complexidade da rede.

Classificação (Categórica): Comparação entre modelos probabilísticos (Naive Bayes) e determinísticos (Regressão Logística) para categorizar o tráfego com alta precisão.

🗂 Estrutura de Arquivos

A organização do repositório é direta para facilitar a reprodução dos experimentos:

notebook_analise.ipynb: O "cérebro" do projeto. Notebook Jupyter contendo a limpeza de dados, análise exploratória (EDA), treino dos modelos e plotagem de gráficos.

traducao.py: [Novo] Módulo utilitário contendo dicionários de mapeamento para traduzir as colunas técnicas do inglês para o português, facilitando a leitura dos gráficos por stakeholders não-técnicos.

datasets/: Pasta destinada aos arquivos .csv brutos.

🛠 Instalação e Uso

Para reproduzir este estudo, certifique-se de ter um ambiente Python configurado.

Instale as dependências:

pip install pandas numpy matplotlib seaborn scikit-learn statsmodels


Execute a análise:
Abra o arquivo notebook_analise.ipynb no Jupyter Notebook ou VS Code e execute as células sequencialmente.

🌐 Internacionalização (traducao.py)

Para tornar a análise acessível, implementamos um módulo de tradução automática das variáveis do dataset.

Como funciona:
O arquivo traducao.py exporta um dicionário chamado mapa_traducao. Ao carregar os dados, aplicamos este mapa para renomear as colunas.

Exemplo de Código:

import pandas as pd
from traducao import mapa_traducao

# Carregamento
df = pd.read_csv('datasets/trafego.csv')

# Aplicação da tradução
df_pt = df.rename(columns=mapa_traducao)

# Agora as colunas são legíveis, ex: 'fwd_pkts_tot' vira 'Total de Pacotes Enviados'
print(df_pt.head())


📈 Resultados: Regressão (Previsão de Duração)

O objetivo foi prever o tempo de duração de um fluxo de rede. Testamos se a relação entre pacotes e tempo é uma linha reta ou uma curva.

Modelo

R² (R-Quadrado)

RMSE (Erro Médio)

Interpretação

Linear Múltipla

0.52 (52%)

93.49

O modelo "sofre" para explicar a variância. Assume que o aumento de pacotes aumenta o tempo de forma constante, o que não é verdade em redes congestionadas.

Polinomial (Grau 2)

0.76 (76%)

57.62

Vencedor. A adição de curvatura ao modelo permitiu capturar 24% a mais da variabilidade dos dados e reduziu o erro grosseiro em quase 40%.

Insight: O tráfego de rede não é linear. O modelo polinomial adapta-se melhor aos picos e variações abruptas de transmissão.

🛡 Resultados: Classificação (Detecção de Tipos)

O objetivo foi classificar corretamente as amostras de tráfego.

Modelo

Acurácia

F1-Score

Matriz de Confusão (Erros)

Naive Bayes

94.61%

0.9702

~1.990 erros totais. Sofreu com falsos positivos na classe minoritária.

Regressão Logística

98.86%

0.9937

Vencedor. Apenas ~420 erros em mais de 36.000 testes.

Veredito: Para um sistema de produção (ex: Firewall ou IDS), a Regressão Logística é a única opção viável, oferecendo uma confiabilidade de quase 99%, enquanto o Naive Bayes geraria muitos alertas falsos.

🔬 Conclusão e Diagnósticos

A análise visual dos resíduos e métricas confirmou que:

Heterocedasticidade: A variância dos erros não é constante (observado no gráfico de Resíduos vs Preditos). O modelo polinomial mitigou isso, mas não eliminou totalmente.

Não-Normalidade: O teste Omnibus e o Q-Q Plot mostram que os dados de rede possuem "caudas pesadas" (muitos outliers extremos), o que é típico de dados de cibersegurança.

Multicolinearidade: O alto Condition Number sugere que variáveis como "Total de Pacotes" e "Pacotes por Segundo" são redundantes. Uma futura redução de dimensionalidade (PCA) é recomendada.

Autor: Augusto Rodrigues, César Ribeiro