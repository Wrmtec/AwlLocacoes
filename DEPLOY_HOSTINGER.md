# Guia de Publicação na Hostinger

Este guia irá ajudá-lo a colocar o seu site no ar utilizando a hospedagem da Hostinger.

## Pré-requisitos
1. Uma conta na Hostinger com um plano de hospedagem ativo.
2. Um domínio configurado e apontando para a Hostinger (DNS propagado).

## Passo a Passo

### 1. Preparar os Arquivos
Para facilitar o envio, **já criei um arquivo compactado** chamado `site_package.zip` na pasta do seu projeto. Este arquivo contém:
- `index.html` (Página principal)
- `style.css` (Estilos)
- `script.js` (Funcionalidades)
- `assets/` (Imagens e outros recursos)

### 2. Acessar o Gerenciador de Arquivos
1. Faça login no **hPanel** (painel da Hostinger).
2. No painel principal, localize a seção **Arquivos** e clique em **Gerenciador de Arquivos**.
3. Selecione o seu domínio (se houver mais de um).

### 3. Enviar o Arquivo
1. Dentro do Gerenciador de Arquivos, abra a pasta **public_html**.
   - **Atenção:** Esta é a pasta raiz do seu site. Arquivos fora dela não serão acessíveis publicamente.
2. Se houver um arquivo `default.php` ou `index.php` padrão da Hostinger, você pode deletá-lo.
3. Clique no ícone de **Upload** (geralmente uma seta para cima ou nuvem) no canto superior direito.
4. Selecione o arquivo **Arquivo** e escolha o `site_package.zip` que está na pasta do seu projeto.

### 4. Extrair e Publicar
1. Após o upload, localize o arquivo `site_package.zip` na lista.
2. Clique com o botão direito sobre ele e selecione **Extract** (Extrair).
3. Uma janela abrirá perguntando o destino. Deixe como está (geralmente `/public_html` ou `.`) e clique em **Extract**.
4. Os arquivos `index.html`, `style.css`, etc., deverão aparecer na pasta `public_html`.
   - **Nota:** Certifique-se de que os arquivos estão soltos dentro da `public_html` e não dentro de uma subpasta. Se estiverem em uma subpasta, entre nela, selecione tudo, mova para `../` (diretório anterior/public_html).

### 5. Finalizar
1. (Opcional) Você pode deletar o arquivo `site_package.zip` do servidor para economizar espaço.
2. Acesse seu domínio no navegador (ex: `www.suaempresa.com.br`) e verifique se o site está carregando corretamente.
3. Teste em dispositivos móveis e desktop para garantir que tudo está perfeito.

## Solução de Problemas Comuns
- **Erro 403 Forbidden:** Verifique se o arquivo principal se chama `index.html` (tem que ser tudo minúsculo).
- **Estilos ou Imagens não carregam:** Verifique se a pasta `assets` foi extraída corretamente e se os caminhos no código estão relativos (ex: `assets/images/logo.png`).
- **Cache:** Se você atualizou o arquivo e não vê as mudanças, tente limpar o cache do navegador ou acessar com uma aba anônima (Ctrl+Shift+N).

## 🚀 Deploy Automático (GitHub Actions)

Para que o site seja atualizado automaticamente toda vez que você fizer um commit no GitHub, siga estes passos:

### 1. Obter Dados de FTP na Hostinger
1. No **hPanel**, vá em **Arquivos** > **Contas FTP**.
2. Anote o **Hostname FTP** (geralmente algo como `ftp.seudominio.com` ou um IP).
3. Anote o **Usuário FTP** e a **Senha FTP** (se não souber, pode alterar a senha ali mesmo).

### 2. Configurar "Secrets" no GitHub
1. Vá até o seu repositório no GitHub.
2. Clique na aba **Settings** (Configurações).
3. No menu lateral esquerdo, vá em **Secrets and variables** > **Actions**.
4. Clique no botão verde **New repository secret**.
5. Adicione os seguintes segredos (um por um):
   - **Nome:** `FTP_SERVER`
     - **Valor:** O Hostname que você pegou na Hostinger.
   - **Nome:** `FTP_USERNAME`
     - **Valor:** O nome de usuário do FTP.
   - **Nome:** `FTP_PASSWORD`
     - **Valor:** A senha do FTP.

### 3. Pronto!
Agora, toda vez que você enviar uma alteração para o GitHub (`git push`), o GitHub Actions vai pegar os arquivos novos e enviar para a Hostinger automaticamente.
Você pode acompanhar o processo na aba **Actions** do seu repositório no GitHub.
