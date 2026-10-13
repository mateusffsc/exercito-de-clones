---
name: clonar
description: Monta o clone de raciocínio de uma referência pública (empresário, copywriter, autor, criador, investidor) a partir do que ela publicou, com fonte em cada ideia, e salva como agente do Claude Code pronto pra trabalhar com você. Usar quando o usuário pedir "clona o fulano", "cria um clone do X", "quero o Hormozi trabalhando comigo", "monta a mente sintética de…" ou "exército de clones".
---

# Clonar

O clone não é "aja como o Fulano". Isso só imita o jeito de falar. Aqui você reconstrói **como a pessoa pensa**: no que ela acredita, como decide, o que ela rejeita, como argumenta e como escreve. Tudo a partir do que ela **publicou**, com a fonte de cada ideia.

O resultado são 3 arquivos:

| Arquivo | O que é |
|---|---|
| `~/.claude/clones/<slug>/fontes.md` | a lista de fontes aprovada pelo usuário |
| `~/.claude/clones/<slug>/mente.md` | a mente: crenças, frameworks, decisões, rejeições, estilo, cada item com fonte e confiança |
| `~/.claude/agents/clone-<slug>.md` | o agente que o Claude Code chama pra trabalhar |

`<slug>` = nome em minúsculas com hífen (`alex-hormozi`). No Windows, `~` é `C:\Users\SEU_USUARIO`.

## Antes de começar

- **Só pessoa pública com material publicado** (livros, entrevistas, palestras, posts, vídeos). Se o alvo parecer pessoa comum (um colega, um ex, um cliente), pare e explique que a skill não clona gente sem obra pública.
- Pergunte **pra que o clone vai trabalhar** (oferta, copy, conteúdo, estratégia, vendas, finanças…). Isso define onde a pesquisa aprofunda.
- Pergunte se o usuário tem material próprio pra somar: PDF de livro que comprou, anotações, transcrições. Livro só entra se for cópia dele ou material público sobre o livro (resumo oficial, capítulo de amostra, a pessoa falando do livro). Nunca baixe livro pirata.

## Etapa 1 · Varredura

Use `WebSearch` em português e em inglês, com variações do nome, empresa e livros. Procure:
- site oficial, livros e resumos oficiais;
- entrevistas e podcasts (com transcrição ou legenda);
- palestras e vídeos do canal da pessoa;
- artigos, newsletters, threads e posts de autoria dela.

Para vídeo do YouTube, tente a legenda com `yt-dlp --skip-download --write-auto-subs --sub-langs "pt.*,en.*" <url>` se o `yt-dlp` estiver instalado. Sem ele, use a descrição e as matérias sobre o vídeo.

Meta: **15 a 30 fontes de pelo menos 4 tipos diferentes**, priorizando o que a própria pessoa disse ou escreveu (fonte primária) sobre o que falam dela.

## Etapa 2 · Fontes aprovadas

Mostre uma tabela e **espere o OK** antes de ler tudo:

| # | Data | Tipo | Fonte | Do que fala | Link |
|---|---|---|---|---|---|

O usuário pode cortar, trocar ou acrescentar. Salve a lista final em `~/.claude/clones/<slug>/fontes.md`.

## Etapa 3 · Leitura

Leia cada fonte uma vez (`WebFetch`, legenda baixada ou arquivo do usuário) e anote em `~/.claude/clones/<slug>/notas.md`:
- a ideia, em uma linha;
- o trecho curto que prova (até 2 frases, entre aspas, nunca o texto inteiro);
- de onde veio: `[F07]` (número da fonte) e, em vídeo, o minuto.

Para muitas fontes, divida a leitura entre subagentes (5 fontes cada) e junte as notas no fim.

## Etapa 4 · A mente

Monte `~/.claude/clones/<slug>/mente.md` com estes blocos. **Cada item termina com as fontes e a confiança**: `[F03, F11] · A`.
- **A** = aparece em 3 ou mais fontes e ela fala com convicção.
- **M** = aparece pouco ou tem tensão com outra ideia.
- **B** = quase tudo é dedução sua. Marque também `(dedução)`.

1. **Crenças de base:** o que ela dá como verdade e usa pra argumentar.
2. **Frameworks:** as ferramentas de pensar que ela repete, com nome e quando usa cada uma.
3. **Cadeias de raciocínio:** "acredita X → porque Y → então faz Z". Isso é o que deixa o clone responder pergunta que ela nunca respondeu.
4. **Como decide:** o que ela prioriza quando duas coisas boas brigam (velocidade × qualidade, preço × volume…).
5. **Opiniões fortes:** posições concretas, com o porquê.
6. **O que rejeita:** o que ela acha errado e por quê. Isso deixa o clone discordar de você do jeito dela.
7. **Onde é especialista e onde especula:** limita a autoridade do clone.
8. **Jeito de argumentar e de escrever:** números primeiro? Analogia? Contrário do senso comum? Frases curtas? Poucas expressões típicas, curtas, com fonte.
9. **O que mudou com o tempo:** visão antiga (ano) → visão atual (ano). A mais recente vale.

Regras da mente:
- Mais vale uma mente curta e bem provada do que uma longa cheia de achismo. Corte o que você não sustentaria com fonte.
- Contradição real fica registrada como tensão; não alise.
- Nada de história pessoal, memória ou frase que a pessoa não publicou.

## Etapa 5 · O agente

Escreva `~/.claude/agents/clone-<slug>.md` a partir de [modelo-clone.md](modelo-clone.md):
- `description` diz **quando chamar** o clone (ex.: "oferta, preço, geração de lead"), porque é isso que o Claude Code lê pra decidir.
- O corpo traz a mente **resumida** (até ~120 linhas) e aponta pros arquivos completos, que o clone pode abrir pra conferir.
- Mantenha as regras de honestidade do modelo sem mudar.

## Etapa 6 · Teste de fidelidade

1. Escolha 5 posições claras que a pessoa já declarou (em temas diferentes).
2. Para cada uma, pergunte ao clone (via subagente `clone-<slug>`) **sem mostrar a resposta real**.
3. Compare com o que ela disse e marque: **bateu**, **parcial**, **errou** ou **contradiz**.
4. Mostre o placar ("4 bateram, 1 parcial, 0 contradiz") com os casos ruins por inteiro.
5. Contradição = erro na mente. Corrija o item que puxou a resposta errada e teste de novo. Nunca apague a pergunta pra passar no teste.

É um teste rápido, não prova. Diga isso no resultado.

## Etapa 7 · Entrega

Diga ao usuário:
- onde estão os 3 arquivos;
- como chamar: "usa o clone-<slug> pra analisar minha oferta" (o Claude Code também chama sozinho quando o assunto bate com a `description`);
- que ele pode juntar vários clones no mesmo projeto com a skill **conselho**;
- o placar do teste e onde o clone é fraco.

## Regras de honestidade (valem pra todo clone)

- O clone é **um modelo do que a pessoa publicou**, não a pessoa. Ele diz isso quando perguntado e nunca finge ser ela de verdade.
- **Nunca inventa** citação, memória, caso pessoal, número ou fonte. Citação real vem entre aspas com a fonte; o resto é "pelo raciocínio dela, …".
- Sem dado pessoal privado: endereço, contato, vida íntima, vazamento, conteúdo pago que o usuário não tem.
- Não serve pra se passar pela pessoa, publicar frase como se fosse dela nem simular indicação ou parceria.
