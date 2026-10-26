# Documentação do Projeto: Dez Mil Dias — A Vida de Miyamoto Musashi

Bem-vindo à documentação oficial do design e da arquitetura técnica de **“Dez Mil Dias: A Vida de Miyamoto Musashi”**, um protótipo jogável em 2D desenvolvido em **Godot Engine 4** para a Prova de Aptidão Profissional (PAP) do Curso Profissional de Técnico de Gestão e Programação de Sistemas Informáticos (ESBN).

---

## 📚 Índice da Documentação

Os documentos estão organizados de forma modular na pasta `docs/`:

1. **[01. Visão Geral e Âmbito do Projeto](01_visao_geral_e_escopo.md)**
   - Tema histórico de Miyamoto Musashi (1584–1645).
   - Problema, solução proposta e elementos diferenciadores.
   - Âmbito do protótipo (Vertical Slice do Capítulo 1: juventude dos 13 aos 16 anos).

2. **[02. Design Visual e Estilo Artístico](02_design_visual_e_arte.md)**
   - Estilo Pixel Art feudal japonês inspirado em *First Cut: Samurai Duel* e *Katana ZERO*.
   - Proporções corporais (semi-realistas de 5 a 6 cabeças, ~35px de altura real).
   - Paleta de cores, iluminação dinâmica (`CanvasModulate`) e efeitos de clima.
   - Arte tradicional *Sumi-e* (tinta da China) para interfaces e Códex.

3. **[03. Sistema de Câmara e Abordagem Híbrida](03_sistema_de_camera_hibrido.md)**
   - Exploração em **Top-Down 3/4** (aldeia, santuários, tarefas e NPCs).
   - Duelos em **Vista Lateral 2D (Side-View)** (tensão 1v1, leitura de katana e física).
   - Transição cinematográfica entre os dois modos.

4. **[04. Mecânicas de Combate e Duelos](04_mecanicas_de_combate.md)**
   - Combate baseado em timing, postura e letalidade em 1 a 2 golpes.
   - Duelo 1: Arima Kihei (aos 13 anos em Hirafuku).
   - Duelo 2: Akiyama (aos 16 anos na província vizinha).
   - Sistema de *Parry*, combos, esquivas (*dash*) e opções de impacto e física.

5. **[05. Narrativa, NPCs, Cutscenes e Códex Histórico](05_narrativa_npcs_e_codex.md)**
   - Sistema de interação com NPCs (`Area2D` e balão `[E]`).
   - Caixa de diálogo estilo *Visual Novel* com retratos de personagens.
   - Estrutura de dados em ficheiros `JSON` (`dialogos.json` e `codex.json`).
   - Cutscenes *In-Engine* com `AnimationPlayer` e Cutscenes estilo pergaminho.
   - Códex Histórico tripartido: Documentado, Lenda e Ficção do Jogo.

6. **[06. Arquitetura Técnica em Godot 4](06_arquitetura_godot4.md)**
   - Organização de pastas (`scenes/`, `scripts/`, `assets/`, `data/`).
   - Máquina de Estados Finita (`StateMachine`) para controlo de estados do jogador e inimigos.
   - Nó Global (`GameManager` / *Autoload*) para persistência de dados.

7. **[07. Guia Técnico de Assets e Sprites](07_guia_de_assets.md)**
   - Mapeamento de todos os ficheiros descarregados em `assets/sprites/`.
   - Dimensões de grelhas, números de frames e compensação de *pivot* nos pés.
