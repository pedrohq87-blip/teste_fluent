# Conteúdo das lições

Cada lição publicada tem **uma ficha JSON** com tudo o que o site precisa. O código do site não guarda conteúdo de lição: ele lê estas fichas ao abrir. Na migração para o banco de dados (Supabase), cada ficha vira um registro, sem conversão.

```
conteudo/start/trilha.json        unidades e títulos das 36 lições + quais já estão publicadas
conteudo/start/licao-NN.json      ficha de cada lição publicada
media/start/licao-NN/             arquivos da lição
media/comum/                      avatares do Teacher Pedro e arquivos usados em várias lições
```

## Publicar uma lição nova

1. Colocar os arquivos em `media/start/licao-NN/` com os nomes padrão abaixo.
2. Criar `conteudo/start/licao-NN.json` (copiar a ficha anterior como modelo).
3. Acrescentar o número em `publicadas` no `trilha.json`.

## Nomes padrão dos arquivos

| Arquivo | O que é |
|---|---|
| `card.png` | ilustração da lição na trilha |
| `video.mp4` / `video.jpg` | videoaula (vertical, crf 27) e capa |
| `vocabulario.mp4` / `vocabulario.jpg` | vídeo de vocabulário e capa |
| `material.pdf` | material de apoio |
| `palavras/w01.mp3`… | áudio de cada palavra dos cartões |
| `coach/A1.mp3`… | falas da conversa com o coach (o nome é o código da fala) |
| `exercicios/<quem>_<o-que>.mp3` | áudios dos exercícios de ouvir |

## Ficha da lição

- `title`, `short`, `img`, `pdf`: título, resumo, ilustração e PDF.
- `steps`: etapas da lição (videoaula, vocabulário, exercícios, conversa).
- `ex`: os 7 exercícios (`choice`, `order`, `listen`).
- `decks`: cartões de vocabulário (`en`, `pr`, `ipa`, `pt`, `audio`, `cat`).
- `coach`: a conversa.
  - `lines`: texto de cada fala, pelo código (G01 abertura, A1… perguntas, P1… elogios, C1… correções, M1… "Repita comigo", F1 fim, R1 "pode repetir?").
  - `stages`: as 6 etapas. Cada uma tem a pergunta (`ask`), o cartão da pessoa (`card`, opcional), o modelo de resposta (`tpl`), as opções de toque (`chips`, com `{nome}` para o nome do aluno) e a correção (`check`).

### Como funciona a correção (`check`)

A resposta do aluno é normalizada (minúsculas, sem pontuação, com espaço no começo e no fim). As regras são testadas em ordem e **a primeira que bate decide**: `"ok"` (acertou) ou o código da correção que o coach fala. Se nenhuma bater, vale `fallback` (`null` = "pode repetir?").

Condições de uma regra (todas precisam valer):

- `if`: expressão regular, ou lista de expressões que precisam aparecer todas;
- `unless`: expressão que **não** pode aparecer;
- `minWords` / `maxWords`: tamanho da resposta;
- `anyOf`: `{ "list": [...], "min": 3 }`, ao menos N expressões da lista;
- `count`: `{ "re": "...", "min": 2 }`, a expressão aparece ao menos N vezes.

Exemplo (Lição 3, "How about you?"):

```json
{ "rules": [
    { "go": "ok", "if": [" (good|great|fine) ", " (how about you|and you) "] },
    { "go": "C3", "if": " (good|great|fine) " } ],
  "fallback": null }
```
