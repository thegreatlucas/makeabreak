# Make a Break Studio ☕

Plataforma web para gerar edições da **Make a Break**, a newsletter semanal da Make, do zero até o HTML pronto para envio no RD Station — com curadoria de notícias e redação automática seguindo o Guia Editorial oficial.

> A Make a Break não replica notícias. Ela **traduz relevância**.

## O que a plataforma faz

O fluxo completo em 5 etapas:

| Etapa | O que acontece |
|---|---|
| **1 · Configuração** | Chave da OpenAI, modelos, número/ano da edição, merge tag do RD Station e tipo de edição |
| **2 · Coleta** | Busca notícias em feeds RSS das fontes recomendadas, no Google Notícias (grátis) e com GPT web search |
| **3 · Curadoria** | Você escolhe o que entra, define a editoria de cada notícia e marca a matéria principal (⭐) de cada bloco |
| **4 · Geração & Edição** | O GPT recebe o Guia Editorial + notícias selecionadas e escreve a edição inteira no tom da Make; tudo editável campo a campo |
| **5 · Preview & Export** | Preview fiel do e-mail, download/cópia do HTML pronto para colar no RD Station |

## Fontes de notícias (em ordem de custo)

1. **Feeds RSS** (grátis) — Meio & Mensagem, B9, Exame, TechCrunch, The Verge, Olhar Digital, Wired, G1, BBC Brasil, Rolling Stone e outros, filtrados pelos últimos 8 dias.
2. **Google Notícias** (grátis, sem chave) — tópicos de Tecnologia/Ciência para o Destaque e buscas específicas por editoria, últimos 7 dias.
3. **GPT web search** (usa tokens) — busca **apenas as editorias que ainda têm menos de 8 notícias**, em chamadas paralelas. Se tudo estiver abastecido, não gasta nada.

Também dá para adicionar notícias manualmente.

## Tipos de edição

Baseados no histórico real da news:

- **📰 Padrão (semanal)** — banner preto + amarelo, highlights, Destaque, Updates, Redes Sociais, News e Plans com tags ciano.
- **🎬 Especial temática** — como a #44 (Barbieheimer): a edição inteira respira um tema, com cor própria, saudação nomeando os leitores e trocadilhos temáticos em todos os blocos.
- **🎂 Aniversário / comemorativa** — como a #48 e a #100: a news fala em primeira pessoa celebrando o marco, com faixa festiva e clima de festa.
- **🎗️ Campanha do mês** — como a #09 (Outubro Rosa): edição normal + box dedicado à causa, na cor da campanha.

## Estrutura da edição gerada

Assunto trocadilhado (com merge tag de primeiro nome), preheader, highlights do banner, abertura com saudação criativa, Destaque principal e as quatro editorias — cada uma com título "espertinho" em caixa alta, matéria principal e bullets com emoji e link. As seções fixas seguem o padrão da news: *"O que mais você precisa saber hoje:"*, *"E pra ficar por dentro das redes sociais:"*, *"Tem mais News por aqui:"* e *"E pra edificar ainda mais o seu fds:"*.

Cada bloco aceita uma **imagem de abertura** (banner + uma por editoria). O GPT sugere o termo de busca da imagem, com atalhos para Google Imagens e Unsplash. Para o envio real, hospede as imagens na biblioteca do RD Station e cole as URLs.

## Como publicar (GitHub Pages)

1. Suba o `index.html` na raiz do repositório.
2. Em **Settings → Pages**, selecione a branch `main` como source.
3. Acesse `https://seuusuario.github.io/nome-do-repo/`.

Não precisa de servidor: é um arquivo único de HTML/CSS/JS.

## Chave da API e privacidade

A chave da OpenAI fica salva **somente no localStorage do seu navegador**. As chamadas vão direto do navegador para a API da OpenAI — nenhum dado passa por servidores intermediários (exceto os proxies públicos de CORS usados apenas para ler os feeds RSS).

Modelos recomendados: `gpt-4.1` para escrita e `gpt-4o-mini` para busca (mais rápido e barato). Modelos de raciocínio (gpt-5/o1/o3) são suportados com esforço reduzido na busca.

## Guia Editorial (resumo embutido no prompt)

Tom leve, conversacional, inteligente e bem-humorado. Pode: trocadilhos, referências pop, frases de efeito. Não pode: corporativês, clickbait, sensacionalismo, ironia agressiva. Assuntos proibidos: política partidária, tragédias, crimes, guerra, conteúdo adulto, fake news e fofoca. Toda notícia precisa responder: *por que isso importa? o que muda? o que isso revela de tendência?*
