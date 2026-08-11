<!DOCTYPE html>
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>영안교회 유치부 초등저학년 말씀암송</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        @import url('https://cdn.jsdelivr.net/gh/orioncactus/pretendard/dist/web/static/pretendard.css');
        body { font-family: 'Pretendard', sans-serif; touch-action: manipulation; user-select: none; }
        .bounce-btn:active { transform: scale(0.95); }
    </style>
</head>
<body class="bg-amber-50 min-h-screen text-slate-800 flex flex-col justify-between">
    <div class="w-full max-w-sm mx-auto p-3 flex flex-col min-h-screen justify-between">
        <header class="bg-white rounded-2xl shadow-sm p-3 mb-2 text-center border-2 border-yellow-300">
            <h1 class="text-base font-black text-amber-600 mb-0.5">영안교회 유치부·초등저학년</h1>
            <p class="text-[11px] font-bold text-slate-600">말씀암송 놀이터</p>
            <div class="mt-1.5 flex justify-center gap-2 text-xs font-bold">
                <span class="bg-emerald-100 text-emerald-800 px-2.5 py-0.5 rounded-full text-[11px]" id="verse-badge">A-1</span>
            </div>
        </header>

        <div class="grid grid-cols-3 gap-1 mb-2">
            <button onclick="switchTab('study')" id="tab-study" class="py-2 px-1 text-xs rounded-xl font-bold bg-amber-500 text-white shadow-sm transition">말씀 카드</button>
            <button onclick="switchTab('quiz1')" id="tab-quiz1" class="py-2 px-1 text-xs rounded-xl font-bold bg-white text-slate-700 border border-amber-200 transition">빈칸 1개</button>
            <button onclick="switchTab('puzzle')" id="tab-puzzle" class="py-2 px-1 text-xs rounded-xl font-bold bg-white text-slate-700 border border-amber-200 transition">조각 맞추기</button>
        </div>

        <main class="flex-1 flex flex-col justify-center space-y-2">
            <div id="view-study" class="space-y-2">
                <div class="bg-white rounded-2xl shadow-sm p-4 border-2 border-amber-200 text-center relative overflow-hidden">
                    <div class="text-[11px] text-slate-400 mb-1">카드를 클릭하면 전체 말씀이 나와요</div>
                    <div id="verse-ref" class="text-lg font-black text-amber-700 mb-2 py-1">고린도후서 5:17</div>
                    
                    <div id="verse-card-box" onclick="toggleVerseContent()" class="min-h-[90px] flex items-center justify-center p-3 bg-amber-50 rounded-xl border border-dashed border-amber-300 cursor-pointer transition hover:bg-amber-100 mb-2">
                        <p id="verse-text" class="text-xs font-bold text-slate-400">여기를 눌러서 말씀을 확인해보세요</p>
                    </div>

                    <div class="flex justify-center gap-1.5 mb-3">
                        <button onclick="setVoiceType('normal')" id="v-normal" class="px-3 py-1.5 rounded-xl text-[11px] font-bold bg-amber-500 text-white shadow-sm">정상 목소리</button>
                        <button onclick="setVoiceType('funny')" id="v-funny" class="px-3 py-1.5 rounded-xl text-[11px] font-bold bg-slate-100 text-slate-600">재미 목소리</button>
                    </div>
                    
                    <div class="grid grid-cols-2 gap-2">
                        <button onclick="speakVerse()" class="bounce-btn py-2.5 bg-pink-500 active:bg-pink-600 text-white rounded-xl text-xs font-bold shadow-sm flex items-center justify-center gap-1">
                            목소리로 듣기
                        </button>
                        <button onclick="nextVerse()" class="bounce-btn py-2.5 bg-amber-500 active:bg-amber-600 text-white rounded-xl text-xs font-bold shadow-sm flex items-center justify-center gap-1">
                            다음 말씀
                        </button>
                    </div>
                </div>
            </div>

            <div id="view-quiz1" class="hidden space-y-2">
                <div class="bg-white rounded-2xl shadow-sm p-4 border-2 border-sky-200 text-center">
                    <h2 class="text-xs font-black text-sky-700 mb-2">빈칸에 들어갈 알맞은 낱말은</h2>
                    <div id="blank1-container" class="text-xs font-bold text-slate-700 leading-relaxed mb-3 min-h-[60px] flex flex-wrap items-center justify-center gap-1 p-2 bg-sky-50 rounded-xl border border-sky-100"></div>
                    <div id="quiz1-options" class="grid grid-cols-2 gap-2 mb-1"></div>
                    <div id="quiz1-result" class="text-xs font-bold hidden"></div>
                </div>
            </div>

            <div id="view-puzzle" class="hidden space-y-2">
                <div class="bg-white rounded-2xl shadow-sm p-4 border-2 border-emerald-200 text-center">
                    <h2 class="text-xs font-black text-emerald-700 mb-2">말씀 조각을 순서대로 맞추어보세요</h2>
                    <div id="puzzle-target" class="min-h-[60px] bg-emerald-50 border border-dashed border-emerald-300 rounded-xl p-2.5 flex flex-wrap gap-1 mb-2 items-center"></div>
                    <div id="puzzle-source" class="flex flex-wrap gap-1 mb-3 max-h-[100px] overflow-y-auto justify-center"></div>
                    <div class="flex gap-2">
                        <button onclick="resetPuzzle()" class="flex-1 py-2 bg-slate-100 text-slate-700 rounded-xl text-xs font-bold">처음부터</button>
                        <button onclick="checkPuzzle()" class="flex-2 py-2 bg-emerald-600 text-white rounded-xl text-xs font-bold">정답 확인</button>
                    </div>
                    <div id="puzzle-result" class="mt-1 text-xs font-bold hidden"></div>
                </div>
            </div>
        </main>

        <footer class="text-center py-1.5 text-[11px] text-slate-400 font-bold">
            영안교회 유치부 초등저학년 말씀암송
        </footer>
    </div>

    <script>
        const verses = [
            { id: "A-1", ref: "고린도후서 5:17", words: ["그런즉", "누구든지", "그리스도", "안에", "있으면", "새로운", "피조물이라", "이전", "것은", "지나갔으니", "보라", "새", "것이", "되었도다"], blank1Idx: 5 },
            { id: "A-2", ref: "갈라디아서 2:20", words: ["내가", "그리스도와", "함께", "십자가에", "못", "박혔나니", "그런즉", "이제는", "내가", "산", "것이", "아니요", "오직", "내", "안에", "그리스도께서", "사시는", "것이라"], blank1Idx: 3 },
            { id: "A-4", ref: "요한복음 14:21", words: ["나의", "계명을", "지키는", "자라야", "나를", "사랑하는", "자니", "나를", "사랑하는", "자는", "내", "아버지께", "사랑을", "받을", "것이요"], blank1Idx: 2 },
            { id: "A-5", ref: "디모데후서 3:16", words: ["모든", "성경은", "하나님의", "감동으로", "된", "것으로", "교훈과", "책망과", "바르게", "함과", "의로", "교육하기에", "유익하니"], blank1Idx: 3 },
            { id: "A-6", ref: "여호수아 1:8", words: ["이", "율법책을", "네", "입에서", "떠나지", "말게", "하며", "주야로", "그것을", "묵상하여", "그", "안에", "기록된", "대로", "다", "지켜", "행하라"], blank1Idx: 3 }
        ];

        let currentIndex = 0;
        let isVerseRevealed = false;
        let currentVoice = 'normal';
        const fakeWordsPool = ["믿음", "사랑", "소망", "기쁨", "은혜", "평안", "생명", "진리", "축복", "기도"];

        let userPuzzleWords = [];
        let shuffledPuzzleWords = [];

        function switchTab(tab) {
            ['study', 'quiz1', 'puzzle'].forEach(t => {
                document.getElementById(`view-${t}`).classList.add('hidden');
                document.getElementById(`tab-${t}`).className = "py-2 px-1 text-xs rounded-xl font-bold bg-white text-slate-700 border border-amber-200 transition";
            });
            document.getElementById(`view-${tab}`).classList.remove('hidden');
            document.getElementById(`tab-${tab}`).className = "py-2 px-1 text-xs rounded-xl font-bold bg-amber-500 text-white shadow-sm transition";

            if (tab === 'quiz1') loadQuiz1();
            if (tab === 'puzzle') loadPuzzle();
        }

        function setVoiceType(type) {
            currentVoice = type;
            ['normal', 'funny'].forEach(v => {
                const btn = document.getElementById(`v-${v}`);
                if (v === type) {
                    btn.className = "px-3 py-1.5 rounded-xl text-[11px] font-bold bg-amber-500 text-white shadow-sm";
                } else {
                    btn.className = "px-3 py-1.5 rounded-xl text-[11px] font-bold bg-slate-100 text-slate-600";
                }
            });
        }

        function loadVerse() {
            const v = verses[currentIndex];
            document.getElementById('verse-ref').innerText = v.ref;
            document.getElementById('verse-badge').innerText = v.id;
            isVerseRevealed = false;
            
            const textBox = document.getElementById('verse-text');
            textBox.innerText = "여기를 눌러서 말씀을 확인해보세요";
            textBox.className = "text-xs font-bold text-slate-400";
        }

        function toggleVerseContent() {
            const v = verses[currentIndex];
            const textBox = document.getElementById('verse-text');
            isVerseRevealed = !isVerseRevealed;
            
            if (isVerseRevealed) {
                textBox.innerText = v.words.join(' ');
                textBox.className = "text-xs font-bold text-slate-800 leading-relaxed";
            } else {
                textBox.innerText = "여기를 눌러서 말씀을 확인해보세요";
                textBox.className = "text-xs font-bold text-slate-400";
            }
        }

        function nextVerse() {
            currentIndex = (currentIndex + 1) % verses.length;
            loadVerse();
        }

        function speakVerse() {
            if ('speechSynthesis' in window) {
                window.speechSynthesis.cancel();
                const v = verses[currentIndex];
                let spokenRef = v.ref.replace(':', '장 ');
                spokenRef += '절';
                
                const utterance = new SpeechSynthesisUtterance(`${spokenRef}. ${v.words.join(' ')}`);
                utterance.lang = 'ko-KR';

                if (currentVoice === 'normal') {
                    utterance.pitch = 1.0;
                    utterance.rate = 0.9;
                } else if (currentVoice === 'funny') {
                    utterance.pitch = 1.9;
                    utterance.rate = 1.3;
                }

                window.speechSynthesis.speak(utterance);
            }
        }

        function loadQuiz1() {
            const v = verses[currentIndex];
            const correctWord = v.words[v.blank1Idx];
            const container = document.getElementById('blank1-container');
            const optionsContainer = document.getElementById('quiz1-options');
            document.getElementById('quiz1-result').classList.add('hidden');

            container.innerHTML = v.words.map((w, idx) => {
                if (idx === v.blank1Idx) {
                    return `<span class="bg-white text-sky-600 px-2 py-0.5 rounded-lg border border-dashed border-sky-400 font-black">빈칸</span>`;
                }
                return `<span>${w}</span>`;
            }).join(' ');

            let wrongs = fakeWordsPool.filter(w => w !== correctWord).sort(() => Math.random() - 0.5).slice(0, 3);
            let options = [correctWord, ...wrongs].sort(() => Math.random() - 0.5);

            optionsContainer.innerHTML = options.map(opt => `
                <button onclick="checkQuiz1('${opt}', '${correctWord}')" class="bounce-btn py-2 px-2 bg-sky-100 active:bg-sky-200 text-sky-900 rounded-xl text-xs font-bold transition border border-sky-200">
                    ${opt}
                </button>
            `).join('');
        }

        function checkQuiz1(selected, correct) {
            const resultEl = document.getElementById('quiz1-result');
            resultEl.classList.remove('hidden');

            if (selected === correct) {
                resultEl.innerText = "참 잘했어요 정답이에요";
                resultEl.className = "text-xs font-bold text-emerald-600 mb-1";
                
                const v = verses[currentIndex];
                const container = document.getElementById('blank1-container');
                container.innerHTML = v.words.map((w, idx) => {
                    if (idx === v.blank1Idx) {
                        return `<span class="bg-emerald-500 text-white px-2 py-0.5 rounded-lg font-black">${w}</span>`;
                    }
                    return `<span>${w}</span>`;
                }).join(' ');

                setTimeout(() => {
                    nextVerse();
                    switchTab('study');
                }, 1500);
            } else {
                resultEl.innerText = "아쉬워요 다시 골라보세요";
                resultEl.className = "text-xs font-bold text-rose-500 mb-1";
            }
        }

        function loadPuzzle() {
            const v = verses[currentIndex];
            userPuzzleWords = [];
            shuffledPuzzleWords = [...v.words].sort(() => Math.random() - 0.5);
            renderPuzzleBoard();
            document.getElementById('puzzle-result').classList.add('hidden');
        }

        function renderPuzzleBoard() {
            const sourceContainer = document.getElementById('puzzle-source');
            const targetContainer = document.getElementById('puzzle-target');

            sourceContainer.innerHTML = shuffledPuzzleWords.map((w, i) => `
                <button onclick="selectPuzzleWord('${w}', ${i}, 'source')" class="px-2 py-1 bg-emerald-100 active:bg-emerald-200 text-emerald-900 rounded-lg text-xs font-bold transition">${w}</button>
            `).join('');

            targetContainer.innerHTML = userPuzzleWords.map((w, i) => `
                <button onclick="selectPuzzleWord('${w}', ${i}, 'target')" class="px-2 py-1 bg-emerald-600 text-white rounded-lg text-xs font-bold transition">${w}</button>
            `).join('');
        }

        function selectPuzzleWord(word, index, from) {
            if (from === 'source') {
                userPuzzleWords.push(word);
                shuffledPuzzleWords.splice(index, 1);
            } else {
                shuffledPuzzleWords.push(word);
                userPuzzleWords.splice(index, 1);
            }
            renderPuzzleBoard();
        }

        function resetPuzzle() {
            loadPuzzle();
        }

        function checkPuzzle() {
            const v = verses[currentIndex];
            const resultEl = document.getElementById('puzzle-result');
            resultEl.classList.remove('hidden');

            const userStr = userPuzzleWords.join(' ');
            const correctStr = v.words.join(' ');

            if (userStr === correctStr) {
                resultEl.innerText = "모든 조각을 맞혔어요 참 잘했어요";
                resultEl.className = "mt-1 text-xs font-bold text-emerald-600";
                setTimeout(() => {
                    nextVerse();
                    switchTab('study');
                }, 1500);
            } else {
                resultEl.innerText = "순서가 올바르지 않아요 다시 해보세요";
                resultEl.className = "mt-1 text-xs font-bold text-rose-500";
            }
        }

        window.onload = loadVerse;
    </script>
</body>
</html>

