# Dash Marketing — Ranking de Posts UniCPO

Página estática (um único `index.html`) que gera um **ranking de posts** a partir do
relatório mensal em PDF. O cálculo roda no navegador; os dados publicados vêm do `dados.json`.

## Funcionamento

- **Três abas de marca.** O seletor no topo alterna entre **UniCPO**, **FAINTER** e **Clínica UniCPO**; cada uma tem seus próprios meses e dados.
- **Abas por mês.** Cada mês é uma aba. Agosto/2026 já vem carregado como exemplo.
- **Upload de PDF.** Em "＋ Adicionar mês" (ou "↻ Atualizar PDF deste mês") você escolhe
  mês/ano e envia o PDF. O site lê a tabela `Vídeo | Like | Comentário | Repost | Envio |
  Salvamento | Visualizações | Seguidores`, calcula o score e monta o ranking.
  Se a leitura automática falhar, há um campo para colar os dados (TAB, vírgula ou 2+ espaços).
- **Dados compartilhados.** Os meses publicados ficam no arquivo `dados.json` do repositório e
  aparecem para **qualquer pessoa** que abrir o link. Meses subidos pelo navegador ficam só ali
  (etiqueta "local") até serem publicados: clique em **Exportar dados** e substitua o `dados.json`
  no GitHub (ou peça para publicarem).
- **Top 3 com player e análise.** Os 3 primeiros do mês aparecem em linhas, com o vídeo tocando na página
  (Instagram, YouTube ou TikTok) ao lado dos números e de uma análise em texto ("Por que está no pódio").
- **Coluna "Link" no PDF.** Se o relatório trouxer a coluna Link (texto ou link clicável), o site lê o
  endereço de cada post e o vídeo do Top 3 já aparece sozinho. Também dá para colar/trocar o link no card.
- **Gráficos** simples: nota final Top 10, quem mais trouxe seguidores, quem mais gerou engajamento
  e mix de interações.
- **Exportar CSV** do ranking do mês.

## Metodologia do score (0–100)

Em cada sub-critério o melhor post do mês leva a pontuação cheia; os demais entram
normalizados (mín–máx).

| Bloco | Peso | Componentes |
|---|---|---|
| Seguidores | 50% | `ln(1 + seguidores)` — escala log |
| Engajamento total | 50% | `ln(1 + engajamento ponderado)` — escala log |

As **visualizações não entram no cálculo** (são impulsionadas por tráfego pago).

Pesos de engajamento: **Like = 1**, **Comentário = 2**, **Repost / Envio / Salvamento = 3**.

## Publicar no GitHub Pages

```bash
cd "<pasta do projeto>"
git init
git add index.html README.md
git commit -m "Ranking de Posts UniCPO"
git branch -M main
git remote add origin https://github.com/unicpobauru/Dash_Marketing.git
git push -u origin main
```

Depois, no repositório: **Settings → Pages → Branch: `main` / `/root` → Save**.
O site fica em `https://unicpobauru.github.io/Dash_Marketing/`.
