let secretNumber = Math.floor(Math.random() * 100) + 1;
let attempts = 0;
let guessHistory = [];
let minRange = 1;
let maxRange = 100;
let isGameOver = false;

// Load Best Score from localStorage if available
let bestScore = localStorage.getItem('guessBestScore') || '-';

// DOM Elements helper with safety checks
function getElement(id) {
    return document.getElementById(id);
}

// Initialize UI elements once DOM is fully loaded
function initGame() {
    const bestScoreEl = getElement('bestScore');
    if (bestScoreEl) bestScoreEl.innerText = bestScore;

    const userGuessInput = getElement('userGuess');
    if (userGuessInput) userGuessInput.focus();
}

function handleGuess(event) {
    if (event) event.preventDefault();
    if (isGameOver) return;

    const userGuessInput = getElement('userGuess');
    if (!userGuessInput) return;

    const guess = parseInt(userGuessInput.value);

    // Validation checks
    if (isNaN(guess) || guess < 1 || guess > 100) {
        showFeedback('Peringatan!', 'Masukkan angka yang valid antara 1 sampai 100.', 'warning');
        return;
    }

    if (guessHistory.includes(guess)) {
        showFeedback('Sudah Ditebak!', `Kamu sudah pernah menebak angka ${guess}. Coba angka lain.`, 'warning');
        userGuessInput.value = '';
        return;
    }

    attempts++;
    const attemptCountEl = getElement('attemptCount');
    if (attemptCountEl) attemptCountEl.innerText = attempts;

    guessHistory.push(guess);
    updateHistoryUI();

    // Evaluate guess against secret number
    if (guess === secretNumber) {
        isGameOver = true;
        handleWin();
    } else if (guess < secretNumber) {
        if (guess >= minRange) minRange = guess + 1;
        showFeedback('Lebih Besar! 📈', `Angka rahasia lebih besar dari ${guess}.`, 'higher');
        updateRangeIndicator();
    } else {
        if (guess <= maxRange) maxRange = guess - 1;
        showFeedback('Lebih Kecil! 📉', `Angka rahasia lebih kecil dari ${guess}.`, 'lower');
        updateRangeIndicator();
    }

    userGuessInput.value = '';
    userGuessInput.focus();
}

function showFeedback(title, desc, type) {
    const feedbackTitle = getElement('feedbackTitle');
    const feedbackDesc = getElement('feedbackDesc');
    const feedbackContainer = getElement('feedbackContainer');

    if (feedbackTitle) feedbackTitle.innerText = title;
    if (feedbackDesc) feedbackDesc.innerText = desc;

    if (feedbackContainer) {
        feedbackContainer.className = "mb-6 p-4 rounded-2xl border text-center transition-all duration-300";
        if (type === 'higher') {
            feedbackContainer.classList.add('bg-blue-950/50', 'border-blue-500/50');
            if (feedbackTitle) feedbackTitle.className = "text-lg font-bold text-blue-400";
        } else if (type === 'lower') {
            feedbackContainer.classList.add('bg-purple-950/50', 'border-purple-500/50');
            if (feedbackTitle) feedbackTitle.className = "text-lg font-bold text-purple-400";
        } else if (type === 'win') {
            feedbackContainer.classList.add('bg-emerald-950/50', 'border-emerald-500/50');
            if (feedbackTitle) feedbackTitle.className = "text-lg font-bold text-emerald-400";
        } else {
            feedbackContainer.classList.add('bg-amber-950/50', 'border-amber-500/50');
            if (feedbackTitle) feedbackTitle.className = "text-lg font-bold text-amber-400";
        }
    }
}

function handleWin() {
    showFeedback('Selamat! 🎉', `Kamu berhasil menebak angka ${secretNumber} dalam ${attempts} percobaan!`, 'win');
    
    const submitBtn = getElement('submitBtn');
    const resetBtn = getElement('resetBtn');
    const userGuessInput = getElement('userGuess');

    if (submitBtn) submitBtn.classList.add('hidden');
    if (resetBtn) resetBtn.classList.remove('hidden');
    if (userGuessInput) userGuessInput.disabled = true;

    if (bestScore === '-' || attempts < parseInt(bestScore)) {
        bestScore = attempts;
        localStorage.setItem('guessBestScore', bestScore);
        const bestScoreEl = getElement('bestScore');
        if (bestScoreEl) bestScoreEl.innerText = bestScore;
    }
}

function updateHistoryUI() {
    const historyListEl = getElement('historyList');
    if (!historyListEl) return;

    if (guessHistory.length === 0) {
        historyListEl.innerHTML = '<span class="text-xs text-slate-500 italic">Belum ada tebakan.</span>';
        return;
    }

    historyListEl.innerHTML = '';
    guessHistory.forEach(val => {
        const badge = document.createElement('span');
        badge.className = `px-2.5 py-1 rounded-xl text-xs font-bold ${
            val === secretNumber 
            ? 'bg-emerald-500 text-white' 
            : val < secretNumber 
                ? 'bg-blue-500/20 text-blue-300 border border-blue-500/30' 
                : 'bg-purple-500/20 text-purple-300 border border-purple-500/30'
        }`;
        badge.innerText = val;
        historyListEl.appendChild(badge);
    });
}

function updateRangeIndicator() {
    const rangeIndicatorEl = getElement('rangeIndicator');
    if (rangeIndicatorEl) {
        rangeIndicatorEl.innerText = `Rentang: ${minRange} - ${maxRange}`;
    }
}

function resetGame() {
    secretNumber = Math.floor(Math.random() * 100) + 1;
    attempts = 0;
    guessHistory = [];
    minRange = 1;
    maxRange = 100;
    isGameOver = false;

    const attemptCountEl = getElement('attemptCount');
    if (attemptCountEl) attemptCountEl.innerText = '0';

    updateRangeIndicator();

    const userGuessInput = getElement('userGuess');
    if (userGuessInput) {
        userGuessInput.disabled = false;
        userGuessInput.value = '';
    }

    const submitBtn = getElement('submitBtn');
    const resetBtn = getElement('resetBtn');
    if (submitBtn) submitBtn.classList.remove('hidden');
    if (resetBtn) resetBtn.classList.add('hidden');

    showFeedback('Ayo Mulai Tebak!', 'Komputer telah memilih angka baru. Masukkan tebakanmu!', 'default');
    updateHistoryUI();
    if (userGuessInput) userGuessInput.focus();
}

window.onload = function() {
    initGame();
};