# assets/

Coloque aqui o modelo da camiseta:

```
assets/tshirt.glb
```

## Requisitos do GLB

- Camiseta preta básica.
- **Centralizada na origem** (0,0,0).
- Escala aproximada **1.0** (≈ tamanho real de uma camiseta, ~0,5 m de largura).
- Materiais com `transparent: true` (o cross-dissolve depende disso — o `index.html`
  já força isso ao carregar, mas exportar já transparente evita surpresas).

## Onde conseguir (licença livre / CC)

- **Poly Pizza** — https://poly.pizza (busque "t-shirt", "shirt")
- **Quaternius** — https://quaternius.com (packs CC0)
- **Sketchfab** — filtre por *Downloadable* + licença *CC* e baixe em glTF/GLB

## Sem asset?

Se `tshirt.glb` não existir, o `index.html` cai para um **placeholder**
(uma camiseta-caixa preta), então a cena continua rodável para teste de
hand-tracking e gravação. O placeholder não serve para o hero shot final —
troque por um GLB de verdade antes da gravação de produto.
