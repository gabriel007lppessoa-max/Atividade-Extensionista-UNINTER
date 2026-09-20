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
