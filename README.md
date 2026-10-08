# Dash Marketing — Ranking de Posts UniCPO

Página estática (um único `index.html`) que gera um **ranking de posts** a partir do
relatório mensal em PDF. Roda 100% no navegador — nada é enviado para servidor.

## Funcionamento

- **Três abas de marca.** O seletor no topo alterna entre **UniCPO**, **FAINTER** e **Clínica UniCPO**; cada uma tem seus próprios meses e dados.
- **Abas por mês.** Cada mês é uma aba. Agosto/2026 já vem carregado como exemplo.
- **Upload de PDF.** Em "＋ Adicionar mês" (ou "↻ Atualizar PDF deste mês") você escolhe
  mês/ano e envia o PDF. O site lê a tabela `Vídeo | Like | Comentário | Repost | Envio |
  Salvamento | Visualizações | Seguidores`, calcula o score e monta o ranking.
  Se a leitura automática falhar, há um campo para colar os dados (TAB, vírgula ou 2+ espaços).
- **Persistência.** Os meses ficam salvos no `localStorage` do navegador. Todo mês é só
  abrir a página e subir o PDF novo.
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
