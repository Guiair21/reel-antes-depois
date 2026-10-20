# Como eu fiz o Reel de antes e depois da minha foto

Tirei essa foto da cachoeira do Buraco do Padre, no Parque Nacional dos Campos Gerais, com o iPhone 15 Pro, e editei no Lightroom do celular. O vídeo quem montou foi o Claude. Vou te passar o caminho inteiro pra você fazer o seu, beleza?

**O que é meu e o que é da inteligência artificial:** a foto e a edição são minhas. A montagem, a trilha e a animação dos cards o Claude fez. Os cards eu gerei no Codex, e a voz do final é um clone da minha.

## O passo a passo

1. Tira a foto. Qualquer celular serve.
2. Edita no app que você já usa. Eu usei o Lightroom do celular.
3. Exporta duas versões do mesmo clique: a original, sem ajuste nenhum, e a editada, no tamanho máximo.
4. Tira o print das informações da foto. No iPhone, abre a foto na galeria e arrasta pra cima. No Android, toca em Detalhes. Aparece data, aparelho e local, e é isso que prova que a foto é sua.
5. Abre o [Claude Code](https://claude.com/claude-code) numa pasta vazia, coloca as fotos lá dentro e cola o prompt aqui de baixo.
6. Responde o que ele perguntar e espera. Aqui o vídeo levou uns 7 minutos pra ficar pronto.
7. Assiste, pede o ajuste que quiser e posta.

Quer os cards do final? Gera no gerador de imagem que você tiver (ChatGPT, Codex, Gemini) com um pôster de referência anexado. E confere letra por letra, porque gerador de imagem ainda erra acento.

Quer a voz? Grava você mesmo falando a frase do final. Se usar clone, marca o post como feito com inteligência artificial.

## O prompt

Clica no botão de copiar no canto do bloco e cola no Claude Code.

```
Você vai montar comigo um Reel vertical de antes e depois de uma foto que eu tirei e editei. Trabalhe na pasta atual, com Python e ffmpeg. Antes de começar, confira se eu tenho Python 3.10 ou mais novo e ffmpeg; se faltar, me diga como instalar. Instale com pip: opencv-python numpy pillow scipy soundfile.

PRIMEIRO ME PERGUNTE, uma coisa por vez, e espere cada resposta:
1. qual arquivo é a foto original e qual é a editada (precisam ser do mesmo clique);
2. se eu tenho o print das informações da foto (data, aparelho, local);
3. o título de duas linhas (padrão "EDITADO" / "NO CELULAR") e o rodapé com o equipamento que usei de verdade (ex.: "IPHONE 15 PRO" / "LIGHTROOM MOBILE");
4. minhas cores (fundo, texto, destaque) ou se uso o padrão: fundo #efefef, texto #2a2a2a, destaque #7d0001;
5. se eu tenho cards 9:16 prontos para o final;
6. se eu tenho um áudio com a minha voz falando a frase do final, e em qual card ela entra;
7. se eu tenho um som ambiente do lugar (cachoeira, mar, vento).

O VÍDEO (1080x1920, 30 qps, H.264 + AAC):
1. Alinhamento: a edição costuma mudar o enquadramento. Use SIFT + homografia do OpenCV (MAGSAC) para encaixar a original sobre a editada, equalizando antes com CLAHE, porque a original é escura. Recorte a maior área, na proporção da editada, que as duas cobrem. Me diga o erro mediano em pixels: abaixo de 1,5 px não fica fantasma.
2. Cenário: fundo liso na cor de fundo; um iPhone visto de cima no centro (600x1228 px, cantos arredondados, moldura cinza, botões laterais, sombra suave embaixo, ilha dinâmica); título em Anton em cima, em duas linhas, a segunda na cor de destaque; rodapé pequeno em Inter Bold com letras espaçadas embaixo. Baixe Anton e Inter do repositório oficial do Google Fonts.
3. Prova (2,6 s, se houver print): o print ocupa a tela do celular; depois de 0,3 s o resto escurece e os blocos de data/aparelho e de local ganham contorno na cor de destaque. Ache esses blocos olhando o print.
4. Revelação (10 s): a original na tela vira a editada em pinceladas largas de borda macia (raio de 13% da largura da foto): céu de 1,4 a 3 s, laterais de 3,2 a 5,5 s, base de 5,6 a 7 s, e o que sobrar completa até 7,8 s.
5. Antes e depois: aos 8,6 s volta a original por 0,5 s com a etiqueta "ANTES" no canto da foto; depois a editada com "DEPOIS", que some aos 10 s.
6. Tela cheia (3,4 s): clique de câmera com clarão branco de 0,18 s; a editada ocupa a tela inteira e aproxima de 6% para 13%, com inclinação de 0,8 grau para cima e giro de 0,4 grau. Bem leve.
7. Cards (se houver): cada card entra com fusão de 0,35 s. Dê profundidade: recorte a forma clara grande do card como camada própria, preencha o fundo onde ela estava (inpaint), faça a forma entrar deslizando e girando de fora da tela e seguir andando mais que o fundo, com sombra projetada macia. O fundo aproxima de 1,00 para 1,05. Por cima, um feixe de luz quente atravessando na diagonal na entrada, um foco suave passeando e vinheta nas bordas respirando de leve. Fade para preto no último 0,6 s.

A TRILHA (sintetizada, sem nenhum som de terceiros):
- Pad sereno em Lá maior que nunca corta: Lá add9, Fá# menor 7, Ré maj9 e de volta ao Lá aberto quando a foto fica inteira, cada acorde nascendo enquanto o anterior some; 5 osciladores levemente desafinados por nota, passa-baixa em 900 Hz.
- Efeitos graves de trailer, sintetizados: obturador no início da prova; glitch curto e queda de grave no corte para a foto; um hit grave em cada pincelada; um som reverso que sobe e para seco; 0,2 s em que só os efeitos baixam; slam com sub de 55 Hz quando a foto fica inteira; glitch no ANTES, hit seco no DEPOIS, obturador de novo no clique final e um boom leve na entrada de cada card.
- Ambiente (se houver): abafado durante a prova, aberto na revelação, crescendo quando a água aparece, saindo quando entra o card.
- Reverb longo (uns 4 s) no pad e nos efeitos. A voz entra SECA, sem reverb, e o pad baixa enquanto ela fala.
- Normalize para -14 LUFS em duas passadas.

ANTES DE ME ENTREGAR: gere uma folha de quadros (um por segundo) e olhe você mesmo: título inteiro, foto alinhada, ANTES aparecendo, cards sem texto cortado. Me mostre a folha, abra o vídeo e me diga a duração e o volume medido.

REGRAS: não invente tela de aplicativo nem apresente o vídeo como gravação da edição; ele é uma transição de antes e depois. Se eu usar voz clonada ou card gerado por inteligência artificial, me lembre de marcar o post como feito com inteligência artificial.
```

Fez o seu? Me marca no [@euguidasilva](https://www.instagram.com/euguidasilva/), que eu quero ver.

---

Desenvolvido por Guilherme Carlos da Silva.
