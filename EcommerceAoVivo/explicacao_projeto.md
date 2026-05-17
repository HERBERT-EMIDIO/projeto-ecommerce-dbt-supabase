# Guia Mestre: Arquitetura de Dados e Data Warehouse E-commerce

Este documento fornece uma visão detalhada do projeto de dados, sua estrutura multi-projeto e os conceitos fundamentais de Data Warehouse que sustentam esta implementação.

## 1. Estrutura do Projeto e Ecossistema

Atualmente, o repositório é composto por três frentes de trabalho dbt principais, cada uma com um propósito distinto dentro do ciclo de aprendizado e desenvolvimento:

- **`EcommerceAoVivo/` (NOVO):** O projeto principal e atual onde estamos configurando a conexão direta com o Supabase. Este será o ambiente onde a lógica de negócio real do e-commerce será implementada.
- **`ecommerce_projeto/`:** Um projeto inicial de base, servindo como primeira estrutura de testes para transformações dbt.
- **`jaffle_shop/`:** O projeto de referência da comunidade dbt. Ele é essencial para entender as melhores práticas de modelagem (como separar staging de marts) e como lidar com entidades clássicas de e-commerce (clientes, pedidos e pagamentos).

### Tecnologias Utilizadas (Modern Data Stack)
1. **Supabase (PostgreSQL):** Nossa fonte de dados transacional e, simultaneamente, nosso destino analítico (Data Warehouse).
2. **dbt (Data Build Tool):** A ferramenta de orquestração de transformações SQL. Ela não move os dados para fora do banco, mas ordena ao banco como transformá-los.
3. **Python (.venv):** O motor que executa o dbt e gerencia as bibliotecas necessárias para a comunicação com o banco de dados.

---

## 2. O Conceito de Data Warehouse (DW)

Um **Data Warehouse** é o "cérebro" analítico de uma empresa. Enquanto o banco de dados do seu site (Supabase/OLTP) precisa ser rápido para salvar um novo pedido, o Data Warehouse (OLAP) precisa ser rápido para **responder perguntas complexas**.

### Pilares de um DW de Sucesso:
- **Consolidação:** Reúne dados que poderiam estar espalhados em diferentes lugares.
- **Histórico:** Permite comparar o faturamento de hoje com o mesmo dia do ano passado.
- **Confiabilidade:** Aplica testes de dados (via dbt) para garantir que não existam pedidos sem clientes ou valores negativos onde não deveriam existir.

---

## 3. Arquitetura de Camadas (The dbt Way)

No seu projeto, seguiremos a arquitetura de camadas recomendada para Data Warehouses modernos:

### Camada 1: Staging (O Espelho)
*   **Pasta:** `models/staging`
*   **Objetivo:** Limpeza básica. Renomear colunas confusas, converter tipos de dados (ex: string para date) e remover duplicatas.
*   **Regra:** Um modelo de staging para cada tabela da fonte.

### Camada 2: Intermediate (A Cozinha)
*   **Pasta:** `models/intermediate`
*   **Objetivo:** Onde a mágica acontece. Aqui unimos tabelas (joins) e criamos lógicas complexas que serão usadas em múltiplos lugares.

### Camada 3: Marts (O Cardápio)
*   **Pasta:** `models/marts`
*   **Objetivo:** Tabelas prontas para o usuário final ou ferramentas de BI.
*   **Exemplos:** `fct_vendas` (tabela de fatos com cada venda) e `dim_produtos` (tabela de dimensões com detalhes dos produtos).

---

## 4. Próximos Passos Recomendados

Para que o seu Data Warehouse ganhe vida no projeto **`EcommerceAoVivo`**, os passos técnicos são:

1.  **Validar Conexão:** Garantir que o `dbt debug` retorne sucesso (corrigindo a senha no `profiles.yml` conforme orientado anteriormente).
2.  **Mapear Sources:** Criar o arquivo `src_ecommerce.yml` para declarar as tabelas brutas que existem no seu Supabase.
3.  **Criar Primeiros Modelos:** Iniciar pela camada de `staging` para organizar os dados brutos.

---
*Este documento é evolutivo e deve ser atualizado conforme novas fontes de dados ou lógicas de negócio forem incorporadas ao ecossistema do EcommerceAoVivo.*
