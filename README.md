# Sintonia Aberta — Rádios Online do Brasil e do Mundo

Plataforma web **100% gratuita e sem backend** para sintonizar milhares de rádios FM, AM e web rádios do Brasil e do mundo ao vivo, construída em um único arquivo `index.html` com HTML, CSS e JavaScript puro (com suporte opcional de build estático via Vite para publicação no Netlify ou GitHub Pages).

---

## Principais Funcionalidades

- **Mais de 4.000 rádios do Brasil e do mundo:** Agregação automática de múltiplas fontes gratuitas com fallback silencioso e remoção de duplicadas (`nome + URL`).
- **Catálogo nacional garantido:** 31 grandes emissoras brasileiras pré-configuradas com carregamento instantâneo e URLs de contingência.
- **Filtros completos:**
  - Todos os **27 estados brasileiros** (`AC` a `TO`) + Distrito Federal.
  - **16+ categorias musicais e temáticas:** Gospel, Sertanejo, Notícias, Rock, Pop, Esporte, Forró, Pagode, Funk, MPB, Eletrônica, Samba, Brega, Católica, Evangélica e Internacional.
  - Filtro por **país** (Brasil, Portugal, EUA, Argentina, Espanha, Reino Unido, França, Itália, Japão, Uruguai e Paraguai).
  - Barra de pesquisa em tempo real por nome, cidade, estado ou frequência (ex.: `101.7`).
- **Abas de navegação:** `Todas`, `Top 100 Mais Ouvidas`, `Favoritas` e `Recentes` (salvas localmente no `localStorage`).
- **Player fixo contínuo com recuperação automática:**
  - Suporte nativo e via **HLS.js** para streams `.m3u8`, além de resolução automática de playlists `.pls` e `.m3u`.
  - Tentativa automática entre `url_resolved`, `url`, mirrors alternativos e próxima emissora da mesma fonte em caso de falha ou timeout.
  - Controle de volume, play/pause, anterior/próxima, favoritar, compartilhamento direto no **WhatsApp** e integração com Media Session API.
- **Card de Informações e Sinopse da Rádio:** Ao clicar em **Ouvir**, exibe um card com sinopse contextual da emissora, ficha técnica (localização, dial, gêneros, codec/bitrate, site oficial) e busca assíncrona na Wikipédia.
- **História do Rádio:** Acervo com linha do tempo da radiodifusão brasileira (1922–hoje) e pesquisa livre de história de qualquer emissora via Wikipédia.
- **Capas de rádios e álbuns de fontes livres:** Carregamento sob demanda (`IntersectionObserver`) combinando favicons do Radio Browser, iTunes Podcast Search, Wikipédia/Wikimedia Commons, DuckDuckGo Icons e capa de música via iTunes Search / MusicBrainz Cover Art Archive.
- **Design responsivo estilo Spotify (tema escuro):** Adaptado para desktop e celular com menu lateral retrátil.
- **Suporte opcional a Google AdSense e AdMob:** Slots ocultos por padrão para não prejudicar a experiência do usuário até que seus IDs reais sejam configurados.

---

## Fontes de Dados e APIs Gratuitas Utilizadas

Nenhuma chave paga ou servidor próprio é necessário:

| Finalidade | Fontes / APIs |
| --- | --- |
| Emissoras e streams | Radio Browser (`de1`, `de2`, `nl1`, `all.api.radio-browser.info`), CuteRadio, Icecast Directory (`yp.xml`), Radio Garden |
| Fallback de listas públicas | Repositórios GitHub (`AlonDrilich/radio-playlists`, `junguler/m3u-radio-music-playlists`, `iptv-org`, `radios-brasil.json`) |
| Capas das rádios | Radio Browser `favicon`, iTunes Podcast Search API, Wikipédia PT / Wikimedia Commons, DuckDuckGo Icons |
| Capas de músicas | iTunes Search API e MusicBrainz / Cover Art Archive |
| Sinopse e história | Wikipédia PT/EN (MediaWiki API com `origin=*`) + acervo local integrado |

---

## Estrutura do Projeto

```text
.
├── index.html          # Aplicação completa (HTML, CSS e JS puro)
├── netlify.toml        # Configuração de build e headers para publicação no Netlify
├── package.json        # Scripts Vite para desenvolvimento e build em dist/
├── public/
│   └── ads.txt         # Modelo de arquivo ads.txt para validação do Google AdSense
└── README.md           # Documentação do projeto
```

---

## Como Executar Localmente

Você pode abrir o arquivo `index.html` diretamente em um servidor estático local ou usar os scripts do projeto com Node.js:

```bash
# 1. Instalar dependências (necessário apenas para o servidor Vite/build)
npm install

# 2. Iniciar servidor de desenvolvimento (porta 3000)
npm run dev

# 3. Gerar build de produção na pasta dist/
npm run build
```

---

## Publicação no Netlify (via GitHub)

O repositório já inclui `netlify.toml` configurado:

1. Envie este projeto para um repositório no **GitHub**.
2. No painel do **Netlify**, selecione **Add new site → Import an existing project** e conecte seu repositório.
3. Confirme as configurações de build (lidas automaticamente do `netlify.toml`):
   - **Build command:** `npm run build`
   - **Publish directory:** `dist`
4. Clique em **Deploy site**.

---

## Configuração Opcional de Anúncios (AdSense / AdMob)

Os blocos de anúncios permanecem totalmente ocultos enquanto não estiverem configurados:

1. No arquivo `index.html`, localize o objeto `AD_CONFIG` dentro da tag `<script>` e preencha seus IDs reais (`adsense.clientId`, `inFeedSlotId`, `sidebarSlotId` ou `admob`).
2. Altere `enabled: true` em `AD_CONFIG`.
3. Caso utilize Google AdSense na web, substitua o identificador de editor no arquivo `public/ads.txt` e na meta tag `google-adsense-account` comentada no `<head>` do `index.html`.
4. Se também utilizar Shoutcast Directory com DevID gratuito, informe a chave na constante `SHOUTCAST_DEV_ID` no `index.html`.

---

## Licença e Direitos

Os links de áudio, nomes comerciais e logotipos pertencem às suas respectivas emissoras e são exibidos a partir de diretórios públicos abertos.
