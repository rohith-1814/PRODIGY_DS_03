# PRODIGY_DS_03
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Fading Gradient Circle</title>
  <style>
    .gradient-circle {
      width: 200px;
      height: 200px;
      border-radius: 50%;
      background: radial-gradient(circle, #ff7e5f 0%, transparent 70%);
      margin: 50px auto;
    }
  </style>
</head>
<body>

  <div class="gradient-circle"></div>

</body>
</html>
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Monoline Solution Icon</title>
  <style>
    .solution-icon {
      width: 80px;
      height: 80px;
      border: 3px solid #4CAF50;
      border-radius: 50%;
      position: relative;
      margin: 50px auto;
    }

    .solution-icon::after {
      content: "";
      position: absolute;
      left: 22px;
      top: 40px;
      width: 15px;
      height: 30px;
      border: solid #4CAF50;
      border-width: 0 3px 3px 0;
      transform: rotate(45deg);
    }
  </style>
</head>
<body>

  <div class="solution-icon"></div>

</body>
</html>
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Tic-Tac-Toe</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      text-align: center;
      margin-top: 50px;
    }

    #board {
      display: grid;
      grid-template-columns: repeat(3, 100px);
      grid-gap: 5px;
      justify-content: center;
      margin-bottom: 20px;
    }

    .cell {
      width: 100px;
      height: 100px;
      font-size: 48px;
      background-color: #f2f2f2;
      border: 2px solid #333;
      display: flex;
      align-items: center;
      justify-content: center;
      cursor: pointer;
    }

    #status {
      font-size: 24px;
      margin-bottom: 10px;
    }

    button {
      padding: 8px 16px;
      font-size: 16px;
    }
  </style>
</head>
<body>

  <div id="status">Player X's turn</div>
  <div id="board"></div>
  <button onclick="resetGame()">Reset Game</button>

  <script>
    const board = document.getElementById("board");
    const status = document.getElementById("status");
    let currentPlayer = "X";
    let cells = Array(9).fill(null);
    let gameActive = true;

    function renderBoard() {
      board.innerHTML = "";
      cells.forEach((value, index) => {
        const cell = document.createElement("div");
        cell.className = "cell";
        cell.textContent = value || "";
        cell.addEventListener("click", () => handleClick(index));
        board.appendChild(cell);
      });
    }

    function handleClick(index) {
      if (!gameActive || cells[index]) return;

      cells[index] = currentPlayer;
      renderBoard();
      if (checkWinner()) {
        status.textContent = `Player ${currentPlayer} wins!`;
        gameActive = false;
      } else if (cells.every(Boolean)) {
        status.textContent = "It's a draw!";
        gameActive = false;
      } else {
        currentPlayer = currentPlayer === "X" ? "O" : "X";
        status.textContent = `Player ${currentPlayer}'s turn`;
      }
    }

    function checkWinner() {
      const winPatterns = [
        [0,1,2], [3,4,5], [6,7,8], // rows
        [0,3,6], [1,4,7], [2,5,8], // columns
        [0,4,8], [2,4,6]           // diagonals
      ];

      return winPatterns.some(pattern => {
        const [a, b, c] = pattern;
        return cells[a] && cells[a] === cells[b] && cells[b] === cells[c];
      });
    }

    function resetGame() {
      currentPlayer = "X";
      cells = Array(9).fill(null);
      gameActive = true;
      status.textContent = "Player X's turn";
      renderBoard();
    }

    renderBoard();
  </script>

</body>
</html>

