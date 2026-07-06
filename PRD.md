# PRD — Pokédex Pokémon

**Data de Atualização:** 06-07-2026_Versão 1.01

## Resumo

Aplicação web single-page, single-file, que funciona como uma Pokédex retrô-futurista: lista os 1025 Pokémon (dados via PokéAPI), permite busca, filtro por tipo e exibição de detalhes (stats, habilidades, cadeia de evolução) em um painel lateral.

## Problema / Motivação

Fornecer uma forma rápida e visualmente distinta (tema CRT/retrô) de consultar dados de Pokémon direto no navegador, sem exigir instalação, backend próprio ou build — bastando abrir um arquivo HTML.

## Público-alvo

Fãs de Pokémon e desenvolvedores que queiram uma referência rápida de dados (stats, tipos, evoluções) sem depender de apps de terceiros.

## Escopo atual (implementado)

- **Listagem paginada**: carrega Pokémon em lotes de 20 (`PAGE_SIZE`) até o total de 1025, com botão "Carregar Mais".
- **Busca**: campo de busca com debounce (300ms), aceita nome exato/parcial ou número; mostra dropdown de sugestões (até 8).
- **Filtro por tipo**: barra de botões com os 18 tipos; seleciona um tipo e substitui a listagem pelos Pokémon daquele tipo.
- **Painel de detalhes** (lateral, deslizante): abre ao clicar em um card, com 4 abas:
  - **INFO**: habilidades, altura, peso, experiência base, geração.
  - **STATS**: barras animadas de HP/ATK/DEF/SP.ATK/SP.DEF/SPD + total base.
  - **SKILLS**: descrição detalhada de cada habilidade (carregada sob demanda).
  - **EVOLUÇÃO**: cadeia de evolução visual, incluindo ramificações (ex. Eevee), navegável (clicar em um estágio abre seus detalhes).
- **Estados de carregamento/erro**: skeletons animados durante carregamento; mensagens de erro com botão de retry em falhas de rede.
- **Responsividade**: grid adapta colunas em telas ≤600px (2 colunas) e 601–900px (3 colunas); painel de detalhes ocupa tela cheia em mobile.
- **Acessibilidade básica**: `aria-label`, `role="dialog"`, fechamento via tecla Esc, foco no botão de fechar ao abrir o painel.

## Fora de escopo (não implementado)

- Persistência local (favoritos, histórico) — cache é apenas em memória e se perde ao recarregar a página.
- Autenticação/contas de usuário.
- Times/comparação de múltiplos Pokémon.
- Internacionalização (a UI é fixa em português; textos de habilidade/descrição vêm em inglês da PokéAPI).
- Testes automatizados.
- Build/bundling — o app roda via CDN + Babel standalone no navegador.

## Dependências externas

- **PokéAPI** (`https://pokeapi.co/api/v2`) — dados de espécies, tipos, habilidades, cadeias de evolução.
- **PokeAPI/sprites** (GitHub raw) — sprites e artwork oficial.
- **React 18 / ReactDOM / Babel Standalone** via unpkg CDN.
- **Google Fonts** (Share Tech Mono, Orbitron).

Todas essas dependências exigem conexão com a internet; o app não funciona offline.

## Riscos / limitações conhecidas

- Sem build step, todo o app é transpilado no navegador a cada carregamento — impacto de performance perceptível em conexões/dispositivos mais lentos.
- Busca por substring faz fallback para buscar a lista completa de 1025 Pokémon quando o nome não é exato.
- Bug conhecido: função `mergePoke` em `App` está com uma implementação quebrada (não é chamada atualmente, então sem impacto prático — ver `CLAUDE.md`).
