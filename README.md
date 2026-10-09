# simulador-investimentos-fiis
Simulador de investimentos em Fundos Imobiliários desenvolvido com Excel.
# Simulador de Investimentos em Fundos Imobiliários (FIIs)

## Sobre o projeto

Este projeto foi desenvolvido como parte do curso de **Analista de Dados com Excel com auxílio de IA e Claude**, com o objetivo de construir uma ferramenta de simulação de investimentos em Fundos de Investimento Imobiliário (FIIs).

A proposta é transformar uma planilha tradicional em uma ferramenta com aparência de aplicativo, permitindo que o usuário visualize projeções de patrimônio e dividendos a partir de parâmetros financeiros personalizados.

O simulador utiliza fórmulas do Excel, intervalos nomeados e uma tabela de referência para automatizar cálculos e facilitar a análise de diferentes cenários de investimento.

## 1. Perguntas de negócio respondidas pela ferramenta

A ferramenta foi construída para responder a cinco perguntas principais:

- **Quanto investir por mês?**  
  O usuário informa o valor que pretende investir mensalmente na célula D16 da planilha `FIIS Agents`.

- **Por quantos anos investir?**  
  O período de investimento é definido na célula D17, permitindo simular a acumulação de patrimônio ao longo do tempo.

- **Qual a taxa de rendimento mensal?**  
  A taxa mensal utilizada na simulação é informada na célula D18 e serve como parâmetro para os cálculos de patrimônio futuro.

- **Quanto de patrimônio será acumulado?**  
  O resultado é apresentado na célula D19. O cálculo considera o aporte mensal, o prazo de investimento e a taxa de rendimento mensal, estimando o valor futuro acumulado.

- **Quanto será recebido de dividendos por mês?**  
  A estimativa é apresentada na célula D20, calculada a partir do patrimônio projetado e da taxa de rendimento mensal da carteira definida na célula D12.

Além dessas respostas, a ferramenta apresenta cenários de acumulação para diferentes períodos e uma sugestão de distribuição dos investimentos entre categorias de FIIs, conforme o perfil selecionado.

## 2. Utilização das funções VF e PROCV

### Função VF — Valor Futuro

A função VF é utilizada para estimar o patrimônio acumulado ao final do período de investimento, considerando aportes mensais e uma taxa de rendimento constante.

Na célula D19 da planilha `FIIS Agents`, a fórmula utilizada é:

`=VF(taxa_mensal;qtd_anos*12;aporte*-1)`

A fórmula utiliza os seguintes parâmetros:

- `taxa_mensal`: taxa de rendimento mensal;
- `qtd_anos*12`: conversão do prazo de investimento de anos para meses;
- `aporte*-1`: valor do aporte mensal com sinal negativo, para representar a saída de dinheiro do investidor na convenção de sinais da função financeira.

O resultado é uma estimativa do patrimônio futuro acumulado. A mesma lógica é utilizada na projeção de cenários com prazos diferentes.

### Função PROCV — Pesquisa Vertical

A função PROCV é utilizada para localizar automaticamente o percentual de alocação correspondente ao perfil de investidor e ao tipo de FII.

Na planilha `FIIS Agents`, a fórmula utiliza uma chave formada pela combinação do perfil selecionado com a categoria do fundo. Essa chave é pesquisada na coluna A da planilha `TBL_CHAVE`, retornando o percentual correspondente à quarta coluna da tabela.

Exemplo da fórmula utilizada:

`=PROCV($C$30&"-"&B34;TBL_CHAVE!$A:$D;4;FALSO)`

A função permite que a distribuição percentual seja atualizada de acordo com o perfil escolhido, sem que seja necessário inserir manualmente cada percentual na planilha principal.

## 3. Intervalos nomeados

Foram criados intervalos nomeados para tornar as fórmulas mais legíveis, facilitar sua manutenção e identificar os parâmetros utilizados nos cálculos.

| Nome do intervalo | Célula | Finalidade |
|---|---|---|
| `salario` | D11 | Armazena o salário informado pelo usuário. |
| `rendimento_carteira` | D12 | Define a taxa de rendimento mensal utilizada na estimativa de dividendos. |
| `sugestao_investimento` | D13 | Calcula uma sugestão de investimento equivalente a 30% do salário. |
| `aporte` | D16 | Representa o valor investido mensalmente. |
| `qtd_anos` | D17 | Define o prazo do investimento em anos. |
| `taxa_mensal` | D18 | Armazena a taxa de rendimento mensal utilizada na projeção. |
| `patrimonio` | D19 | Identifica a célula que apresenta o patrimônio acumulado projetado. |

Esses intervalos permitem utilizar nomes descritivos nas fórmulas, facilitando a compreensão da lógica de cálculo e a manutenção da ferramenta.

## 4. Percentuais de cada perfil de investidor

A planilha `TBL_CHAVE` reúne os percentuais de distribuição por categoria de FII para três perfis de investidor: conservador, moderado e agressivo.

Os percentuais foram baseados no modelo do Expert utilizado como referência durante o desenvolvimento do projeto.

### Perfil conservador

| Tipo de FII | Percentual |
|---|---:|
| Papel | 30% |
| Tijolo | 50% |
| Híbridos | 10% |
| FOFs | 10% |
| Desenvolvimento | 0% |
| Hotelarias | 0% |
| **Total** | **100%** |

### Perfil moderado

| Tipo de FII | Percentual |
|---|---:|
| Papel | 32% |
| Tijolo | 35% |
| Híbridos | 8% |
| FOFs | 5% |
| Desenvolvimento | 10% |
| Hotelarias | 10% |
| **Total** | **100%** |

### Perfil agressivo

| Tipo de FII | Percentual |
|---|---:|
| Papel | 50% |
| Tijolo | 10% |
| Híbridos | 5% |
| FOFs | 5% |
| Desenvolvimento | 20% |
| Hotelarias | 10% |
| **Total** | **100%** |

A tabela de referência permite que a ferramenta identifique os percentuais de cada categoria por meio da função PROCV e calcule os valores sugeridos para distribuição do aporte mensal.

Os percentuais são parâmetros do modelo utilizado no projeto e possuem finalidade ilustrativa e educacional, não constituindo recomendação individualizada de investimento.

## 5. Alterações realizadas em relação à ferramenta do Expert

Em relação ao modelo utilizado como referência, foram realizadas personalizações visuais para conferir identidade própria à ferramenta.

As principais alterações foram:

- Criação e utilização de uma logomarca personalizada.
- Adaptação de cores para diferenciar visualmente os elementos da planilha.

A estrutura central de simulação e os parâmetros de distribuição por perfil foram mantidos com base no modelo de referência, enquanto as modificações visuais buscaram tornar a ferramenta mais personalizada e agradável de utilizar.
