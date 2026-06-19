# Make a Break Studio ☕

Plataforma web para gerar edições da **Make a Break**, a newsletter semanal da Make, do zero até o HTML pronto para envio no RD Station — com curadoria de notícias e redação automática seguindo o Guia Editorial oficial.

> A Make a Break não replica notícias. Ela **traduz relevância**.

## O que a plataforma faz

O fluxo completo:

| Etapa | O que acontece |
|---|---|
| **📊 Dashboard** | Notícias em alta de cada editoria (10+ por bloco). Dê 👍/👎 em cada uma para a news aprender que tipo de conteúdo você quer em cada editoria (aprendizado salvo no Supabase) |
| **1 · Configuração** | Chave da OpenAI, modelos, número/ano da edição, merge tag do RD Station, tipo de edição e credenciais do Supabase |
| **2 · Coleta** | Busca notícias em feeds RSS das fontes recomendadas, no Google Notícias (grátis) e com GPT web search |
| **3 · Curadoria** | Você escolhe o que entra (meta de 7 por editoria), marca até 2 destaques (⭐) por editoria e dá 👍/👎. No 👎, a news troca por outra; dá pra trazer candidatos 1 a 1 (aceita/recusa), ordenar por relevância/data e filtrar. O título tem botões **Acessar** e **Editar**. Não há mais editoria "Destaque": o destaque do topo é escolhido entre as estrelas |
| **4 · Geração & Edição** | O GPT recebe o Guia Editorial + notícias selecionadas e escreve a edição inteira no tom da Make; tudo editável campo a campo. Até 2 matérias por editoria, cada uma com link da fonte. Cada bloco tem botão **Regenerar** com campo "o que corrigir" e galeria de sugestões de imagem para escolher. Dá para ligar/desligar seções |
| **5 · Preview & Export** | Preview fiel do e-mail, download/cópia do HTML pronto para colar no RD Station |

## Fontes de notícias (em ordem de custo)

1. **Feeds RSS** (grátis) — **somente fontes brasileiras** (conteúdo em português), pouco inclinadas politicamente. Ligados por padrão: Meio & Mensagem, B9, Adnews, Rock Content, Tecnoblog, Canaltech, Olhar Digital, TecMundo, Exame, Superinteressante, G1 (Ciência, Tecnologia e Pop & Arte), Hypeness e Rolling Stone Brasil. Outros BR como opção (Mobile Time, Meio Bit, Startupi, Jovem Nerd, Cinepop, POPline, IGN Brasil, Omelete). **Apenas os últimos 5 dias** e **10 a 20 notícias por editoria** (mínimo com top-up automático; o máximo mantém as de maior afinidade pelos joinhas). **Nada em inglês**: feeds internacionais foram removidos, a busca via GPT exige resposta em português e qualquer notícia em inglês é **traduzida automaticamente**. Filtros automáticos removem **promoção/ofertas**, **política** (exceto quando é sobre redes sociais) e **notícias repetidas de fontes diferentes**.
2. **Google Notícias** (grátis, sem chave) — buscas por editoria em pt-BR, últimos 5 dias.
3. **GPT web search** (usa tokens) — busca **apenas as editorias que ainda não fecharam em 7 selecionadas**, em chamadas paralelas. Se tudo estiver abastecido, não gasta nada.

Também dá para adicionar notícias manualmente.

## Tipos de edição

Baseados no histórico real da news:

- **📰 Padrão (semanal)** — banner preto + amarelo, highlights, Destaque, Updates, Redes Sociais, News e Plans com tags ciano.
- **🎬 Especial temática** — como a #44 (Barbieheimer): a edição inteira respira um tema, com cor própria, saudação nomeando os leitores e trocadilhos temáticos em todos os blocos.
- **🎂 Aniversário / comemorativa** — como a #48 e a #100: a news fala em primeira pessoa celebrando o marco, com faixa festiva e clima de festa.
- **🎗️ Campanha do mês** — como a #09 (Outubro Rosa): edição normal + box dedicado à causa, na cor da campanha.

## Estrutura da edição gerada

Assunto trocadilhado (com merge tag de primeiro nome), preheader, highlights do banner, abertura com saudação criativa, Destaque principal e as quatro editorias — cada uma com título "espertinho" em caixa alta, matéria principal e bullets com emoji e link. As seções fixas seguem o padrão da news: *"O que mais você precisa saber hoje:"*, *"E pra ficar por dentro das redes sociais:"*, *"Tem mais News por aqui:"* e *"E pra edificar ainda mais o seu fds:"*.

Cada bloco aceita uma **imagem de abertura** (banner + uma por editoria). O GPT sugere o termo de busca e o app abre uma **galeria de sugestões de imagem (Openverse, grátis)**: você clica na que mais combina e ela vai pro HTML. Também há atalhos para Google Imagens e Unsplash. Para o envio real, hospede as imagens na biblioteca do RD Station e cole as URLs.

O **pre-header** é fixo no padrão `Ano X - Edição #XXX - A Newsletter da Make`. As matérias saem com **três parágrafos de até 5 linhas**, e o prompt proíbe travessões, a fórmula "não é X, é Y" e clichês típicos de IA.

## Identidade visual (Make ID)

A interface do Studio segue a identidade da **Make ID**: tema claro, tipografia **Uni Sans** (fonte oficial, **self-hosted** em `fonts/*.woff2`, pesos 400/500/600/700/800) e ícones de linha **Lucide** (estilo próximo ao SF Symbols da Apple) no lugar de emojis em toda a interface. O **e-mail/preview** e os bullets da newsletter mantêm os emojis e o visual preto + amarelo de propósito, porque são o conteúdo/identidade do próprio e-mail.

Paleta (extraída da auditoria da Make ID), em variáveis CSS: navy `#070D42`, vermelho coral `#EA3428` (claro `#EB6057`), fundo claro. Elementos de marca aplicados: cabeçalho navy com a logo e o sinal de `+`, barras verticais coral nos títulos, rótulos navy e estados ativos em coral.

## Como publicar (GitHub Pages)

1. Suba o `index.html` na raiz do repositório.
2. Em **Settings → Pages**, selecione a branch `main` como source.
3. Acesse `https://seuusuario.github.io/nome-do-repo/`.

Não precisa de servidor: é um arquivo único de HTML/CSS/JS.

## Chave da API e privacidade

A chave da OpenAI fica salva **somente no localStorage do seu navegador**. As chamadas vão direto do navegador para a API da OpenAI — nenhum dado passa por servidores intermediários (exceto os proxies públicos de CORS usados apenas para ler os feeds RSS).

Modelos recomendados: `gpt-4.1` para escrita e `gpt-4o-mini` para busca (mais rápido e barato). Modelos de raciocínio (gpt-5/o1/o3) são suportados com esforço reduzido na busca.

## Inteligência (Supabase)

Os votos 👍/👎 do Dashboard e da Curadoria ficam guardados no **Supabase**, então o aprendizado de preferências por editoria é compartilhado entre dispositivos e pessoas da equipe. A `anon key` fica embutida no app (é pública por design e protegida por RLS) e pode ser sobrescrita na aba **Configuração**. Sem credenciais, o app cai automaticamente no `localStorage` (aprendizado só naquele navegador).

Para criar a tabela, rode no **SQL Editor** do Supabase:

```sql
create table if not exists public.feedback (
  id         uuid primary key default gen_random_uuid(),
  created_at timestamptz not null default now(),
  item_key   text,
  editoria   text not null,
  vote       smallint not null check (vote in (-1, 1)),
  titulo     text not null,
  fonte      text,
  link       text,
  resumo     text,
  keywords   text[] default '{}',
  context    text default 'curadoria'
);
create index if not exists feedback_editoria_idx on public.feedback (editoria);
create index if not exists feedback_created_idx  on public.feedback (created_at desc);
alter table public.feedback enable row level security;
create policy "anon read feedback"  on public.feedback for select to anon using (true);
create policy "anon write feedback" on public.feedback for insert to anon with check (true);
```

Como funciona: cada voto extrai as palavras-chave do título e soma (+1/−1) um peso por editoria. As notícias são reordenadas por afinidade no Dashboard e na Curadoria, e itens com 👎 não voltam a aparecer.

### Cache do Dashboard

O Dashboard guarda as notícias em alta numa segunda tabela (`news_cache`), no estilo de um portal (foto, chamada e trecho do texto). Ele lê do cache na hora de abrir (rápido) e **se atualiza sozinho a cada 6 horas** puxando dos feeds — também dá para forçar pelo botão. Rode no SQL Editor:

```sql
create table if not exists public.news_cache (
  item_key   text primary key,
  editoria   text not null,
  titulo     text not null,
  fonte      text,
  link       text,
  resumo     text,
  imagem     text,
  data       timestamptz,
  updated_at timestamptz not null default now(),
  created_at timestamptz not null default now()
);
create index if not exists news_cache_editoria_idx on public.news_cache (editoria);
create index if not exists news_cache_data_idx     on public.news_cache (data desc);
alter table public.news_cache enable row level security;
create policy "anon read news"   on public.news_cache for select to anon using (true);
create policy "anon insert news" on public.news_cache for insert to anon with check (true);
create policy "anon update news" on public.news_cache for update to anon using (true) with check (true);
```

> Auto-refresh é client-side: enquanto a página estiver aberta, ele checa a cada 30 min e repõe quando o cache passa de 6h; ao abrir o Dashboard, mostra o cache na hora e atualiza se estiver velho. Não há servidor/cron próprio (o site é estático no GitHub Pages).

### Rascunho da coleta

A coleta de notícias e os flags de seleção (selecionada, estrela, editoria, capa) são salvos numa terceira tabela (`coleta`), por edição, para **recuperar ao recarregar** a página e permitir **trabalho simultâneo**. Salva automático (debounce) e usa soft-delete (`removed`) para não apagar itens de quem está junto. Rode no SQL Editor:

```sql
create table if not exists public.coleta (
  edicao     text not null,
  item_key   text not null,
  titulo text, fonte text, link text, resumo text, imagem text, data timestamptz,
  editoria text, sel boolean default false, star boolean default false,
  vote smallint default 0, principal boolean default false, capa boolean default false,
  removed boolean default false,
  updated_at timestamptz not null default now(),
  primary key (edicao, item_key)
);
alter table public.coleta enable row level security;
create policy "anon read coleta"   on public.coleta for select to anon using (true);
create policy "anon insert coleta" on public.coleta for insert to anon with check (true);
create policy "anon update coleta" on public.coleta for update to anon using (true) with check (true);
```

## Guia Editorial (resumo embutido no prompt)

Tom leve, conversacional, inteligente e bem-humorado. Pode: trocadilhos, referências pop, frases de efeito. Não pode: corporativês, clickbait, sensacionalismo, ironia agressiva. Assuntos proibidos: política partidária, tragédias, crimes, guerra, conteúdo adulto, fake news e fofoca. Toda notícia precisa responder: *por que isso importa? o que muda? o que isso revela de tendência?*
