# Atividade-Extensionista-UNINTER
Desenvolvimento de Infraestrutura de BI para Inclusão Digital e Apoio Decisório no Terceiro Setor.
# Desenvolvimento de Infraestrutura de Business Intelligence no Terceiro Setor

**Autor:** Gabriel Lourenço Pessoa da Silva (RU: 5296983)
**Instituição:** Centro Universitário Internacional UNINTER
**Curso:** CST em Ciência de Dados
**Local da Aplicação:** Bebedouro, São Paulo (SP)

## 📌 Sobre o Projeto
Este repositório contém a documentação e os scripts desenvolvidos para a **Atividade Extensionista II** do curso de Ciência de Dados. O projeto teve como objetivo implementar uma infraestrutura de Business Intelligence (BI) e promover a inclusão digital em uma Organização da Sociedade Civil (ONG) na cidade de Bebedouro-SP.

## 🎯 Objetivos Alcançados
1. **Estruturação de Dados:** Modelagem de banco de dados relacional para unificar registros operacionais (planilhas soltas e documentos em papel).
2. **Painel Gerencial:** Desenvolvimento de um dashboard automatizado em Microsoft Power BI para monitoramento de KPIs (atendimentos, finanças, projetos).
3. **Inclusão Digital:** Capacitação da equipe gestora da instituição com oficinas práticas de literacia de dados.

## 🛠️ Tecnologias Utilizadas
* **Microsoft Power BI:** Criação de dashboards, medidas DAX e modelagem de dados.
* **Power Query:** Processo de ETL (Extração, Transformação e Carga) para limpeza de bases fragmentadas.
* **SQL / Banco de Dados Relacional:** Estruturação da base central da instituição.

## 📊 Exemplos de Medidas DAX Utilizadas
Durante o projeto, várias métricas foram criadas para o acompanhamento gerencial da ONG. Exemplos:
- `Total_Atendimentos = COUNTROWS('Fato_Atendimentos')`
- `Custo_por_Projeto = DIVIDE(SUM('Fato_Despesas'[Valor]), [Total_Atendimentos], 0)`
- `Taxa_de_Evasao_Mensal = DIVIDE([Evasoes_Mes], [Total_Atendimentos], 0)`

## 🤝 Impacto Social (ODS)
Projeto alinhado aos Objetivos de Desenvolvimento Sustentável da ONU:
* ODS 8 - Trabalho decente e crescimento econômico
* ODS 9 - Indústria, inovação e infraestrutura

*/* 
===================================================================
PROJETO: Infraestrutura de BI para o Terceiro Setor (Bebedouro-SP)
AUTOR: Gabriel Lourenço Pessoa da Silva
DESCRIÇÃO: Arquivo contendo as principais medidas DAX desenvolvidas 
           para o painel gerencial da instituição filantrópica.
===================================================================
*/

// ==========================================
// 1. MÉTRICAS OPERACIONAIS (ATENDIMENTOS)
// ==========================================

// Calcula o número total de atendimentos realizados pela ONG
Total_Atendimentos = COUNTROWS('Fato_Atendimentos')

// Calcula a quantidade de famílias distintas que foram beneficiadas
Familias_Beneficiadas = DISTINCTCOUNT('Fato_Atendimentos'[ID_Familia])

// Conta quantos voluntários estão atualmente com status "Ativo"
Voluntarios_Ativos = 
CALCULATE(
    COUNTROWS('Dim_Voluntarios'),
    'Dim_Voluntarios'[Status] = "Ativo"
)

// ==========================================
// 2. MÉTRICAS FINANCEIRAS (RECEITAS E CUSTOS)
// ==========================================

// Soma total de recursos captados (doações, eventos, subsídios)
Total_Arrecadado = SUM('Fato_Financeiro'[Receitas])

// Soma total dos custos operacionais e despesas dos projetos
Custo_Operacional = SUM('Fato_Financeiro'[Despesas])

// Calcula o saldo disponível (Receitas - Despesas)
Saldo_Projetos = [Total_Arrecadado] - [Custo_Operacional]

// Verifica a eficiência financeira: Custo médio por cada atendimento realizado
Custo_Por_Atendimento = 
DIVIDE(
    [Custo_Operacional], 
    [Total_Atendimentos], 
    0
)

// ==========================================
// 3. INTELIGÊNCIA DE TEMPO (TIME INTELLIGENCE)
// ==========================================

// Calcula o total arrecadado no mês anterior para fins de comparação
Arrecadado_Mes_Anterior = 
CALCULATE(
    [Total_Arrecadado],
    DATEADD('Dim_Calendario'[Data], -1, MONTH)
)

// Calcula a variação percentual de arrecadação (Mês atual vs Mês anterior)
Variacao_Arrecadacao_MoM = 
DIVIDE(
    [Total_Arrecadado] - [Arrecadado_Mes_Anterior],
    [Arrecadado_Mes_Anterior],
    0
)

// Calcula o acumulado de arrecadação no ano (YTD - Year to Date)
Arrecadado_Acumulado_Ano = 
TOTALYTD(
    [Total_Arrecadado],
    'Dim_Calendario'[Data]
)

// ==========================================
// 4. FORMATAÇÃO CONDICIONAL
// ==========================================

// Medida para aplicar cor condicional no painel (Verde se saldo positivo, Vermelho se negativo)
Cor_Status_Financeiro = 
IF(
    [Saldo_Projetos] >= 0, 
    "#198754", // Verde
    "#DC3545"  // Vermelho
)
