# Relevo · Provador Espacial — cena de captura WebXR

Cena WebXR (three.js) para gravar o **concept film** do Relevo: pegar uma camiseta
3D com as mãos no Meta Quest (hand-tracking, em passthrough) e aproximá-la do corpo,
onde ela faz um *cross-dissolve* até ~5% de opacidade — o **match-frame** para a
pós-produção pintar a versão CGI vestida.

> **Enquadramento honesto.** Isto é a parte que **roda de verdade**: exibição e
> manipulação 3D em AR. As etapas de "reconhecimento da tela do celular" e a
> "camiseta vestindo o corpo" são CGI/edição. Nada aqui reconstrói 3D a partir de
> fotos, e não há servidor de pareamento celular↔óculos. Ver [SPEC](#spec--o-que-não-é-isto).

---

## Rodar agora (Meta Quest)

1. **Ligue o hand-tracking** no headset:
   `Configurações → Movimento e controles → Hand tracking` (ou
   `Configurações → Controles`, conforme a versão do sistema). Ative
   "Hand tracking" e, se houver, "Auto switch (controles ↔ mãos)".
2. Abra o **Meta Quest Browser** e vá para a URL publicada:
   **https://coniose.github.io/relevo-provador/**
3. Toque em **"Entrar em AR"**. Aceite a permissão de hand-tracking se for pedida.
   No `immersive-ar` o Quest já entrega **passthrough** (você vê a sala).
4. Faça **pinça** (ponta do indicador + polegar) perto da camisa para pegá-la.
   Solte desfazendo a pinça.
5. **Aproxime do torso**: a camisa some suavemente (cross-dissolve até ~5%).
   Afaste e ela volta.
6. Ao **sair da sessão**, aparece o botão **"Exportar take (JSON)"** no HUD —
   baixa o `take-mao.json` com a trajetória das mãos para a pós.

> Sem `assets/tshirt.glb`, a cena usa um **placeholder** (camiseta-caixa preta).
> Funciona para testar hand-tracking e gravação; troque por um GLB real antes do
> hero shot. Ver `assets/README.md`.

## Preview no PC (sem headset)

Abra a URL no Chrome/Edge desktop: sem XR, a cena cai para **OrbitControls**
(gire o modelo com o mouse). Útil para conferir o asset e a iluminação.

## Vitrine (model-viewer) — desktop / celular / Quest

`vitrine.html` é uma vitrine de loja standalone usando `<model-viewer>` (Google,
cross-browser, com WebXR pra AR). Gira o produto, troca cor/tamanho e tem botão
"Provar no seu espaço" (AR no Quest/celular; degrada com mensagem no desktop).
URL: **https://coniose.github.io/relevo-provador/vitrine.html**

---

## ⚠️ Testar ANTES de agendar a gravação

**Captura do passthrough.** A gravação/cast nativo do Quest pode sair com **fundo
preto** (o passthrough não é capturado, e isso varia por versão do SO). Faça este
teste esta semana:

1. Entre em qualquer experiência AR/passthrough.
2. Grave ~10 s pela captura nativa do Quest.
3. Veja o vídeo: **o fundo real (sua sala) aparece ou está preto?**

- ✅ Aparece → pode gravar o POV direto.
- ❌ Preto → **plano B**: grave a camada virtual (camisa) em fundo preto e componha
  o ambiente/espelho em pós. O `take-mao.json` alinha o CGI ao movimento real das mãos.

---

## Roteiro de gravação (shot a shot)

| # | Shot | Origem | O que o software entrega |
|---|------|--------|--------------------------|
| 1 | POV escrolando a Shein no celular | Câmera real | — (edição) |
| 2 | Colocando o Meta Quest | Câmera real | — (edição) |
| 3 | UI "reconhece a tela" + botão **Projetar**, clique com a mão | **CGI/overlay** | — (não é software; é motion graphics) |
| 4 | Camisa surge em AR; seleciono, seguro e arrasto até o corpo; fica ~95% transparente | **Esta cena WebXR** + CGI da camisa vestida no match-frame | Grab por pinça, cross-dissolve, `take-mao.json` |

O software cobre o **shot 4** inteiro e a manipulação 3D do shot 3. Os shots 1, 2 e a
UI do 3 são captura real + edição — construir o handshake celular↔óculos seria semanas
de trabalho para algo que a câmera não distingue de um overlay bem-feito.

---

## Estrutura

```
relevo-provador/
  index.html                 # cena WebXR (three.js) — shot 4 / captura no Quest
  vitrine.html               # vitrine de loja (model-viewer) p/ desktop, celular e Quest
  assets/
    tshirt.glb               # camiseta (ausente → placeholder)
    README.md
  take-mao.example.json      # exemplo de take exportado
  .github/workflows/pages.yml# deploy automático no push da main
  .nojekyll                  # evita Jekyll em /assets
```

## Deploy

GitHub Actions publica a raiz do repo no GitHub Pages a cada push na `main`
(`.github/workflows/pages.yml`). HTTPS é obrigatório para WebXR — o Pages resolve isso.
URL final: **https://coniose.github.io/relevo-provador/**

## SPEC — o que NÃO é isto

- ❌ Reconstrução 3D a partir de fotos.
- ❌ Servidor de pareamento celular↔óculos / "reconhecimento de tela".
- ❌ Unity, APK, sideload — é página web, roda no navegador do Quest.

Estas fronteiras são deliberadas: o concept film vende a visão em CGI e **prova a
execução** com o que de fato roda nesta cena.
