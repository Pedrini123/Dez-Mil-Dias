# 05. Narrativa, NPCs, Cutscenes e Códex Histórico

## 1. Princípios Narrativos
O objetivo primordial de *Dez Mil Dias* é proporcionar uma experiência onde o jogador aprende sobre a vida real de Miyamoto Musashi enquanto joga, distinguindo com clareza o que é história verídica daquilo que são lendas populares ou ficção do jogo.

---

## 2. Sistema de Diálogos com NPCs

### Mecânica de Interação no Godot 4:
1. **Deteção com `Area2D`:** Cada NPC possui uma área de colisão circular.
2. **Sinal Visual:** Quando o Musashi entra na área (`body_entered`), surge suavemente um balão sobre o NPC: `[E] Falar`.
3. **Bloqueio de Estado:** Ao pressionar `E`, o jogo entra no estado `DIALOGUE`, pausando o movimento livre do jogador.
4. **Interface Estilo Visual Novel:**
   - Caixa de texto em madeira escura na parte inferior.
   - Retrato do interlocutor desenhado com traços expressivos de tinta (*Sumi-e*).
   - Efeito de texto a escrever (*typewriter effect*) com som subtil de pincelada.
   - Tecla `Espaço` ou clique para avançar; suporte para ramificações simples (respostas de escolha múltipla).

---

## 3. Estrutura de Dados em Ficheiros JSON
Para manter o projeto modular e demonstrar competências de gestão de dados na PAP, todos os textos e diálogos são guardados em ficheiros `JSON` independentes:

### Exemplo de Estrutura: `data/dialogos.json`
```json
{
  "monge_dorinbo": {
    "nome": "Monge Dorinbo (Tio de Musashi)",
    "retrato": "res://assets/ui/portraits/dorinbo.png",
    "falas": [
      "Bennosuke... o treino com a espada de madeira não te torna invencível.",
      "Vi o desafio que o guerreiro Arima Kihei afixou no poste do templo. Não deves desafiá-lo por orgulho.",
      "A vida não é uma canção de guerra; cada golpe tem consequências irreparáveis."
    ]
  },
  "aldeao_pescador": {
    "nome": "Pescador da Aldeia",
    "retrato": "res://assets/ui/portraits/pescador.png",
    "falas": [
      "Aquele forasteiro Arima anda armado com uma lança e uma espada curta.",
      "Dizem que viaja de aldeia em aldeia à procura de glória fácil."
    ]
  }
}
```

---

## 4. As Cutscenes: Como Contar a História com Eficiência?

### A. Cutscenes "In-Engine" (Com `AnimationPlayer`)
Sem necessidade de desenhar vídeos externos, o Godot mexe a câmara e os sprites em tempo real:
* **Entrada do Duelo:**
  1. A câmara desliza da aldeia para o centro do pátio do templo.
  2. Faixas pretas cinemáticas surgem no topo e no fundo.
  3. Folhas de cerejeira sopram pelo ecrã enquanto a música tradicional ganha tensão.
  4. Arima Kihei dá dois passos e desembainha a espada.

### B. Cutscenes em Pergaminho Histórico (*Narrative Pan*)
* Para a introdução dos capítulos ou viagens longas.
* Uma gravura estática em alta resolução (estilo pintura tradicional japonesa).
* A câmara faz um movimento muito lento de zoom (*Ken Burns effect*) enquanto surge a narrativa histórica escrita no ecrã.

---

## 5. O Códex Histórico (Documentado, Lenda e Ficção)
O Códex é uma das principais marcas autorais e inovadoras do projeto. Sempre que o jogador investiga um monumento, fala com um monge ou termina um duelo, uma entrada é desbloqueada no menu do Códex:

### As Três Categorias de Fiabilidade:
1. 🟢 **DOCUMENTADO:** Factos confirmados por fontes primárias (o próprio *Go Rin no Sho*, monumentos funerários ou crónicas contemporâneas).
   - *Exemplo:* O duelo com Arima Kihei ocorreu em 1596, quando Musashi tinha 13 anos.
2. 🟡 **LENDA:** Tradições orais e episódios popularizados mais tarde (como no romance de Eiji Yoshikawa).
   - *Exemplo:* A lenda de que Musashi passou anos amarrado a uma árvore pelo monge Takuan para domar a sua agressividade.
3. 🔵 **FICÇÃO DO JOGO:** Diálogos, NPCs secundários e ligações de jogabilidade criadas expressamente para enriquecer o protótipo.

### Exemplo de Estrutura: `data/codex.json`
```json
[
  {
    "id": "duelo_arima_kihei",
    "titulo": "O Primeiro Duelo (Arima Kihei)",
    "classificacao": "DOCUMENTADO",
    "texto": "No prefácio do Livro dos Cinco Anéis, Musashi escreve que o seu primeiro combate ocorreu aos treze anos, contra um guerreiro da escola Shintō-ryū chamado Arima Kihei, derrotando-o com um bastão de madeira.",
    "desbloqueado": false
  }
]
```
