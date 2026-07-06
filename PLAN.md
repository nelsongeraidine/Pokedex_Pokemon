# PLAN — Pokédex Pokémon

**Data de Atualização:** 06-07-2026_Versão 1.01

Documento vivo para acompanhar o estado e os próximos passos do projeto. Atualizar conforme o trabalho avança.

## Estado atual

Projeto funcional e completo para o escopo descrito em `PRD.md`: listagem, busca, filtro por tipo e painel de detalhes com stats/habilidades/evolução, tudo em `index.html`, sem build.

## Backlog (não priorizado)

- [ ] Corrigir/remover a função `mergePoke` quebrada em `App` (`index.html`) — hoje é dead code inofensivo, mas confunde leitura.
- [ ] Persistir favoritos/últimos vistos em `localStorage`.
- [ ] Adicionar testes (hoje não há nenhum) — exigiria decidir um runner, já que o projeto não usa Node/build.
- [ ] Avaliar mover o app para um setup com build (Vite, por exemplo) caso o carregamento via Babel-no-navegador vire gargalo de performance.
- [ ] Internacionalizar textos (hoje fixos em pt-BR, com dados de habilidade/descrição vindos em inglês da PokéAPI).
- [ ] Comparação de times / múltiplos Pokémon lado a lado.

## Como este arquivo deve ser usado

- Antes de iniciar uma nova feature ou correção relevante, adicionar um item aqui.
- Ao concluir, marcar como feito ou remover a linha (mantendo o `CLAUDE.md` como fonte de arquitetura, não de tarefas).
- Este arquivo não substitui `PRD.md` (o que o produto é/faz) nem `CLAUDE.md` (como o código é organizado).
