# 06. Arquitetura Técnica em Godot Engine 4

## 1. Estrutura de Diretórios do Projeto
A raiz do repositório está organizada de forma modular e limpa para facilitar o desenvolvimento e a inspeção por parte do júri da PAP:

```
C:\Dez Mil Dias PAP\
├── .git/                      # Controlo de versões Git
├── assets/                    # Recursos visuais e sonoros
│   ├── sprites/               # Sprite sheets 2D
│   │   ├── musashi/           # Todas as animações do protagonista (Side-View)
│   │   ├── arima_kihei/       # Animações do rival 1
│   │   ├── akiyama/           # Animações do rival 2
│   │   ├── cenarios/          # Casas, templos, árvores, chão e céus
│   │   ├── npcs/              # Sprites para aldeões
│   │   └── topdown/           # Sprites e tiles para a exploração de cima
│   ├── ui/                    # Retratos, molduras, fontes e ícones
│   └── audio/                 # Efeitos sonoros de katanas, passos e música
├── data/                      # Ficheiros JSON de dados
│   ├── dialogos.json          # Textos de todas as conversas e NPCs
│   └── codex.json             # Entradas e classificações do Códex
├── docs/                      # Documentação técnica e design (ficheiros .md)
├── scenes/                    # Cenas do Godot (.tscn)
│   ├── core/                  # GameManager, UI/HUD, Transições
│   ├── exploration/           # Aldeia e zonas Top-Down
│   ├── duels/                 # Arenas de duelo 1v1 em Side-View
│   └── characters/            # Nós reutilizáveis de personagens (Player, NPC, Inimigo)
├── scripts/                   # Ficheiros de código GDScript (.gd)
│   ├── autoload/              # Scripts globais (Singletons)
│   ├── combat/                # Lógica de espada, dano, parry e colisores
│   ├── exploration/           # Movimento Top-Down e interações
│   └── ui/                    # Controlo de caixas de texto e Códex
├── Logo/                      # Logótipos do projeto
├── Relatorio PAP e Anteprojeto/ # Documentação escolar da PAP
├── .gitignore                 # Regras para ficheiros temporários do Office e sistema
└── README.md                  # Apresentação principal do repositório
```

---

## 2. Padrões de Programação em GDScript

### A. Autoloads / Singletons (Gestão de Estado Global)
Criamos um script global acessível em qualquer cena do jogo:
* `GameManager.gd`:
  - Guarda a cena atual (`exploration` ou `duel`).
  - Guarda a posição do Musashi no mapa da aldeia para que ele regresse ao local certo após o duelo.
  - Guarda o estado das missões e os diálogos já lidos.
* `CodexManager.gd`:
  - Carrega as entradas de `data/codex.json`.
  - Método `unlock_entry(id: String)` para desbloquear entradas no Códex e emitir sinais para a interface.

---

## 3. Gestão de Cenas e Transições
A transição entre a aldeia (*Top-Down*) e os duelos (*Side-View*) é feita com um nó dedicado `SceneTransition.tscn`:

```gdscript
# Exemplo de transição elegante em GDScript
func change_mode(new_scene_path: String) -> void:
    # 1. Toca animação de corte de espada / fade
    await $AnimationPlayer.play("sword_slash")
    # 2. Muda a cena no motor
    get_tree().change_scene_to_file(new_scene_path)
    # 3. Revela a nova cena
    $AnimationPlayer.play_backwards("sword_slash")
```

---

## 4. O Sistema de Colisões nos Duelos
Para os duelos 1v1 com espada em vista lateral:
* **HurtBox (`Area2D`):** Zona do corpo do espadachim suscetível a receber dano.
* **HitBox (`Area2D`):** Zona da lâmina da katana que gera dano, ativada apenas nos frames exatos do corte pelo nó `AnimationPlayer`.
* **ParryBox (`Area2D`):** Zona frontal ativada durante a guarda. Se a `HitBox` inimiga colidir primeiro com a `ParryBox`, o ataque é anulado, geram-se faíscas e o atacante entra em estado de desequilíbrio (*stagger*).
