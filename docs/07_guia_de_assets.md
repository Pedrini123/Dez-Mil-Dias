# 07. Guia Técnico de Assets e Sprites

Este documento serve como mapa de referência para a configuração de todas as *sprite sheets* no Godot 4 (definindo o número de frames horizontais e a resolução de cada animação).

---

## 1. Miyamoto Musashi (Protagonista — Side-View)
* **Caminho da Pasta:** `res://assets/sprites/musashi/`
* **Altura Padrão do Canvas:** 96 píxeis
* **Altura Real da Personagem:** ~34 píxeis
* **Ponto de Ancoragem (*Offset / Pivot*):** Centrado na base dos pés (`Bottom-Center`).

| Ficheiro PNG | Resolução Total | Frames (`Hframes`) | Dimensão de Cada Frame | Descrição da Animação |
| :--- | :--- | :--- | :--- | :--- |
| `idle.png` | 480 x 96 | 5 | 96 x 96 | Respiração e postura de guarda inicial |
| `run.png` | 768 x 96 | 8 | 96 x 96 | Corrida com katana embainhada/segura |
| `jump.png` | 288 x 96 | 3 | 96 x 96 | Salto e queda |
| `attack_1.png` | 480 x 96 | 5 | 96 x 96 | Corte frontal rápido (*Slash 1*) |
| `attack_2.png` | 480 x 96 | 5 | 96 x 96 | Segundo corte do combo |
| `attack_3.png` | 480 x 96 | 5 | 96 x 96 | Estocada final com passo em frente |
| `air_attack.png` | 576 x 96 | 6 | 96 x 96 | Corte aéreo em arco descendente |
| `defend.png` | 576 x 96 | 6 | 96 x 96 | Postura de bloqueio e absorção de impacto |
| `dash.png` | 768 x 96 | 8 | 96 x 96 | Esquiva rápida para trás ou para os lados |
| `hurt.png` | 384 x 96 | 4 | 96 x 96 | Reação física a golpe sofrido |
| `death.png` | 960 x 96 | 10 | 96 x 96 | Queda no chão e colapso |
| `special_attack.png`| 1344 x 96 | 14 | 96 x 96 | Golpe especial de desembaínhar rápido (*Iaijutsu*) |

---

## 2. Arima Kihei (Rival do Duelo 1 — Side-View)
* **Caminho da Pasta:** `res://assets/sprites/arima_kihei/`
* **Altura Padrão do Canvas:** 44 píxeis
* **Altura Real da Personagem:** ~35 píxeis

| Ficheiro PNG | Resolução Total | Frames (`Hframes`) | Dimensão de Cada Frame | Descrição |
| :--- | :--- | :--- | :--- | :--- |
| `idle.png` | 500 x 44 | 5 | 100 x 44 | Guarda baixa e paciente |
| `run.png` | 700 x 44 | 7 | 100 x 44 | Avanço rápido em direção ao jogador |
| `jump.png` | 300 x 44 | 3 | 100 x 44 | Salto |
| `attack_1.png` | 500 x 44 | 5 | 100 x 44 | Ataque rápido com lança/espada |
| `attack_2.png` | 500 x 44 | 5 | 100 x 44 | Segundo golpe consecutivo |
| `attack_3.png` | 1000 x 44 | 10 | 100 x 44 | Corte profundo de longo alcance |
| `dash_attack.png` | 1100 x 44 | 11 | 100 x 44 | Investida rápida pelo ecrã |
| `defend.png` | 600 x 44 | 6 | 100 x 44 | Guarda e parry |
| `dash.png` | 800 x 44 | 8 | 100 x 44 | Esquiva |
| `hurt.png` | 300 x 44 | 3 | 100 x 44 | Dano sofrido |
| `death.png` | 1000 x 44 | 10 | 100 x 44 | Queda e derrota |

---

## 3. Akiyama (Rival do Duelo 2 — Side-View)
* **Caminho da Pasta:** `res://assets/sprites/akiyama/`
* **Altura Padrão do Canvas:** 84 píxeis
* **Altura Real da Personagem:** ~34 píxeis

| Ficheiro PNG | Resolução Total | Frames (`Hframes`) | Dimensão de Cada Frame | Descrição |
| :--- | :--- | :--- | :--- | :--- |
| `idle.png` | 424 x 84 | 4 | 106 x 84 | Postura alta imponente |
| `run.png` | 848 x 84 | 8 | 106 x 84 | Movimento de pés ágil |
| `basic_attack.png`| 530 x 84 | 5 | 106 x 84 | Corte diagonal limpo |
| `strong_attack.png`| 954 x 84 | 9 | 106 x 84 | Golpe pesado de duas mãos |
| `hurt.png` | 318 x 84 | 3 | 106 x 84 | Reação a impacto |
| `death.png` | 1060 x 84 | 10 | 106 x 84 | Queda de joelhos |

---

## 4. Cenários Feudais (Backgrounds e Camadas Parallax)
* **Caminho da Pasta:** `res://assets/sprites/cenarios/`
* **Resolução Padrão de Todos os Ficheiros:** **353 x 180 píxeis**

| Ficheiro | Descrição e Utilização |
| :--- | :--- |
| `sky.png` | Fundo de céu estático (primeira camada do `ParallaxBackground`). |
| `clouds.png` | Nuvens lentas em deslocamento contínuo. |
| `fuji.png` | Silhueta do Monte Fuji à distância. |
| `mountain_back.png`, `mountain_middle.png`, `mountain_front.png` | Camadas de relevo com efeito de profundidade. |
| `trees.png` e `background_trees.png` | Florestas e árvores de bambu/sakura. |
| `shrine_single.png` e `shrine_multiple.png` | Santuários xintoístas e portões *Torii* para a arena de duelo. |
| `house.png` | Casas tradicionais de madeira para a aldeia. |
| `ground.png` e `grass.png` | Superfície transitável com colisores para o combate. |

---

## 5. NPCs (Aldeões e Figurantes)
* **Caminho da Pasta:** `res://assets/sprites/npcs/`
* `npc.png`: Ilustração isolada de camponês (29 x 28 píxeis).
* `npc_spritesheet.png`: Conjunto com 16 variações de animação (464 x 28 píxeis, 16 frames de 29 x 28 píxeis).
