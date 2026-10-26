# 04. Mecânicas de Combate e Duelos

## 1. Filosofia de Combate
Ao contrário de jogos de fantasia ou *hack and slash* onde os inimigos recebem dezenas de golpes antes de cair, o combate de *Dez Mil Dias* é inspirado no realismo das fontes históricas de Musashi (*Go Rin no Sho*):
* **Letalidade Alta:** 1 a 2 golpes bem assentes decidem a vitória ou a derrota.
* **Tensão e Distância (*Maai*):** O posicionamento e o respeito pelo alcance da espada do adversário são cruciais.
* **Timing e Postura:** O ataque não pode ser executado às cegas; um ataque falhado deixa o espadachim vulnerável a um contra-ataque imediato.

---

## 2. Ações do Jogador no Duelo

| Ação | Tecla / Comando | Descrição Mecânica |
| :--- | :--- | :--- |
| **Movimento** | `A` / `D` ou `Setas` | Passos laterais firmes para medir o alcance (*maai*). |
| **Ataque Rápido** | `Botão Esquerdo` ou `J` | Corte frontal rápido com a ponta da lâmina. Dano moderado, recuperação rápida. |
| **Ataque Forte** | `K` ou `Botão Central` | Golpe descendente com grande peso e alcance. Quebra defesas simples, mas deixa o jogador exposto se falhar. |
| **Defesa / Parry** | `Botão Direito` ou `L` | Postura de guarda com a lâmina. Se pressionada no instante exato do golpe inimigo (janela de 0.15s), executa um **Parry Perfeito**, desequilibrando o oponente. |
| **Esquiva (*Dash*)** | `Shift` ou `Espaço` | Passo rápido para trás ou desvio lateral, evitando o corte adversário. |

---

## 3. Os Duelos Históricos do Capítulo 1

### Duelo 1: Arima Kihei (Aos 13 anos — 1596)
* **Local:** Pátio do Santuário de Hirafuku.
* **Contexto Histórico:** Kihei era um guerreiro experiente da escola de artes marciais *Shintō-ryū*, que afixou uma tábua desafiando qualquer habitante local. Musashi, ainda adolescente (chamado Bennosuke), aceitou o desafio.
* **Comportamento da IA de Kihei:**
  - Mantém a distância com uma postura defensiva rígida.
  - Utiliza uma investida com corte em corrida (*dash attack*).
  - Padrão: 2 cortes rápidos seguidos de uma pausa de recuperação, momento em que o jogador deve contra-atacar.

### Duelo 2: Akiyama (Aos 16 anos — 1599)
* **Local:** Limite da Província de Tajima.
* **Contexto Histórico:** O segundo duelo registado na obra de Musashi. Akiyama era um mestre de espada formidável.
* **Comportamento da IA de Akiyama:**
  - Muito mais agressivo e paciente no bloqueio.
  - Utiliza fintas (*feints*) para fazer o jogador gastar a esquiva antes de desferir um corte pesado (*strong attack*).
  - Exige domínio do tempo de *parry* para abrir a sua guarda.

---

## 4. Máquina de Estados do Combate (FSM em GDScript)
O lutador opera com base numa Máquina de Estados Finita para prevenir bugs e sobreposição de animações:

```
                  ┌──────────────┐
                  │     IDLE     │
                  └──────┬───────┘
                         │
        ┌────────────────┼────────────────┐
        ▼                ▼                ▼
  ┌───────────┐    ┌───────────┐    ┌───────────┐
  │  WALKING  │    │ ATTACKING │    │ DEFENDING │
  └───────────┘    └─────┬─────┘    └─────┬─────┘
                         │                │ (timing perfeito)
                         │                ▼
                         │          ┌───────────┐
                         │          │   PARRY   │
                         │          └───────────┘
                         ▼
                  ┌──────────────┐
                  │  HIT / HURT  │
                  └──────┬───────┘
                         ▼
                  ┌──────────────┐
                  │    DEATH     │
                  └──────────────┘
```

---

## 5. Feedback Visual e Auditivo (Game Feel)
* **Hit-Stop:** Quando uma espada conecta, o jogo congela por 6 a 8 frames (0.1s), dando peso físico e sensação de choque de lâminas.
* **Screen Shake:** Tremor breve e suave da câmara em impactos fortes.
* **Áudio:** Som metálico cortante e seco (*clash*) em bloqueios bem-sucedidos; silêncio e som de rasgão de tecido/lâmina em golpes fatais.
