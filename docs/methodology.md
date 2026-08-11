# Metodologia de Análise Financeira e Arquitetura do Modelo - LTX Industrial

## 1. Visão Geral do Projeto
Este repositório contém o modelo de dados financeiro, scripts de análise de performance executiva e documentação técnica da **LTX Industrial**. A arquitetura foi desenvolvida para suportar análises de Controladoria, FP&A (Financial Planning and Analysis), Gestão de Custos e Análise de Liquidez Operacional.

---

## 2. Estrutura dos Dados e Dicionário de Variáveis
A base primária `data/financial_data.csv` consiste em 36 séries temporais mensais (2023 - 2025) cobrindo duas unidades operacionais distintas:
1. **LTX Industrial - Divisão Metalmecânica** (Operação principal de alta escala).
2. **LTX Industrial - Divisão Automação** (Operação de alta tecnologia e margem diferenciada).

### Dicionário de Dados:
| Campo | Tipo | Descrição / Fórmula |
| :--- | :--- | :--- |
| `date` | Date | Data de referência do fechamento mensal (`YYYY-MM-01`). |
| `year` | Int | Ano fiscal de apuração. |
| `month` | Int | Mês do período financeiro (1 a 12). |
| `business_unit` | String | Divisão de negócios correspondente. |
| `revenue` | Float | Receita Bruta Consolidada. |
| `cogs` | Float | Custo dos Produtos Vendidos (Matéria-prima, MO direta, overhead de fábrica). |
| `gross_profit` | Float | **Lucro Bruto**: `revenue - cogs`. |
| `opex` | Float | **Despesas Operacionais**: Vendas, Gerais e Administrativas (SG&A). |
| `ebitda` | Float | **EBITDA**: `gross_profit - opex`. |
| `capex` | Float | Investimentos em Capital Fixo e Modernização de Ativos. |
| `accounts_receivable` | Float | Saldo de Contas a Receber no Fechamento. |
| `inventory` | Float | Saldo de Estoques Totais (MP, WIP, PA). |
| `accounts_payable` | Float | Saldo de Contas a Pagar a Fornecedores. |
| `operating_cash_flow` | Float | **Fluxo de Caixa Operacional (FCO)**. |
| `net_cash_flow` | Float | **Fluxo de Caixa Líquido**: `operating_cash_flow - capex`. |

---

## 3. Metodologia de Cálculo dos KPIs
Para manter o alinhamento com os padrões de FP&A corporativo, aplicam-se as seguintes métricas no notebook `analysis/financial_analysis.ipynb`:

### A. Indicadores de Lucratividade
- **Margem Bruta (%)**: `(Gross Profit / Revenue) * 100`
- **Margem EBITDA (%)**: `(EBITDA / Revenue) * 100`
- **Eficiência Operacional (OPEX / Revenue %)**: `(OPEX / Revenue) * 100`

### B. Gestão de Capital de Giro e Ciclo Financeiro
- **DSO (Days Sales Outstanding)**: `(Accounts Receivable / Revenue) * 30` *(Dias médios de recebimento)*
- **DIO (Days Inventory Outstanding)**: `(Inventory / COGS) * 30` *(Dias médios de giro de estoque)*
- **DPO (Days Payables Outstanding)**: `(Accounts Payable / COGS) * 30` *(Dias médios de pagamento a fornecedores)*
- **Ciclo de Conversão de Caixa (CCC)**: `DSO + DIO - DPO`

---

## 4. Governança e Melhores Práticas de Repositório
- **Reprodutibilidade**: Todo o pipeline de análise é executado via Python (`pandas`, `numpy`, `seaborn`).
- **Escalabilidade**: A estrutura de dados permite extensão para novos níveis de detalhe (ex: cliente/produto) mantendo a integridade histórica.
- **Formato Open-Standard**: Arquivos em `.csv` padrão UTF-8 e `.ipynb` documentado para rápida auditabilidade por times de BI e Finanças.

