# Meu Primeiro Repositório

Este é um projeto de pratica criado para aprender a usar o GitHub
e enviar meu primeiro Pull Request com a ajuda do Claude Code.

## O que eu aprendi

- Criar uma conta no GitHub
- Conectar o GitHub CLI (gh)
- Fazer meu primeiro commit
- Abrir meu primeiro Pull Request

## Blocos e Câmera

Ferramenta para montar uma cena simples com blocos, animar a câmera e exportar
um vídeo-guia. Em vez de descrever o movimento de câmera por prompt, você
entrega esse vídeo para a IA de vídeo e ela segue o movimento exato.

Tudo está em um único arquivo: [`index.html`](index.html).

### Como abrir

Dê dois cliques em `index.html` (Chrome ou Edge, com internet). Não precisa
instalar nada. Para ter um link público, ative o GitHub Pages do repositório.

### Como usar

1. **Monte a cena.** Use a lista *Adicionar* (bloco, parede, piso, telhado,
   árvore, pessoa, carro) ou importe um modelo `.glb`. Clique em um objeto para
   mover, girar, mudar o tamanho em metros e a cor.
2. **Enquadre.** Arraste para orbitar, botão direito para deslocar, rolagem
   para aproximar. O retângulo claro é exatamente o que sai no vídeo. Ajuste a
   lente (mm), a inclinação e a altura da câmera.
3. **Grave o movimento.** Leve o cursor da linha do tempo ao instante desejado
   e clique em **+ Keyframe**. Repita em outro instante com outra vista. Ou use
   um dos *Movimentos prontos* (avançar, órbita, travelling, grua).
4. **Exporte.** *Exportar vídeo* gera um MP4 (H.264) no formato escolhido
   (9:16, 16:9, 1:1, 4:5 ou 4:3). *Exportar quadro atual* gera um PNG.

### Cena a partir de uma imagem

O botão **Cena por imagem** monta a maquete de blocos a partir de um render ou
de uma foto, já com a câmera no ponto de vista da imagem.

- **Com IA embutida** (na versão publicada no Claude): escolha a imagem e
  clique em *Montar cena com IA*.
- **Com qualquer outra IA**: clique em *Copiar prompt*, envie o prompt junto
  com a imagem, e cole de volta o JSON que ela responder.

A imagem fica por cima do quadro, com opacidade ajustável, para conferir o
enquadramento. O formato do JSON é este:

```json
{
  "objects": [
    {"type": "box", "name": "Térreo", "pos": [0, 0, 0], "size": [12, 3, 8], "rotY": 0, "color": "#4a4a4d"}
  ],
  "camera": {"pos": [-8, 1.6, 20], "target": [0, 3, 0], "focal": 24}
}
```

Medidas em metros, Y para cima. `pos` é o centro da base do objeto e `size` é
largura, altura e profundidade. Tipos aceitos: `box`, `cylinder`, `sphere`,
`ramp`, `roof`, `tree`, `person` e `car`.

### Do bloco ao vídeo realista

1. Exporte o PNG do primeiro quadro e gere a imagem realista dele em uma IA de
   imagem, mantendo o enquadramento.
2. Na IA de vídeo, envie a imagem realista como primeiro quadro (ou referência
   de estilo) e o MP4 dos blocos como vídeo de referência de movimento.
3. No prompt, descreva só o visual (materiais, luz, vegetação). O movimento já
   está no vídeo.

O passe *Profundidade* exporta o mesmo movimento em mapa de profundidade
(perto claro, longe escuro), para fluxos que usam controle por profundidade.

### Atalhos

| Tecla | Ação |
| --- | --- |
| G / E / R | Mover / girar / tamanho |
| K | Gravar keyframe |
| Espaço | Tocar e pausar |
| Ctrl+D | Duplicar |
| Delete | Excluir objeto |
| Ctrl+Z / Ctrl+Shift+Z | Desfazer / refazer |

### Limites conhecidos

- A cena fica salva no navegador. Use *Salvar cena* para guardar um arquivo.
- Modelos `.glb` importados valem só durante a sessão e não entram no arquivo
  da cena. Arquivos com compressão Draco não são lidos.
- Navegadores sem codificador H.264 gravam o vídeo em WebM, em tempo real.
