# Previsão de ingressantes no ensino superior privado de São Paulo

Projeto INEP – Censo da Educação Superior (2015–2024).
Análise exploratória e comparação de abordagens de regressão linear para prever o número de
ingressantes em vagas novas no ano seguinte (*t+1*), por curso e instituição, nas modalidades
Presencial e EAD.

## Conteúdo

| Arquivo | Descrição |
|---|---|
| `regression.ipynb` | Notebook com exploração dos dados, modelagem (presencial e EAD) e conclusões |
| `requirements.txt` | Dependências Python |
| `.env.example` | Modelo das variáveis de ambiente de conexão ao Snowflake |

## Como executar

1. Criar e ativar um ambiente virtual e instalar as dependências:

   ```bash
   python -m venv .venv
   .venv\Scripts\activate
   pip install -r requirements.txt
   ```

2. Copiar `.env.example` para `.env` e preencher as credenciais do Snowflake
   (o `.env` não é versionado).

3. Abrir `regression.ipynb` e executar as células em ordem.

## Dados

Os dados são lidos do Snowflake (banco `PROJETO_INEP`), em arquitetura por camadas
(STAGE → TRUSTED → ANALYTICS), a partir dos Microdados do Censo da Educação Superior do INEP.

## Principais resultados

- Em ambas as modalidades, o histórico do próprio curso explica quase toda a previsão: o modelo
  linear proporcional `y(t+1) = b · y(t)` é simples e competitivo.
- Modelos em escala logarítmica e com efeitos fixos apresentaram desempenho inferior.
- No EAD, o Censo não registra vagas nem inscrições; a previsão é mais precisa no nível da instituição.
- Restringir a análise às entidades presentes nos 10 anos (painel balanceado) foi testado e descartado como modelo principal por introduzir viés de sobrevivência; fica como análise de robustez (seção 5 do notebook).

O detalhamento está na seção "Conclusões e recomendações" do notebook.
