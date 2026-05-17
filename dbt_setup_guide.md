# Guia de Configuração e Inicialização do dbt

Este documento serve como um guia rápido com os comandos essenciais para configurar o ambiente virtual do Python, inicializar o dbt e resolver erros comuns de conexão com o banco de dados Supabase.

---

## 1. Configurando o Ambiente Virtual Python (.venv)

Para isolar as dependências do projeto e evitar conflitos com outras instalações no seu computador, utilizamos um ambiente virtual.

**Passo a passo no terminal do Windows (PowerShell):**

1. **Criar o ambiente virtual:**
   ```powershell
   python -m venv .venv
   ```

2. **Ativar o ambiente virtual:**
   ```powershell
   .venv\Scripts\activate
   ```
   *(Quando ativado, o prefixo `(.venv)` aparecerá no início da linha do terminal)*

3. **Instalar o dbt e o adaptador do Postgres:**
   ```powershell
   pip install dbt-core dbt-postgres
   ```

---

## 2. Comandos Principais do dbt

Com o ambiente virtual ativado, você pode interagir com o seu projeto dbt. Certifique-se de navegar para dentro da pasta do projeto dbt antes de rodá-los (ex: `cd EcommerceAoVivo`).

- **Testar a conexão com o banco de dados:**
  ```bash
  dbt debug
  ```
- **Instalar dependências de pacotes externos (se houver):**
  ```bash
  dbt deps
  ```
- **Carregar arquivos CSV (seeds) para o banco:**
  ```bash
  dbt seed
  ```
- **Rodar os modelos (transformar os dados):**
  ```bash
  dbt run
  ```
- **Rodar os testes de qualidade:**
  ```bash
  dbt test
  ```

---

## 3. Resolução de Erro de Conexão: Supabase (IPv6 vs IPv4)

### O Problema
Ao tentar rodar `dbt debug`, você pode se deparar com o seguinte erro:
```text
> Database Error
could not translate host name "db.[seu-codigo].supabase.co" to address: Name or service not known
```

### Por que isso acontece?
O Supabase atualizou recentemente sua infraestrutura. O endereço de conexão direta (que começa com `db...`) agora resolve **apenas para endereços IPv6**. 

Se o seu computador ou provedor de internet (ISP) não tiver suporte para IPv6 e forçar o uso do protocolo antigo (IPv4), o terminal não conseguirá encontrar o servidor de banco de dados, causando o erro de "Name or service not known" (Nome ou serviço desconhecido).

### A Solução
Você precisa usar o endereço **Connection Pooler** (IPv4) que o Supabase fornece gratuitamente, no lugar do endereço de conexão direta.

1. Vá ao painel do Supabase.
2. Acesse **Project Settings** > **Database**.
3. Na seção "Connection string / Parameters", garanta que você está visualizando os dados para **IPv4** (geralmente ligado ao Connection Pooling).
4. Edite o seu arquivo oculto do dbt localizado em `C:\Users\SEU_USUARIO\.dbt\profiles.yml`.
5. Substitua o `host` e o `user` pelos valores fornecidos no Pooler do Supabase. 

**Exemplo de como o arquivo `profiles.yml` deve ficar:**
```yaml
EcommerceAoVivo:
  outputs:
    dev:
      type: postgres
      threads: 1
      dbname: postgres
      schema: public
      port: 5432
      # Usar o Host do Pooler (contém "pooler" no nome)
      host: aws-1-us-west-1.pooler.supabase.com
      
      # O usuário muitas vezes requer o id do projeto junto
      user: postgres.qucqitfosffiluxdqqss 
      
      pass: "sua_senha_aqui"
  target: dev
```

Após fazer a substituição e salvar o arquivo, basta rodar `dbt debug` novamente.

---

## 5. Retomando o Projeto após Desligar o Computador

Sempre que você desligar o computador e quiser retomar o trabalho no seu projeto dbt, você não precisa configurar o `profiles.yml` ou rodar o `dbt init` novamente. Esses passos são feitos apenas na primeira vez.

Para voltar a trabalhar e conectar ao Supabase, siga estes passos:

1. **Abra o terminal** no seu editor de código (VS Code, Cursor, etc) ou abra o PowerShell separadamente.

2. **Ative o seu Ambiente Virtual (Muito Importante!)**:
   Você não precisa instalar o dbt ou criar o `.venv` novamente, pois eles já estão salvos no seu computador. Porém, você precisa "ligar" o ambiente virtual toda vez que abrir um novo terminal para que o Windows saiba onde o dbt está instalado.
   Para ativar, certifique-se de estar na pasta onde você criou o `.venv` e rode:
   ```bash
   .venv\Scripts\activate
   ```
   *(Você saberá que deu certo quando aparecer `(.venv)` no início da linha do seu terminal)*

3. **Navegue até a pasta do seu projeto dbt** (onde está o arquivo `dbt_project.yml`):
   ```bash
   cd c:\herbert\Cursos\CURSOS\ProjetoEcommerce_sql\aula03\ProjetoEcommerceAntigravity\EcommerceAoVivo
   ```

4. **Teste a conexão com o banco de dados**:
   Execute o comando de debug para garantir que a comunicação com o Supabase está funcionando corretamente:
   ```bash
   dbt debug
   ```
   *Se a mensagem for `All checks passed!`, você já está conectado e pronto para continuar.*

5. **Comandos do dia a dia**:
   A partir daqui, a conexão está ativa e você pode usar os comandos normais do dbt para trabalhar com seus dados no Supabase:
   - `dbt run`: para construir/atualizar as tabelas e views no Supabase.
   - `dbt test`: para validar a qualidade dos dados.
   - `dbt docs generate` e `dbt docs serve`: para atualizar e abrir a documentação do projeto.
