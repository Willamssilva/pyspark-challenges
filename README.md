# 🛠️ Projeto de Engenharia de Dados: Pipeline de CRM no Databricks

## 📌 O Problema de Negócio
A equipe de visualização de dados (ferramentas como Power BI) precisava de acesso estruturado aos dados de clientes para campanhas de marketing. No entanto, os dados estavam armazenados em formato bruto (CSV) no Data Lake. O acesso direto ao arquivo cru era inviável por questões de governança, performance e falta de tratamento de dados (Data Quality).

## 💡 A Solução
Construção de um pipeline ETL (Extract, Transform, Load) utilizando **PySpark** no ambiente **Databricks**. O projeto aplica os conceitos da **Arquitetura Medalhão (Medallion Architecture)**, movendo os dados do estado bruto para um banco de dados estruturado e focado em CRM, pronto para o consumo das áreas de negócio.

## 🚀 Tecnologias e Ferramentas Utilizadas
* **Ambiente:** Databricks
* **Linguagens e Frameworks:** Apache Spark (PySpark), Spark SQL, Python
* **Armazenamento:** Databricks Volumes / Data Lake

## ⚙️ Transformações e Técnicas Aplicadas
Durante o desenvolvimento deste pipeline, as seguintes etapas de Engenharia de Dados foram executadas:

1. **Ingestão e Leitura:** Leitura do arquivo CSV bruto com inferência de schema e mapeamento de delimitadores.
2. **Data Quality (Qualidade de Dados):** Auditoria na base para identificar falsos nulos (strings literais `"NULL"`) mascarados no arquivo de texto, evitando falhas em agregações futuras.
3. **Enriquecimento (Camada Prata):** Criação de novas features para facilitar a criação de dashboards, como a união de colunas (`first_name` e `last_name`) utilizando a função `concat_ws`.
4. **Projeção e Filtragem (Camada Ouro):** Encadeamento de métodos (*Method Chaining*) para aplicar filtros regionais (ex: clientes do estado de NY) e selecionar estritamente as colunas necessárias para o time de CRM, otimizando o uso de memória e processamento.
5. **Boas Práticas de Arquitetura:** Separação clara entre comandos de **Transformação** (que garantem a imutabilidade do DataFrame) e **Ações** de visualização/contagem.
