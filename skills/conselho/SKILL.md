---
name: conselho
description: Coloca vários clones do Exército de Clones trabalhando juntos no mesmo projeto ou pergunta, em paralelo, com crítica cruzada e uma versão final combinada. Usar quando o usuário pedir "junta os clones", "conselho", "mesa redonda", "o que o Hormozi e o Ogilvy achariam disso", "coloca os clones pra trabalhar nesse projeto" ou citar 2 ou mais clones na mesma tarefa.
---

# Conselho

Um clone sozinho já ajuda. O pulo do gato é **vários clones no mesmo projeto**: um monta, outro ataca, outro reescreve, e você fica com o que sobreviveu.

## Etapa 1 · Quem está no conselho

- Liste os clones prontos: arquivos `~/.claude/agents/clone-*.md`.
- Se o usuário citar alguém que ainda não tem clone, ofereça rodar a skill **clonar** antes. Não improvise um clone sem fontes.
- Sugira 2 a 4 clones que **pensam diferente** sobre o tema. Clones parecidos só concordam.

## Etapa 2 · O briefing

Os clones não veem esta conversa. Escreva tudo num arquivo `conselho/<AAAA-MM-DD>-<tema>/briefing.md` na pasta atual:
- **Tarefa:** o que precisa sair no fim (uma oferta, um título, uma decisão, um plano).
- **Contexto:** negócio, público, números, o que já foi tentado.
- **Material:** cole o texto, a copy, a planilha ou o link que está em análise.
- **Critério:** como saber se ficou bom.

Mostre o briefing em 5 linhas e confirme antes de chamar os clones.

## Etapa 3 · Escolha o modo

| Modo | Quando | Como roda |
|---|---|---|
| **Mesa redonda** (padrão) | decisão, estratégia, "o que vocês acham" | todos recebem a mesma pergunta e respondem em paralelo |
| **Linha de produção** | algo pra entregar (oferta, página, roteiro) | papéis em sequência: um **cria**, outro **ataca**, outro **refaz** |

## Etapa 4 · Rodada 1

Chame cada clone com a ferramenta de agente (`subagent_type: clone-<slug>`), **todos na mesma mensagem** para rodarem em paralelo. Cada um recebe:
- o caminho do `briefing.md` (e o conteúdo dele);
- o papel, se for linha de produção;
- o pedido: "Responda no seu raciocínio. Até 250 palavras. Termine com: sua recomendação em 1 frase."

Salve cada resposta em `conselho/<…>/r1-<slug>.md`.

## Etapa 5 · Rodada 2 · Crítica cruzada

Mande para cada clone as respostas dos **outros** e peça:
- onde discorda e por quê (no raciocínio dele);
- o que aproveitaria da resposta do outro;
- a recomendação final revisada, em 1 frase.

Salve em `conselho/<…>/r2-<slug>.md`. Pule esta rodada só se o usuário pedir pressa.

## Etapa 6 · Síntese (você, não um clone)

Entregue ao usuário, nesta ordem:
1. **A versão final**: a oferta, o título ou a decisão pronta, juntando o melhor de cada um.
2. **Onde concordam.**
3. **Onde brigam**: cada lado em 1 linha, no raciocínio de quem defende.
4. **O que é dedução**: marque o que nenhum clone sustentou com fonte.
5. **Próximo passo**: o que testar primeiro.

Salve tudo em `conselho/<…>/sintese.md`.

## Regras

- Os clones são modelos do que cada pessoa publicou, não as pessoas. Não apresente a síntese como opinião real delas.
- Nunca publique fala de clone como frase da pessoa.
- Se dois clones concordarem em tudo, diga isso e sugira um terceiro que pense diferente.
