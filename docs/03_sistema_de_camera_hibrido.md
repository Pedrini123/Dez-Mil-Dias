# 03. Sistema de Câmara e Abordagem Híbrida

## 1. Por que a Abordagem Híbrida?
Nos jogos tradicionais de samurai, existe um conflito constante de *design*:
* Se o jogo for puramente em **Vista Lateral (Side-View)**, a exploração de vilas, caminhos e casas torna-se linear (apenas andar para a esquerda ou direita).
* Se o jogo for puramente em **Top-Down (Vista de Cima)**, os duelos de espada perdem impacto cinematográfico e exigem desenhar golpes e cortes em 8 direções diferentes.

A **Abordagem Híbrida** resolve os dois problemas com elegância e eleva significativamente o nível técnico do projeto na PAP.

---

## 2. Visão Comparativa dos Dois Modos

```
                          ┌───────────────────────────┐
                          │     ESTRUTURA HÍBRIDA     │
                          └─────────────┬─────────────┘
                                        │
           ┌────────────────────────────┴───────────────────────────┐
           ▼                                                         ▼
┌─────────────────────────────────────┐   ┌─────────────────────────────────────┐
│      MODO EXPLORAÇÃO (Top-Down)     │   │        MODO DUELO (Side-View)       │
├─────────────────────────────────────┤   ├─────────────────────────────────────┤
│ • Câmara a 45º sobre a aldeia.      │   │ • Câmara lateral na altura dos olhos.│
│ • Movimento livre em 8 direções.    │   │ • Movimento horizontal (esquerda/dir)│
│ • Interação com NPCs e objetos.     │   │ • Foco total nas posturas da katana. │
│ • Realização de tarefas e pistas.   │   │ • Bloqueios (*parry*), esquiva, corte│
│ • Desbloqueio do Códex Histórico.   │   │ • Duelo 1v1 tenso e letal.          │
└─────────────────────────────────────┘   └─────────────────────────────────────┘
```

---

## 3. Modo 1: Exploração da Aldeia (Top-Down 3/4)
* **Objetivo:** Sentir a vida quotidiana do Japão do final do século XVI e preparar o duelo.
* **Mecânicas Ativas:**
  - Movimentação suave com as teclas `W`, `A`, `S`, `D` ou setas.
  - Colisões com casas, pontes de madeira, cercas e árvores.
  - Aproximação de NPCs (com nó `Area2D`): quando o jogador se aproxima, surge um indicador visual `[E] Falar`.
  - Investigação de pontos de interesse (ex: aviso de duelo no poste de madeira do templo).
* **Vantagem de Animação:** O Musashi precisa apenas de animações simples de caminhada (4 direções) e interação, sem necessidade de ataques complexos nesta vista.

---

## 4. Modo 2: Duelos Históricos (Vista Lateral 2D)
* **Objetivo:** Viver o confronto decisivo e a tensão do corte único.
* **Mecânicas Ativas:**
  - Controlos de duelo: Ataque rápido, ataque forte, defesa/parry (`Botão Direito` ou `K`), esquiva lateral (`Shift` ou `Espaço`).
  - Câmara Dinâmica (`Camera2D`):
    - Inicia afastada, enquadrando os dois espadachins.
    - Faz zoom suave quando a distância entre os adversários diminui (*tensão de proximidade*).
    - Pequeno congelamento dramático de 0.1s (*hit stop*) e tremor de câmara (*screen shake*) quando a katana atinge o alvo.

---

## 5. A Transição Cinematográfica entre Modos
A passagem do Modo de Exploração para o Modo de Duelo ocorre quando o jogador ativa um evento histórico:

1. **Gatilho:** Musashi arranca o desafio do poste ou entra no círculo do pátio do templo.
2. **Ecrã de Corte (*Screen Slash*):**
   - Faixas pretas de cinema surgem no topo e na base do ecrã.
   - O ecrã é cortado por um traço preto de tinta da China (*Sumi-e*).
   - Surge o texto histórico com o nome e a escola do oponente:  
     *“1596 — Duelo no Santuário de Hirafuku: Arima Kihei (Escola Shintō-ryū)”*.
3. **Carregamento da Cena:** O Godot troca da cena da aldeia (`village.tscn`) para a arena lateral do duelo (`duel_arima.tscn`).
4. **Regresso pós-duelo:** Concluído o duelo, o ecrã volta à exploração, o estado da história avança e a nova entrada é arquivada no Códex.
