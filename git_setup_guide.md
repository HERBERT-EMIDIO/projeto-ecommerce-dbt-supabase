# Guia de Configuração do Git e GitHub

Este guia descreve o passo a passo para versionar o seu projeto de Data Warehouse (dbt + Supabase) usando Git e enviá-lo para o GitHub.

## 1. Nome Sugerido para o Repositório no GitHub
Recomendamos um nome descritivo e profissional:
- **`projeto-ecommerce-dbt-supabase`**
- *Alternativas:* `ecommerce-data-pipeline`, `data-warehouse-ecommerce`

## 2. Passo a Passo: Criando o Repositório no GitHub
1. Acesse sua conta no [GitHub](https://github.com/).
2. No canto superior direito, clique no botão **`+`** e selecione **`New repository`**.
3. Em **Repository name**, digite o nome sugerido (ex: `projeto-ecommerce-dbt-supabase`).
4. Selecione **Public** ou **Private** (Privado é recomendado se o código for estritamente pessoal, mas Público é ótimo para portfólio).
5. **Não** marque a opção "Add a README file" (nós já criamos um localmente na sua máquina).
6. Clique no botão verde **`Create repository`**.

## 3. Passo a Passo: Configurando o Git Localmente
Abra o seu terminal (PowerShell ou no VS Code), certifique-se de estar na pasta raiz do projeto (`c:\herbert\Cursos\CURSOS\ProjetoEcommerce_sql\aula03\ProjetoEcommerceAntigravity`) e execute os comandos abaixo na ordem:

### Passo A: Inicializar o repositório
```bash
git init
```
*Isso cria a pasta oculta `.git` no seu projeto, avisando que agora ele é rastreado pelo Git.*

### Passo B: Adicionar os arquivos ao pacote ("Stage")
```bash
git add .
```
*O ponto `.` significa "adicione todos os arquivos e pastas atuais" (exceto o que estiver no arquivo `.gitignore`).*

### Passo C: Criar o primeiro "Commit"
```bash
git commit -m "commit inicial: estrutura do projeto dbt e documentacoes"
```
*Isso salva a "foto" atual do seu projeto com uma mensagem descritiva.*

### Passo D: Conectar seu projeto local com o GitHub
*Na página do GitHub, após criar o repositório, ele vai te mostrar um comando parecido com este. Copie de lá e cole no terminal:*
```bash
git remote add origin https://github.com/SEU_USUARIO/projeto-ecommerce-dbt-supabase.git
```
*(Lembre-se de substituir pela URL correta do seu repositório)*

### Passo E: Alterar a branch principal para 'main'
```bash
git branch -M main
```

### Passo F: Enviar (Push) os arquivos para o GitHub
```bash
git push -u origin main
```
*Isso enviará seus códigos para a nuvem. Uma janela pode abrir pedindo para você autorizar o login com sua conta do GitHub.*

---

## 4. Comandos Git do Dia a Dia

Sempre que você fizer alterações no projeto (modificar um modelo dbt, adicionar documentação, etc), precisará salvar essas alterações no GitHub. A sequência que você fará constantemente é:

1. **Ver o que foi alterado:**
   ```bash
   git status
   ```
2. **Adicionar as alterações:**
   ```bash
   git add .
   ```
3. **Salvar com uma mensagem:**
   ```bash
   git commit -m "sua mensagem aqui explicando o que mudou"
   ```
   *Exemplo:* `git commit -m "adiciona modelo de faturamento de vendas"`
4. **Enviar para o GitHub:**
   ```bash
   git push
   ```

## 5. Dica sobre Segurança (.gitignore)
No seu projeto já incluímos um arquivo chamado `.gitignore`. Ele diz ao Git para ignorar pastas pesadas ou arquivos que não devem ir para a internet, como a pasta `.venv` e a pasta `target/` do dbt. Como as senhas do banco de dados (o arquivo `profiles.yml`) ficam salvas fora dessa pasta (na pasta do seu usuário do Windows), elas já estão seguras por padrão!
