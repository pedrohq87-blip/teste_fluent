# Fluent · Plataforma (versão web)

Protótipo navegável da plataforma de inglês da Fluent: apresentação, experiência do aluno (ciclo Start, Lições 1 a 4) e prévia do painel do professor.

## Como publicar
Site estático, sem build. No Vercel: **Add New → Project → importar este repositório → Deploy** (Framework: *Other*, sem comando de build).

## Estrutura
- `index.html`: o código do site (HTML, CSS e JavaScript), sem conteúdo de lição
- `conteudo/start/`: a trilha e uma ficha JSON por lição (exercícios, cartões, conversa com o coach). Formato em `conteudo/LEIA-ME.md`
- `media/start/licao-NN/`: vídeos, áudios, ilustração e PDF de cada lição
- `media/comum/`: avatares do Teacher Pedro e arquivos compartilhados

## Observações
- O microfone usa o reconhecimento de voz do navegador (Chrome, Edge, Android e Safari no iPhone). Precisa de https, que o Vercel já fornece.
- O progresso do aluno fica salvo no navegador (localStorage). Para alunos reais e o painel do professor com dados de verdade, o próximo passo é um banco de dados (por exemplo, Supabase).
