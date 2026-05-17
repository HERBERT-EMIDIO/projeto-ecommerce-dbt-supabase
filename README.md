# Projeto E-commerce Data Pipeline

Este repositório contém a infraestrutura e as transformações de dados para um projeto de E-commerce, utilizando uma stack moderna de Data Warehouse.

## 🚀 Arquitetura e Tecnologias

- **Banco de Dados (Data Warehouse):** PostgreSQL via [Supabase](https://supabase.com/).
- **Transformação de Dados:** [dbt (data build tool)](https://www.getdbt.com/) executado localmente.
- **Linguagem:** SQL (para modelos) e Python (para gerenciamento do ambiente).

## 📁 Estrutura do Projeto e Arquitetura Medalhão

O projeto dbt (`/EcommerceAoVivo`) segue a **Arquitetura Medalhão** para organizar a maturidade e a qualidade dos dados. As configurações avançadas estão definidas no arquivo `dbt_project.yml`, o que inclui a criação de schemas específicos por camada, definição de variáveis globais e uso de tags:

- **Camada Bronze (`models/bronze/`)**: Dados brutos originados da fonte (`raw`). O dbt está configurado para materializar essas tabelas como **Views** diretamente no schema `bronze` do Supabase, o que garante acesso aos dados no estado original sem duplicação de armazenamento.
- **Camada Silver (`models/silver/`)**: Dados limpos e padronizados. Materializados no schema `silver`. É nesta camada que realizamos tratamentos de tipos (como arredondamento financeiro para 2 casas decimais) e enriquecimentos de negócio (como a coluna de `classificacao_preco` via CASE WHEN).
- **Camada Gold (`models/gold/`)**: KPIs e tabelas prontas para consumo de BI (Data Marts). O dbt está configurado para separar os schemas por área de negócio, por exemplo: `gold_sales`, `gold_cs`, e `gold_pricing`.

### 🗂️ Arquivos Adicionais
- `EcommerceAoVivo/models/_sources.yml`: Mapeamento documentado de todas as fontes de dados brutas do banco de dados, incluindo a descrição individual de cada coluna.
- `dbt_setup_guide.md`: Guia de configuração e comandos úteis do dbt no dia a dia.
- `git_setup_guide.md`: Guia para versionamento e envio de código para o GitHub.
- `explicacao_projeto.md`: Documentação técnica sobre o contexto do negócio e dados.
## 🛠️ Como executar localmente

1. **Clone este repositório:**
   ```bash
   git clone https://github.com/SEU_USUARIO/projeto-ecommerce-dbt-supabase.git
   ```

2. **Ative o ambiente virtual Python:**
   *(É necessário ter o dbt-postgres instalado no seu ambiente)*
   ```bash
   .venv\Scripts\activate
   ```

3. **Configure as credenciais do banco:**
   Certifique-se de configurar o arquivo `profiles.yml` na sua máquina local com as credenciais do Supabase.

4. **Navegue até o projeto dbt:**
   ```bash
   cd EcommerceAoVivo
   ```

5. **Teste a conexão e execute os modelos:**
   ```bash
   dbt debug
   dbt run
   dbt test
   ```

## 📚 Documentação dos Dados

A documentação gerada pelo dbt sobre os modelos, linhagem de dados e testes pode ser acessada rodando:
```bash
dbt docs generate
dbt docs serve
```
Isso abrirá uma interface web local com toda a documentação da linhagem dos dados.

### 🖼️ Visualização da Linhagem (Lineage Graph)
Abaixo, exemplos da documentação e do gráfico de linhagem (Lineage Graph) gerados automaticamente pelo dbt mostrando o fluxo dos dados desde a origem (Raw) até a camada de negócios (Gold):

![Lineage Graph do Projeto](img/lineage_graph.png)

![Interface do dbt docs](img/dbt_docs.png)
