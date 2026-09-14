# Loja InovaTech

Catálogo digital responsivo para equipamentos de tecnologia, redes, servidores, datacenter e CFTV. O projeto foi desenvolvido como uma aplicação web estática, com Bootstrap no front-end, dados mockados em JavaScript e atendimento comercial iniciado pelo WhatsApp.

## Visão geral

O projeto oferece:

- catálogo de produtos com busca por nome, marca, modelo e tags;
- filtros por categoria, marca e condição do produto;
- ordenação por relevância, preço ou nome;
- paginação do catálogo;
- página individual com galeria, descrição, especificações, estoque e produtos relacionados;
- geração de mensagem de compra pré-preenchida para o WhatsApp;
- painel auxiliar para gerar o JSON de novos produtos;
- banner de consentimento de cookies com persistência em `localStorage`;
- interface responsiva baseada em Bootstrap 5 e Bootstrap Icons.

## Estrutura do projeto

| Arquivo | Responsabilidade |
| --- | --- |
| `index.html` | Página principal da loja, busca, filtros e catálogo. |
| `produto.html` | Estrutura da página de detalhes de um produto. |
| `cad-prod.html` | Formulário auxiliar de cadastro de produtos. |
| `loja-data.js` | Categorias, marcas e produtos mockados. |
| `loja.js` | Busca, filtros, ordenação, paginação e renderização do catálogo. |
| `produto.js` | Leitura do ID na URL e renderização dos detalhes do produto. |
| `cad-prod.js` | Conversão do formulário de cadastro em JSON compatível com `loja-data.js`. |
| `loja.css` | Estilos específicos da loja e dos cartões de produto. |
| `cookie-consent.js` | Consentimento de cookies e persistência da escolha do visitante. |
| `LICENSE` | Licença GNU GPL v3. |

## Requisitos

- navegador moderno com suporte a JavaScript ES6+;
- um servidor HTTP local ou hospedagem de arquivos estáticos;
- conexão com a internet para carregar Bootstrap, Bootstrap Icons e Animate.css via CDN;
- os arquivos compartilhados referenciados por `../src/` quando o projeto estiver integrado ao site principal.

Não existe processo de build ou gerenciador de dependências neste diretório.

## Execução local

### Visual Studio Code

1. Abra a pasta no Visual Studio Code.
2. Instale a extensão **Live Server**, caso ainda não esteja instalada.
3. Clique com o botão direito em `index.html` e selecione **Open with Live Server**.
4. Acesse a URL exibida pela extensão.

### Python

Com Python 3 instalado, execute na raiz do projeto:

```powershell
py -m http.server 5500
```

Depois, abra <http://localhost:5500>.

O uso de um servidor HTTP é recomendado porque os arquivos utilizam caminhos relativos, carregamento de recursos e APIs do navegador que podem apresentar comportamento diferente quando o HTML é aberto diretamente via `file://`.

## Rotas e uso

### Catálogo

Abra `index.html` para pesquisar produtos, selecionar uma categoria, aplicar filtros, ordenar os resultados e navegar entre páginas.

### Detalhes do produto

Os detalhes são acessados pelo parâmetro `id`:

```text
produto.html?id=1001
```

O ID deve corresponder a um produto existente em `loja-data.js`. IDs inválidos exibem uma página de produto não encontrado.

### Cadastro auxiliar

Abra `cad-prod.html` para preencher os dados de um produto. O formulário gera um objeto JSON pronto para ser copiado e inserido manualmente no array `PRODUCTS` de `loja-data.js`.

O campo de especificações aceita uma entrada por linha no formato:

```text
Processador: Intel Xeon
Memória: 32GB DDR4 ECC
Armazenamento: 1TB NVMe
```

Tags e imagens devem ser separadas por vírgula.

## Dados e integração

Atualmente, `loadProducts()` e `loadCategories()` simulam chamadas assíncronas e retornam as constantes locais de `loja-data.js`. Para conectar uma API real:

1. substitua essas funções por chamadas `fetch()`;
2. mantenha o contrato de dados documentado pelo typedef `Product`;
3. valide respostas, erros HTTP e campos obrigatórios antes da renderização;
4. mova a gestão de estoque, preços e cadastro para o backend;
5. nunca use o painel `cad-prod.html` como área administrativa de produção sem autenticação e autorização no servidor.

O projeto contém referências preparadas para componentes compartilhados em `../src/css` e `../src/js`. Esses arquivos pertencem à estrutura maior do site e precisam estar disponíveis quando a loja for integrada a ela. A página `cad-prod.html` também referencia `admin.css`; esse arquivo deve ser disponibilizado pela integração ou incluído no pacote final.

## Imagens de produtos

Os nomes em `product.images` são convertidos pelo catálogo em arquivos PNG dentro de:

```text
../src/assets/products/
```

Quando uma imagem não existe ou falha ao carregar, o sistema utiliza:

```text
../src/assets/no-image.png
```

Ao adicionar produtos, informe os nomes dos arquivos sem a extensão quando seguir o padrão atual, por exemplo `servidor-dell-r440-1`.

## Segurança e privacidade

- textos dinâmicos do catálogo são escapados ou inseridos com `textContent`;
- IDs de produto são validados antes da consulta local;
- URLs e mensagens do WhatsApp usam codificação apropriada;
- links externos abertos em nova aba usam `rel="noopener noreferrer"`;
- a decisão de cookies é armazenada localmente, sem depender de um cookie para o próprio consentimento;
- o cadastro administrativo é apenas client-side e não fornece controle de acesso;
- antes de publicar, revise os números de WhatsApp, URLs canônicas, páginas de privacidade e termos de serviço.

## Personalização

Para alterar o catálogo, edite `loja-data.js`. Para alterar o comportamento de busca, filtros ou ordenação, edite `loja.js`. A identidade visual da loja está concentrada em `loja.css`, enquanto estilos compartilhados podem vir de `../src/css/template.css`.

## Licença

Este projeto é distribuído sob a **GNU General Public License v3.0**. Consulte o arquivo `LICENSE` para os termos completos.
