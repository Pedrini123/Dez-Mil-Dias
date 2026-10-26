# 02. Design Visual e Estilo Artístico

## 1. Visão Estética Geral
O estilo visual de *Dez Mil Dias* baseia-se numa união cuidadosa entre a estética retro de **Pixel Art refinada (16/32-Bit)** para o jogo ativo e a tradição artística da pintura a tinta da China (**Sumi-e / Ukiyo-e**) para a narrativa e interfaces.

* **Inspiração Principal:** *First Cut: Samurai Duel*, *Katana ZERO*, *Eastward* e as pinturas clássicas do próprio Musashi.
* **Ferramentas de Criação:** Aseprite (sprites e animações) e Krita / IA generativa (apenas conceitos de retratos e ilustrações históricas com revisão manual).

---

## 2. Padrão das Personagens e Proporções Corporais

### O Teste de Escala em Píxeis:
Para garantir coerência visual milimétrica, os personagens foram aferidos na mesma escala:
* **Miyamoto Musashi (Protagonista):** Altura visível de **34 píxeis**.
* **Arima Kihei (Rival do Duelo 1):** Altura visível de **35 píxeis**.
* **Akiyama (Rival do Duelo 2):** Altura visível de **34 píxeis**.

### Proporção de 5 a 6 Cabeças:
* Não utilizamos modelos *chibi* (cabeças exageradas e infantis).
* A proporção de 5 a 6 cabeças confere uma anatomia atlética e sóbria que permite:
  1. Leitura nítida das três posturas clássicas de katana: alta (*jōdan*), média (*chūdan*) e baixa (*gedan*).
  2. Lâminas com 25 a 30 píxeis de alcance, facilitando a identificação do alcance (*maai*) e a janela de defesa (*parry*).

---

## 3. Resolução Interna e Grid de Cenários
* **Resolução Base:** Viewport de **320x180** píxeis (ou 480x270).
* **Escala Automática no Godot 4:**
  - Modo `canvas_items` ou `viewport` com filtro *Nearest* (*Pixel Perfect*).
  - Escala com nitidez sem distorção para 1280x720 (4x) e 1920x1080 (6x Full HD).
* **Escala do Mundo:**
  - O chão ocupa a base do ecrã (30 a 40 píxeis).
  - O samurai de 34 píxeis ocupa cerca de 20% da altura do ecrã, passando confortavelmente pelas portas das casas japonesas e permitindo uma visão ampla do horizonte.

---

## 4. Iluminação Dinâmica e Atmosfera Feudal

Em vez de criar dezenas de cenários desenhados à mão, utilizamos o sistema de iluminação 2D do Godot 4 (`CanvasModulate`, luzes pontuais `PointLight2D` e partículas `GPUParticles2D`):

| Atmosfera | Iluminação no Godot | Efeito Narrativo no Jogo |
| :--- | :--- | :--- |
| **Manhã Clara** | Luz solar suave, ligeira névoa matinal. | Fase de exploração pacífica da aldeia e treino inicial. |
| **Pôr do Sol (*Golden Hour*)** | Tonalidade alaranjada/dourada com sombras compridas. | Momento tenso antes do primeiro duelo contra Arima Kihei. |
| **Noite sob Luar** | Azul-escuro e cinzas profundos; reflexos brilhantes na lâmina. | Introspecção, investigação secreta ou tensão noturna. |
| **Chuva e Vento** | Partículas diagonais de gotas, relâmpagos e folhas a voar. | Duelos decisivos de vida ou morte. |

---

## 5. Efeitos de Impacto, Lâminas e Sangue

1. **Rasto da Espada (*Slash Arc*):**
   - Efeito visual de arco branco/cinzento semitransparente com duração de 0.08 a 0.12 segundos para acentuar a velocidade da katana.
2. **Faíscas de Defesa (*Parry Sparks*):**
   - Partículas douradas e brancas na ponta de contacto das duas lâminas quando um golpe é aparado com sucesso.
3. **Sangue e Finalizações:**
   - Efeito em leque com partículas de sangue (`CPUParticles2D`).
   - Manchas estáticas no solo (*blood decals*) que permanecem após o término do golpe letal.
   - Reação sóbria e dramática: o adversário derrotado cai de joelhos e larga a espada, mantendo a honra e o respeito característicos da época.
