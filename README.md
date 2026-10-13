# Exército de Clones

**As mentes que você admira trabalhando nos seus projetos, dentro do Claude Code.** Grátis, código aberto (MIT), rodando no seu computador.

Clone aqui não é escrever "aja como o Hormozi". Isso só imita o jeito de falar. O Exército de Clones vasculha o que a pessoa **publicou** (livros, entrevistas, vídeos, posts), monta **como ela pensa** (no que acredita, como decide, o que rejeita, como argumenta) com a fonte de cada ideia, e transforma isso num agente que trabalha com você.

| Skill | O que faz |
|---|---|
| `clonar` | pesquisa a referência, te mostra as fontes pra aprovar, monta a mente com fonte e confiança em cada item, cria o agente e roda um teste de fidelidade |
| `conselho` | coloca 2 a 4 clones no mesmo projeto: todos respondem em paralelo, um critica o outro e você recebe a versão final combinada |

Já vem com um clone de exemplo pronto: **Alex Hormozi** (oferta, preço e geração de lead), em [`exemplos/alex-hormozi`](exemplos/alex-hormozi).

---

## Do que você precisa

- **Claude Code** (vem com o plano Pro ou superior do Claude): [claude.com/claude-code](https://claude.com/claude-code). Funciona no terminal, no app do Claude pra computador (aba Code) e no VS Code.
- Opcional: [`yt-dlp`](https://github.com/yt-dlp/yt-dlp) para o clone ler a legenda de vídeos do YouTube (`pip install yt-dlp`).

Nenhuma API paga: tudo roda com o seu plano do Claude.

## Instalação (2 comandos)

Abra o Claude Code e digite, um de cada vez:

```
/plugin marketplace add mateusffsc/exercito-de-clones
```

```
/plugin install exercito-de-clones@exercito-de-clones
```

Reinicie o Claude Code. Pronto.

<details>
<summary>Prefere copiar os arquivos na mão?</summary>

**Windows (PowerShell):**
```powershell
git clone https://github.com/mateusffsc/exercito-de-clones "$env:TEMP\exercito-de-clones"
New-Item -ItemType Directory -Force "$env:USERPROFILE\.claude\skills" | Out-Null
Copy-Item "$env:TEMP\exercito-de-clones\skills\*" "$env:USERPROFILE\.claude\skills" -Recurse -Force
```

**Mac / Linux:**
```bash
git clone https://github.com/mateusffsc/exercito-de-clones /tmp/exercito-de-clones
mkdir -p ~/.claude/skills && cp -R /tmp/exercito-de-clones/skills/* ~/.claude/skills/
```
</details>

### Ativar o clone de exemplo (Hormozi)

**Windows (PowerShell):**
```powershell
git clone https://github.com/mateusffsc/exercito-de-clones "$env:TEMP\exercito-de-clones"
$ex = "$env:TEMP\exercito-de-clones\exemplos\alex-hormozi"
New-Item -ItemType Directory -Force "$env:USERPROFILE\.claude\agents", "$env:USERPROFILE\.claude\clones\alex-hormozi" | Out-Null
Copy-Item "$ex\clone-alex-hormozi.md" "$env:USERPROFILE\.claude\agents\"
Copy-Item "$ex\mente.md", "$ex\fontes.md" "$env:USERPROFILE\.claude\clones\alex-hormozi\"
```

**Mac / Linux:**
```bash
git clone https://github.com/mateusffsc/exercito-de-clones /tmp/exercito-de-clones
ex=/tmp/exercito-de-clones/exemplos/alex-hormozi
mkdir -p ~/.claude/agents ~/.claude/clones/alex-hormozi
cp $ex/clone-alex-hormozi.md ~/.claude/agents/
cp $ex/mente.md $ex/fontes.md ~/.claude/clones/alex-hormozi/
```

Reinicie o Claude Code.

## Como usar

**Criar um clone:**
```
clona o Gary Halbert pra me ajudar com copy de anúncio
```
Ele pesquisa, te mostra a tabela de fontes, espera o seu OK, monta a mente e cria o agente `clone-gary-halbert`.

**Trabalhar com um clone:**
```
usa o clone-alex-hormozi pra analisar essa oferta: [cola a oferta]
```

**Juntar vários no mesmo projeto:**
```
conselho com o hormozi, o halbert e o ogilvy: reescreve a oferta da minha página de vendas
```
Cada clone responde em paralelo, critica o dos outros, e você recebe a versão final, onde eles concordam e onde brigam.

## Onde fica cada coisa

```
~/.claude/agents/clone-<nome>.md     o agente que o Claude Code chama
~/.claude/clones/<nome>/fontes.md    as fontes aprovadas
~/.claude/clones/<nome>/mente.md     a mente, com fonte e confiança em cada item
~/.claude/clones/<nome>/notas.md     os trechos curtos de cada fonte
```

No Windows, `~` é `C:\Users\SEU_USUARIO`.

## Regras do exército

- **Só gente pública com obra publicada.** Não clona colega, cliente nem ninguém sem material público.
- **O clone é um modelo do que a pessoa publicou, não a pessoa.** Ele avisa isso e nunca finge ser ela.
- **Nada inventado:** citação real vem com fonte; o resto aparece como dedução, com nível de confiança.
- **Sem livro pirata e sem dado privado.** Livro só entra se for seu ou se for material público sobre ele.
- Não use clone pra se passar pela pessoa, publicar frase como se fosse dela ou simular indicação.

## Créditos

Ideias de método (fontes aprovadas antes da leitura, mente com fonte em cada item e teste de fidelidade) inspiradas no [mind-clone](https://github.com/mrgnfndr-dr/mind-clone), de mrgnfndr-dr (MIT).

Feito por [Mateus Ferreira](https://www.instagram.com/mateus.curta.ia/). MIT: pode usar, mudar e compartilhar.
