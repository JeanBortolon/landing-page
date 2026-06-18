# Landing Page — README

Resumo rápido

Pequeno projeto de landing page estática. Arquivos principais estão em `index.html` e a pasta `assets/` contém estilos e imagens.

Estrutura de arquivos

- `index.html` — Página principal (HTML). Contém seções: home, intro, grid-one, gallery, grid-two, pricing, contact e footer. Também implementa um menu lateral controlado por um `input[type=checkbox]` com id `close-menu`.

- `assets/variables.css` — Variáveis CSS (cores, fontes, espaçamentos) usadas pelos outros estilos.
- `assets/classes.css` — Estilos utilitários e classes reutilizáveis (por exemplo containers, helpers).
- `assets/elements.css` — Reset/base para elementos HTML (h1, p, a, buttons etc.).
- `assets/menu.css` — Estilos específicos do menu (aside, label do checkbox, comportamento responsivo do menu lateral).
- `assets/styles.css` — Estilos principais da página (layout das seções, grids, responsividade, imagens etc.).

- `assets/javascript-not-optimized.svg`, `assets/main-bg.svg` — SVGs usados no layout.
- `assets/images/` — Imagens da galeria (`img1.png`, `img2.png`, `img3.png`).

O que cada arquivo contém e onde editar

- `index.html`:
  - Estrutura do conteúdo (texto e seções). Alterar títulos, textos e links âncora aqui.
  - Menu mobile: existe um `input#close-menu` com um `label` que abre/fecha o menu. Atualmente há handlers inline no `h1` e `ul` que chamam `document.getElementById('close-menu').checked = false;` para fechar o menu ao navegar.

- `assets/*.css`:
  - `variables.css`: primeiro lugar a editar para alterar cores, fontes e espaçamentos globais.
  - `classes.css`: adicione utilitários reutilizáveis (margens, display helpers).
  - `elements.css`: padronize tipografia e estilos base.
  - `menu.css`: se precisa ajustar o comportamento do menu em diferentes larguras, edite este arquivo.
  - `styles.css`: regras de layout, grids e ajustes finais.

Boas práticas e dicas rápidas

- Evite handlers inline. Recomenda-se adicionar um pequeno script JS para fechar o menu quando qualquer link do `nav` for clicado. Exemplo (colocar antes do `</body>` ou num arquivo JS):

```js
document.querySelectorAll('nav a').forEach(a =>
  a.addEventListener('click', () => {
    document.getElementById('close-menu').checked = false;
  })
);
```

- Para alterar variáveis de estilo (cores, tipografia), edite `assets/variables.css` — isso facilita temas e manutenção.

- Teste em diferentes larguras (desktop/tablet/telefone) e use as ferramentas do navegador (DevTools) para checar breakpoints e comportamento do menu.

Como testar localmente

- Abra `index.html` no navegador (duplo clique no arquivo ou via servidor local).
- Navegue pelos links âncora para verificar o fechamento do menu em dispositivos pequenos.

Detalhes dos estilos CSS (explicação aprofundada)

- `assets/variables.css`:
  - Objetivo: centralizar cores, fontes, espaçamentos, sombras e breakpoints para fácil manutenção.
  - O arquivo normalmente declara variáveis em `:root` como `--color-primary`, `--spacing-unit`, `--container-max-width`, `--bp-md`.
  - Uso prático: altere `--color-primary` para trocar a cor principal do site sem tocar em outras regras.
  - Exemplo de variável e uso:

    :root { --color-primary: #0b6cf7; --spacing-unit: 1rem; }

    .btn { background: var(--color-primary); padding: calc(var(--spacing-unit) * 0.75); }

- `assets/classes.css`:
  - Contém utilitários e padrões reutilizáveis para layout e espaçamento (ex.: `.main-content`, `.white-bg`, `.grid`, `.form-group`).
  - Recomenda-se usar classes utilitárias para manter regras isoladas e reduzir duplicação.
  - Exemplo: `.main-content` costuma limitar largura com `max-width: var(--container-max-width); margin: 0 auto; padding: 0 1rem;`.

- `assets/elements.css`:
  - Normalização e base tipográfica: define estilos de `h1`..`h6`, `p`, `a`, `button`, listas e campos de formulário.
  - Configure `font-family`, `font-size` base e `line-height` aqui para consistência.

- `assets/menu.css`:
  - Implementa padrão checkbox-toggle: o `input#close-menu` controla `aside.menu` através de seletores CSS (por exemplo, `#close-menu:checked ~ aside.menu { transform: translateX(0); }`).
  - `label[for="close-menu"]` funciona como botão (hamburger/fechar). Em telas pequenas o menu geralmente fica overlay com `position: fixed; inset: 0;`.
  - Ajuste breakpoint para alterar comportamento entre mobile e desktop, p.ex.:

    @media (min-width: 768px) {
      aside.menu { position: static; transform: none; }
    }

  - Acessibilidade: adicione `aria-expanded` dinamicamente via JS se usar mais comportamento interativo.

- `assets/styles.css`:
  - Contém regras de layout das seções (`.section`), grids e responsividade da galeria e dos artigos.
  - Boas práticas: usar `display: grid` com `gap` e `grid-template-columns` ajustados em media queries para controlar colunas.
  - Exemplo prático de grid responsivo:

    .grid { display: grid; grid-template-columns: 1fr; gap: calc(var(--spacing-unit)); }
    @media (min-width: 768px) { .grid { grid-template-columns: repeat(3, 1fr); } }

  - Use `max-width` e `margin: 0 auto` para centralizar conteúdo e `box-sizing: border-box` globalmente para previsibilidade.

Técnicas e recomendações práticas

- Mobile-first: escreva regras base voltadas para mobile e expanda com `@media (min-width: ...)` para telas maiores.
- Separação de responsabilidades: variáveis em `variables.css`, resets/tipografia em `elements.css`, utilitários em `classes.css`, componentes (menu) em `menu.css` e layout em `styles.css`.
- A técnica checkbox-toggle evita JS, mas pode precisar de pequenos scripts para melhorar acessibilidade (ex.: atualizar `aria-expanded` ou fechar o menu ao clicar em links).
- Teste com teclado e leitores de tela; adicione `aria-label`, roles e `:focus` visíveis para links e botões.
- Documente mudanças: ao alterar variáveis ou breakpoints, adicione um comentário no topo do arquivo modificado com a data e o motivo.

Exemplo de pequeno script (recomendado) para fechar o menu ao clicar em qualquer link do nav — adicione antes de `</body>` ou num arquivo JS separado:

```js
document.querySelectorAll('nav a').forEach(a =>
  a.addEventListener('click', () => {
    const checkbox = document.getElementById('close-menu');
    if (checkbox) checkbox.checked = false;
  })
);
```



