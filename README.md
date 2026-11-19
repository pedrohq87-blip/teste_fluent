# Fluent · Plataforma (versão web)

Protótipo navegável da plataforma de inglês da Fluent: apresentação, experiência do aluno (ciclo Start, Lições 1 e 2) e prévia do painel do professor.

## Como publicar
Site estático, sem build. No Vercel: **Add New → Project → importar este repositório → Deploy** (Framework: *Other*, sem comando de build).

## Estrutura
- `index.html` — a aplicação inteira (HTML, CSS e JavaScript)
- `vocab.json` — vocabulário das lições e falas da conversa da Lição 2
- `media/` — vídeos, áudios e imagens

## Observações
- O microfone usa o reconhecimento de voz do navegador (Chrome, Edge, Android e Safari no iPhone). Precisa de https, que o Vercel já fornece.
- O progresso do aluno fica salvo no navegador (localStorage). Para alunos reais e o painel do professor com dados de verdade, o próximo passo é um banco de dados (por exemplo, Supabase).
