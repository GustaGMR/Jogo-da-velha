README — Jogo da Velha com Limite de 6 Jogadas
📋 Descrição
Este arquivo contém a implementação de um Jogo da Velha (Tic-Tac-Toe) em React, baseado no tutorial clássico da documentação do React, porém com uma regra personalizada: o tabuleiro só pode conter, no máximo, 6 peças simultaneamente.

Quando esse limite é atingido, a jogada mais antiga é automaticamente removida do tabuleiro, criando um efeito de "fila deslizante" (FIFO — First In, First Out).

🎯 Objetivo
Demonstrar como modificar o comportamento padrão do Jogo da Velha para implementar uma mecânica alternativa onde as peças "expiram" após certo número de jogadas, exigindo dos jogadores uma estratégia diferente da convencional.

⚙️ Regras do Jogo
Dois jogadores alternam turnos: X sempre começa.

Cada jogador clica em uma casa vazia para posicionar sua peça.

Regra especial: o tabuleiro só pode ter 6 peças ao mesmo tempo.

Ao inserir a 7ª peça, a peça mais antiga é removida automaticamente.

A vitória ocorre quando três peças do mesmo jogador formam uma linha (horizontal, vertical ou diagonal).

Após uma vitória, o botão "Jogar novamente" reinicia a partida.

🧩 Estrutura do Código
Componentes
Componente	Responsabilidade
Square	Renderiza uma única casa (botão) do tabuleiro.
Board	Renderiza as 9 casas e controla os cliques.
Game	Gerencia o estado global da partida (tabuleiro, histórico, vencedor).
Funções auxiliares
calculateWinner(squares) — Verifica se há um vencedor percorrendo as 8 combinações possíveis.

🔄 Lógica da Regra de 6 Jogadas
A função handlePlay implementa a regra principal:

js
let nextHistory = [...history, { index, player }];

if (nextHistory.length > 6) {
  const oldest = nextHistory.shift(); // remove a jogada mais antiga
  if (finalSquares[oldest.index] === oldest.player) {
    finalSquares[oldest.index] = null;
  }
}
Detalhes importantes

O history funciona como uma fila FIFO.

Antes de apagar a peça antiga, verifica-se se aquela casa ainda contém a peça original. Isso evita apagar uma peça mais recente que tenha sido colocada na mesma casa depois.

Como o histórico é limitado a 6 entradas, ele não armazena o histórico completo da partida (diferente do tutorial original).

🖥️ Interface
Tabuleiro
Grade 3×3 de botões clicáveis.

Mostra o status: "Next player: X" ou "Winner: X".

Painel de informações (game-info)
Contador: Jogadas no tabuleiro: N / 6

Fila de jogadas: exibe a ordem das peças, por exemplo:

text
X@4 → O@0 → X@8 → O@2 → X@6 → O@1
Botão "Jogar novamente" — aparece somente quando há um vencedor.


🔁 Diferenças em relação ao Jogo da Velha original do React
Aspecto	Original	Esta versão
Histórico	Completo, com navegação entre jogadas	Limitado a 6 entradas
Remoção de peças	Não existe	Peça mais antiga é removida
Estado do tabuleiro	Derivado do histórico	Mantido separadamente em squares
Botão de reinício	Não possui	resetGame() reinicia tudo
Navegação "Go to move #"	Sim	Removida

⚠️ Observações Técnicas
O código comentado no início do arquivo é a versão original do tutorial, mantida apenas como referência.

O history desta versão não serve como linha do tempo navegável — ele representa apenas a fila de peças ativas.

Como o tabuleiro é armazenado à parte, o calculateWinner é chamado diretamente sobre finalSquares.

🧠 Possíveis Extensões
Ajustar o limite de peças (ex.: 4, 5, 8) tornando-o configurável.

Adicionar navegação reversa no histórico.

Implementar IA para jogar contra o computador.

Exibir animação ao remover a peça mais antiga.

Adicionar placar de vitórias entre os jogadores.

📄 Licença
Código livre para fins educacionais, baseado no tutorial oficial do React (react.dev).
