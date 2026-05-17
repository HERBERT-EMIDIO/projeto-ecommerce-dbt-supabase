# Projeto E-commerce Data Pipeline

Este repositório contém a infraestrutura e as transformações de dados para um projeto de E-commerce, utilizando uma stack moderna de Data Warehouse.

## 🚀 Arquitetura e Tecnologias

- **Banco de Dados (Data Warehouse):** PostgreSQL via [Supabase](https://supabase.com/).
- **Transformação de Dados:** [dbt (data build tool)](https://www.getdbt.com/) executado localmente.
- **Linguagem:** SQL (para modelos) e Python (para gerenciamento do ambiente).

## 📁 Estrutura do Projeto

- `/EcommerceAoVivo`: Contém o projeto dbt em si (modelos, testes, macros).
- `dbt_setup_guide.md`: Guia de configuração e comandos úteis do dbt.
- `git_setup_guide.md`: Guia para versionamento e envio para o GitHub.
- `architecture.md`: Documentação técnica da arquitetura de dados (se aplicável).

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
