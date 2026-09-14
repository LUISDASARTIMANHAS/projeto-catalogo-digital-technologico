# Instruções para agentes

## Escopo do projeto

- Este é um catálogo web estático em JavaScript vanilla, HTML semântico e CSS, com Bootstrap 5 e Bootstrap Icons carregados por CDN.
- Não há processo de build, gerenciador de dependências ou testes automatizados neste diretório.
- Consulte [README.md](README.md) para requisitos, execução local, rotas, modelo de dados e integração futura.

## Arquitetura e arquivos principais

- `index.html` e `loja.js`: catálogo, busca, filtros, ordenação, paginação e links de atendimento.
- `produto.html` e `produto.js`: detalhes do produto; a entrada é `produto.html?id=...`.
- `loja-data.js`: fontes globais `CATEGORIES`, `BRANDS` e `PRODUCTS`; preserve o contrato `Product` documentado no código.
- `cad-prod.html` e `cad-prod.js`: gerador client-side de JSON para cadastro manual; não é uma área administrativa autenticada.
- `cookie-consent.js`: consentimento armazenado em `localStorage`.
- `loja.css`: estilos específicos do catálogo e da página de produto.

A ordem dos scripts é relevante: carregue os dados antes das funções que os consomem. Preserve a compatibilidade com scripts clássicos e estado global; não converta para módulos ES sem atualizar todas as páginas dependentes.

## Convenções de implementação

- Mantenha HTML semântico, responsivo e acessível: associe rótulos aos campos, preserve foco e teclado, use `alt` significativo e não dependa apenas de cor.
- Use Bootstrap para componentes e layout quando já houver um equivalente; concentre customizações visuais em `loja.css`.
- Preserve a separação atual entre HTML, JavaScript e CSS. Evite introduzir framework ou dependência de build para mudanças pontuais.
- Adicione JSDoc com `@param` e `@return` às novas funções quando aplicável, seguindo o padrão existente.
- Prefira `textContent`, validação de entrada e codificação de URL. Ao usar `innerHTML`, escape qualquer dado controlado pelo usuário antes da interpolação.
- Valide IDs e campos de produto antes de renderizar. Não trate dados do formulário como confiáveis.
- Use `rel="noopener noreferrer"` em links externos com `target="_blank"`.
- Não coloque credenciais, autorização ou lógica administrativa real no front-end.
- Preserve as páginas e links de privacidade, termos e consentimento de cookies ao alterar a interface.

## Dados e recursos

- Produtos são inseridos manualmente em `loja-data.js`; o formulário de `cad-prod.html` apenas gera JSON para cópia.
- Imagens seguem os caminhos `../src/assets/products/` e `../src/assets/no-image.png` quando a loja estiver integrada ao site maior.
- Referências a `../src/`, `admin.css`, páginas legais e recursos externos podem depender da integração principal e devem ser verificadas antes de serem consideradas disponíveis.
- Links de WhatsApp, URLs canônicas e dados de contato devem ser conferidos antes de publicar.

## Validação

- Para testar no ambiente local, use um servidor HTTP, por exemplo `py -m http.server 5500`, e valide `index.html`, `produto.html?id=1001` e `cad-prod.html` no navegador.
- Depois de alterações em JavaScript, verifique o console do navegador, busca/filtros, navegação para detalhes, fallback de imagem, consentimento e links externos afetados.
- Como não há suíte automatizada, informe explicitamente quais verificações manuais foram executadas.
- Não altere `LICENSE` nem faça mudanças não relacionadas ao pedido.
