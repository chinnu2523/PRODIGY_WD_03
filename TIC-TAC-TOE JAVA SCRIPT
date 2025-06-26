const cellElements = document.querySelectorAll('[data-cell]');
const board = document.querySelector('.game-board');
const statusText = document.querySelector('.status-text');
const restartButton = document.querySelector('.restart-btn');

let isPlayerXTurn = true;
let gameActive = true;
const winningCombinations = [
    [0, 1, 2],
    [3, 4, 5],
    [6, 7, 8],
    [0, 3, 6],
    [1, 4, 7],
    [2, 5, 8],
    [0, 4, 8],
    [2, 4, 6]
];
let currentBoard = ["", "", "", "", "", "", "", "", ""];

startGame();

function startGame() {
    isPlayerXTurn = true;
    gameActive = true;
    currentBoard = ["", "", "", "", "", "", "", "", ""];
    statusText.innerText = `Player X's turn`;
    cellElements.forEach(cell => {
        cell.classList.remove('x');
        cell.classList.remove('o');
        cell.removeEventListener('click', handleClick);
        cell.addEventListener('click', handleClick, { once: true });
    });
}

function handleClick(e) {
    const cell = e.target;
    const currentClass = isPlayerXTurn ? 'x' : 'o';
    const playerSymbol = isPlayerXTurn ? 'X' : 'O';
    const cellIndex = Array.from(cellElements).indexOf(cell);

    if (!gameActive || currentBoard[cellIndex] !== "") return;

    // Place Mark
    placeMark(cell, currentClass);
    currentBoard[cellIndex] = playerSymbol;

    // Check For Win
    if (checkWin(currentClass)) {
        endGame(false);
    } else if (isDraw()) {
        // Check For Draw
        endGame(true);
    } else {
        // Switch Turns
        swapTurns();
        statusText.innerText = `Player ${isPlayerXTurn ? 'X' : 'O'}'s turn`;
    }
}

function endGame(draw) {
    gameActive = false;
    if (draw) {
        statusText.innerText = 'It\'s a Draw!';
    } else {
        statusText.innerText = `Player ${isPlayerXTurn ? 'X' : 'O'} Wins!`;
    }
}

function isDraw() {
    return [...cellElements].every(cell => {
        return cell.classList.contains('x') || cell.classList.contains('o');
    });
}

function placeMark(cell, currentClass) {
    cell.classList.add(currentClass);
}

function swapTurns() {
    isPlayerXTurn = !isPlayerXTurn;
}

function checkWin(currentClass) {
    return winningCombinations.some(combination => {
        return combination.every(index => {
            return cellElements[index].classList.contains(currentClass);
        });
    });
}

restartButton.addEventListener('click', startGame);
