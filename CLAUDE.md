# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

**Data de Atualização:** 06-07-2026_Versão 1.01

## Visão geral

Pokédex retrô-futurista single-file: HTML + CSS + React (via CDN/Babel standalone) em um único `index.html`, consumindo a PokéAPI. Sem build, sem package manager, sem testes.

## Arquitetura em uma página

Tudo vive em `index.html`, na ordem:
1. `<style>` — tema CRT (variáveis CSS, animações, classes de componente).
2. Constantes — cores por tipo, labels/cores de stats, config de API (`BASE_URL`, `PAGE_SIZE=20`, `TOTAL=1025`).
3. `api` + `cache` (Map em memória) — wrappers sobre a PokéAPI.
4. Componentes: `TypeBadge`, `StatBar`, `EvolutionChainView` (+ helpers), `DetailPanel` (abas INFO/STATS/SKILLS/EVOLUÇÃO), `PokemonCard`/`CardSkeleton`.
5. `App` — estado central. Três modos mutuamente exclusivos alimentam `pokeMap` (id → Pokémon): lista paginada (`items`), filtro por tipo (`typeItems`), busca debounced (`suggestions`). `displayItems` escolhe o modo ativo por prioridade: tipo > busca > lista.

Bug conhecido: `mergePoke` em `App` é dead code quebrado (nunca é chamado).

## Escopo do projeto

Ver @PRD.md para o que está implementado e o que está fora de escopo. Qualquer feature pedida que conflite com o PRD deve ser sinalizada antes de implementar (ver regra 5).

## Regras de comportamento

1. Antes de qualquer mudança não-trivial (que toque mais de um arquivo ou mude comportamento existente), proponha um plano antes de executar.
2. Nunca adicione bibliotecas externas, CDNs ou pacotes sem consultar antes. O projeto é vanilla por design.
3. Comentários em português. Comentários explicam o "porquê" do código, não o "o quê".
4. Antes de criar arquivo novo além de `CLAUDE.md`/`PRD.md`/`PLAN.md`/`index.html`, justifique por que ele precisa existir.
5. Se a feature pedida conflitar com @PRD.md, avise antes de implementar.
6. Toda atualização do projeto deve ficar documentada com data e versão (`DD-MM-YYYY_Versão X.XX`) em `CLAUDE.md`, `PRD.md` e `PLAN.md`.

## Convenções de código

- Componentes React: PascalCase (`PokemonCard`). Hooks/funções auxiliares: camelCase (`useDebounce`, `extractId`).
- Constantes globais (mapas de tipo/stats, config): UPPER_SNAKE_CASE.
- Estilo via objetos `style` inline no JSX; classes CSS só para o que precisa de `:hover`, animação ou pseudo-elemento.
- Strings de UI em português (pt-BR); dados vindos da PokéAPI (nomes, descrições) permanecem como a API retorna.

## Como rodar

Abrir `index.html` direto no navegador, ou servir a pasta (necessário se o navegador bloquear fetch em `file://`):

    npx serve .

React, ReactDOM e Babel Standalone vêm via CDN (unpkg); o JSX é transpilado no navegador a cada carregamento.
