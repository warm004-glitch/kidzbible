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
            <h1 class="text-lg font-black text-amber-600 mb-0.5">영안교회 유치부·초등저학년</h1>
            <p class="text-xs font-bold text-slate-600">40구절 말씀암송 놀이터</p>
            <div class="mt-1.5 flex justify-center gap-2 text-sm font-bold">
                <span class="bg-emerald-100 text-emerald-800 px-3 py-1 rounded-full text-sm" id="verse-badge">A-1</span>
            </div>
        </header>

        <div class="grid grid-cols-3 gap-1 mb-2">
            <button onclick="switchTab('study')" id="tab-study" class="py-2.5 px-1 text-sm rounded-xl font-bold bg-amber-500 text-white shadow-sm transition">말씀 카드</button>
            <button onclick="switchTab('quiz1')" id="tab-quiz1" class="py-2.5 px-1 text-sm rounded-xl font-bold bg-white text-slate-700 border border-amber-200 transition">빈칸 1개</button>
            <button onclick="switchTab('puzzle')" id="tab-puzzle" class="py-2.5 px-1 text-sm rounded-xl font-bold bg-white text-slate-700 border border-amber-200 transition">조각 맞추기</button>
        </div>

        <main class="flex-1 flex flex-col justify-center space-y-2">
            <div id="view-study" class="space-y-2">
                <div class="bg-white rounded-2xl shadow-sm p-4 border-2 border-amber-200 text-center relative overflow-hidden">
                    <div class="text-sm text-slate-500 mb-1 font-bold" id="verse-num-label">A-1 구절을 읽어보세요</div>
                    <div id="verse-ref" class="text-2xl font-black text-amber-700 mb-3 py-1">고린도후서 5:17</div>
                    
                    <div id="verse-card-box" onclick="toggleVerseContent()" class="min-h-[140px] flex items-center justify-center p-4 bg-amber-50 rounded-xl border border-dashed border-amber-300 cursor-pointer transition hover:bg-amber-100 mb-3">
                        <p id="verse-text" class="text-lg font-bold text-slate-400 leading-snug">여기를 눌러서 말씀을 확인해보세요</p>
                    </div>

                    <div class="flex justify-center gap-2 mb-3">
                        <button onclick="setVoiceType('normal')" id="v-normal" class="px-4 py-2 rounded-xl text-sm font-bold bg-amber-500 text-white shadow-sm">정상 목소리</button>
                        <button onclick="setVoiceType('funny')" id="v-funny" class="px-4 py-2 rounded-xl text-sm font-bold bg-slate-100 text-slate-600">재미 목소리</button>
                    </div>
                    
                    <div class="grid grid-cols-2 gap-2">
                        <button onclick="speakVerse()" class="bounce-btn py-3.5 bg-pink-500 active:bg-pink-600 text-white rounded-xl text-base font-bold shadow-sm flex items-center justify-center gap-1">
                            목소리로 듣기
                        </button>
                        <button onclick="nextVerse()" class="bounce-btn py-3.5 bg-amber-500 active:bg-amber-600 text-white rounded-xl text-base font-bold shadow-sm flex items-center justify-center gap-1">
                            다음 말씀
                        </button>
                    </div>
                </div>
            </div>

            <div id="view-quiz1" class="hidden space-y-2">
                <div class="bg-white rounded-2xl shadow-sm p-4 border-2 border-sky-200 text-center">
                    <h2 class="text-base font-black text-sky-700 mb-2">빈칸에 들어갈 알맞은 낱말은</h2>
                    <div id="blank1-container" class="text-lg font-bold text-slate-700 leading-relaxed mb-3 min-h-[90px] flex flex-wrap items-center justify-center gap-2 p-3 bg-sky-50 rounded-xl border border-sky-100"></div>
                    <div id="quiz1-options" class="grid grid-cols-2 gap-2 mb-1"></div>
                    <div id="quiz1-result" class="text-base font-bold hidden"></div>
                </div>
            </div>

            <div id="view-puzzle" class="hidden space-y-2">
                <div class="bg-white rounded-2xl shadow-sm p-4 border-2 border-emerald-200 text-center">
                    <h2 class="text-base font-black text-emerald-700 mb-2">말씀 조각을 두 단어씩 순서대로 맞추어보세요</h2>
                    <div id="puzzle-target" class="min-h-[90px] bg-emerald-50 border border-dashed border-emerald-300 rounded-xl p-3 flex flex-wrap gap-2 mb-2 items-center"></div>
                    <div id="puzzle-source" class="flex flex-wrap gap-1.5 mb-3 max-h-[130px] overflow-y-auto justify-center"></div>
                    <div class="flex gap-2">
                        <button onclick="resetPuzzle()" class="flex-1 py-3 bg-slate-100 text-slate-700 rounded-xl text-sm font-bold">처음부터</button>
                        <button onclick="checkPuzzle()" class="flex-2 py-3 bg-emerald-600 text-white rounded-xl text-sm font-bold">정답 확인</button>
                    </div>
                    <div id="puzzle-result" class="mt-1 text-sm font-bold hidden"></div>
                </div>
            </div>
        </main>

        <footer class="text-center py-1.5 text-xs text-slate-400 font-bold">
            영안교회 유치부 초등저학년 말씀암송
        </footer>
    </div>

    <script>
        const verses = [
            { id: "A-1", ref: "고린도후서 5:17", text: "그런즉 누구든지 그리스도 안에 있으면 새로운 피조물이라 이전 것은 지나갔으니 보라 새 것이 되었도다", blankIdx: 5 },
            { id: "A-2", ref: "갈라디아서 2:20", text: "내가 그리스도와 함께 십자가에 못 박혔나니 그런즉 이제는 내가 산 것이 아니요 오직 내 안에 그리스도께서 사시는 것이라", blankIdx: 3 },
            { id: "A-4", ref: "요한복음 14:21", text: "나의 계명을 지키는 자라야 나를 사랑하는 자니 나를 사랑하는 자는 내 아버지께 사랑을 받을 것이요 나도 그를 사랑하여 그에게 나를 나타내리라", blankIdx: 2 },
            { id: "A-5", ref: "디모데후서 3:16", text: "모든 성경은 하나님의 감동으로 된 것으로 교훈과 책망과 바르게 함과 의로 교육하기에 유익하니", blankIdx: 3 },
            { id: "A-6", ref: "여호수아 1:8", text: "이 율법책을 네 입에서 떠나지 말게 하며 주야로 그것을 묵상하여 그 안에 기록된 대로 다 지켜 행하라 그리하면 네 길이 평탄하게 될 것이며 네가 형통하리라", blankIdx: 3 },
            { id: "A-7", ref: "요한복음 15:7", text: "너희가 내 안에 거하고 내 말이 너희 안에 거하면 무엇이든지 원하는 대로 구하라 그리하면 이루리라", blankIdx: 2 },
            { id: "A-9", ref: "마태복음 18:20", text: "두 세 사람이 내 이름으로 모인 곳에는 나도 그들 중에 있느니라", blankIdx: 2 },
            { id: "A-11", ref: "마가복음 4:19", text: "세상의 염려와 재물의 유혹과 기타 욕심이 들어와 말씀을 막아 결실하지 못하게 됨이요", blankIdx: 1 },
            { id: "B-1", ref: "로마서 3:23", text: "모든 사람이 죄를 범하였으매 하나님의 영광에 이르지 못하더니", blankIdx: 1 },
            { id: "B-2", ref: "이사야 53:6", text: "우리는 다 양 같아서 그릇 행하여 각기 제 길로 갔거늘 여호와께서는 우리 모두의 죄악을 그에게 담당시키셨도다", blankIdx: 2 },
            { id: "B-3", ref: "로마서 6:23", text: "죄의 삯은 사망이요 하나님의 은사는 그리스도 예수 우리 주 안에 있는 영생이니라", blankIdx: 2 },
            { id: "B-4", ref: "히브리서 9:27", text: "한 번 죽는 것은 사람에게 정해진 것이요 그 후에는 심판이 있으리니", blankIdx: 3 },
            { id: "B-5", ref: "로마서 5:8", text: "우리가 아직 죄인 되었을 때에 그리스도께서 우리를 위하여 죽으심으로 하나님께서 우리에 대한 자기의 사랑을 확증하셨느니라", blankIdx: 3 },
            { id: "B-7", ref: "에베소서 2:8-9", text: "너희는 그 은혜에 의하여 믿음으로 말미암아 구원을 받았으니 이것은 너희에게서 난 것이 아니요 하나님의 선물이라", blankIdx: 3 },
            { id: "B-9", ref: "요한복음 1:12", text: "영접하는 자 곧 그 이름을 믿는 자들에게는 하나님의 자녀가 되는 권세를 주셨으니", blankIdx: 1 },
            { id: "B-10", ref: "요한계시록 3:20", text: "볼지어다 내가 문 밖에 서서 두드리노니 누구든지 내 음성을 듣고 문을 열면 내가 그에게로 들어가 그와 더불어 먹고 그는 나와 더불어 먹으리라", blankIdx: 3 },
            { id: "B-11", ref: "요한일서 5:13", text: "내가 하나님의 아들의 이름을 믿는 너희에게 이것을 쓰는 것은 너희로 하여금 너희에게 영생이 있음을 알게 하려 함이라", blankIdx: 3 },
            { id: "B-12", ref: "요한복음 5:24", text: "내가 진실로 진실로 너희에게 이르노니 내 말을 듣고 또 나 보내신 이를 믿는 자는 영생을 얻었고 심판에 이르지 아니하나니 사망에서 생명으로 옮겼느니라", blankIdx: 3 },
            { id: "C-1", ref: "고린도전서 3:16", text: "너희는 너희가 하나님의 성전인 것과 하나님의 성령이 너희 안에 계시는 것을 알지 못하느냐", blankIdx: 3 },
            { id: "C-4", ref: "빌립보서 4:13", text: "내게 능력 주시는 자 안에서 내가 모든 것을 할 수 있느니라", blankIdx: 1 },
            { id: "C-5", ref: "예레미야애가 3:22-23", text: "여호와의 인자와 긍휼이 무궁하시므로 우리가 진멸되지 아니함이니이다 이것들이 아침마다 새로우니 주의 성실하심이 크시도소이다", blankIdx: 2 },
            { id: "C-7", ref: "이사야 26:3", text: "주께서 심지가 견고한 자를 평강하고 평강하도록 지키시리니 이는 그가 주를 신뢰함이니이다", blankIdx: 2 },
            { id: "C-8", ref: "베드로전서 5:7", text: "너희 염려를 다 주께 맡기라 이는 그가 너희를 돌보심이라", blankIdx: 2 },
            { id: "C-9", ref: "로마서 8:32", text: "자기 아들을 아끼지 아니하시고 우리 모든 사람을 위하여 내주신 이가 어찌 그 아들과 함께 모든 것을 우리에게 주시지 아니하겠느냐", blankIdx: 2 },
            { id: "C-10", ref: "빌립보서 4:19", text: "나의 하나님이 그리스도 예수 안에서 영광 가운데 그 풍성한 대로 너희 모든 쓸 것을 채우시리라", blankIdx: 2 },
            { id: "C-11", ref: "히브리서 2:18", text: "그가 시험을 받아 고난을 당하셨은즉 시험 받는 자들을 능히 도우실 수 있느니라", blankIdx: 2 },
            { id: "D-1", ref: "마태복음 6:33", text: "그런즉 너희는 먼저 그의 나라와 그의 의를 구하라 그리하면 이 모든 것을 너희에게 더하시리라", blankIdx: 3 },
            { id: "D-2", ref: "누가복음 9:23", text: "또 무리에게 이르시되 아무든지 나를 따라오려거든 자기를 부인하고 날마다 제 십자가를 지고 나를 따를 것이니라", blankIdx: 3 },
            { id: "D-4", ref: "로마서 12:2", text: "너희는 이 세대를 본받지 말고 오직 마음을 새롭게 함으로 변화를 받아 하나님의 선하시고 기뻐하시고 온전하신 뜻이 무엇인지 분별하도록 하라", blankIdx: 3 },
            { id: "D-5", ref: "고린도전서 15:58", text: "그러므로 내 사랑하는 형제들아 견실하며 흔들리지 말고 항상 주의 일에 더욱 힘쓰는 자들이 되라 이는 너희 수고가 주 안에서 헛되지 않은 줄 앎이라", blankIdx: 3 },
            { id: "D-7", ref: "마가복음 10:45", text: "인자가 온 것은 섬김을 받으려 함이 아니라 도리어 섬기려 하고 자기 목숨을 많은 사람의 대속물로 주려 함이니라", blankIdx: 2 },
            { id: "D-9", ref: "잠언 3:9-10", text: "네 재물과 네 소산물의 처음 익은 열매로 여호와를 공경하라 그리하면 네 창고가 가득히 차고 네 포도즙 틀에 새 포도즙이 가득하리라", blankIdx: 2 },
            { id: "D-11", ref: "사도행전 1:8", text: "오직 성령이 너희에게 임하시면 너희가 권능을 받고 예루살렘과 온 유대와 사마리아와 땅 끝까지 이르러 내 증인이 되리라", blankIdx: 2 },
            { id: "E-1", ref: "마태복음 28:19-20", text: "그러므로 너희는 가서 모든 민족을 제자로 삼아 아버지와 아들과 성령의 이름으로 세례를 베풀고 내가 너희에게 분부한 모든 것을 가르쳐 지키게 하라 볼지어다 내가 세상 끝날까지 너희와 항상 함께 있으리라 하시니라", blankIdx: 3 },
            { id: "E-2", ref: "요한일서 3:18", text: "자녀들아 우리가 말과 혀로만 사랑하지 말고 행함과 진실함으로 하자", blankIdx: 2 },
            { id: "E-3", ref: "빌립보서 2:3-4", text: "아무 일이든지 다툼이나 허영으로 하지 말고 오직 겸손한 마음으로 각각 자기보다 남을 낫게 여기고 각각 자기 일을 볼뿐더러 또한 각각 다른 사람들의 일을 돌아보아 나의 기쁨을 충만하게 하라", blankIdx: 3 },
            { id: "E-5", ref: "에베소서 5:3", text: "음행과 온갖 더러운 것과 탐욕은 너희 중에서 그 이름조차도 부르지 말라 이는 성도에게 마땅한 바니라", blankIdx: 2 },
            { id: "E-7", ref: "히브리서 13:11", text: "너희는 도둑질하지 말며 속이지 말며 서로 거짓말하지 말라", blankIdx: 1 },
            { id: "E-9", ref: "히브리서 11:6", text: "믿음이 없이는 하나님을 기쁘시게 하지 못하나니 하나님께 나아가는 자는 반드시 그가 계신 것과 또한 그가 자기를 찾는 자들에게 상 주시는 이심을 믿어야 할지니라", blankIdx: 3 },
            { id: "E-12", ref: "마태복음 5:16", text: "이같이 너희 빛이 사람 앞에 비치게 하여 그들로 너희 착한 행실을 보고 하늘에 계신 너희 아버지께 영광을 돌리게 하라", blankIdx: 3 }
        ];

        let currentIndex = 0;
        let isVerseRevealed = false;
        let currentVoice = 'normal';
        const fakeWordsPool = ["믿음", "사랑", "소망", "기쁨", "은혜", "평안", "생명", "진리", "축복", "기도"];

        let userPuzzleChunks = [];
        let shuffledPuzzleChunks = [];

        function getChunks(text) {
            const words = text.split(' ');
            const chunks = [];
            for (let i = 0; i < words.length; i += 2) {
                if (i + 1 < words.length) {
                    chunks.push(words[i] + ' ' + words[i + 1]);
                } else {
                    chunks.push(words[i]);
                }
            }
            return chunks;
        }

        function switchTab(tab) {
            ['study', 'quiz1', 'puzzle'].forEach(t => {
                document.getElementById(`view-${t}`).classList.add('hidden');
                document.getElementById(`tab-${t}`).className = "py-2.5 px-1 text-sm rounded-xl font-bold bg-white text-slate-700 border border-amber-200 transition";
            });
            document.getElementById(`view-${tab}`).classList.remove('hidden');
            document.getElementById(`tab-${tab}`).className = "py-2.5 px-1 text-sm rounded-xl font-bold bg-amber-500 text-white shadow-sm transition";

            if (tab === 'quiz1') loadQuiz1();
            if (tab === 'puzzle') loadPuzzle();
        }

        function setVoiceType(type) {
            currentVoice = type;
            ['normal', 'funny'].forEach(v => {
                const btn = document.getElementById(`v-${v}`);
                if (v === type) {
                    btn.className = "px-4 py-2 rounded-xl text-sm font-bold bg-amber-500 text-white shadow-sm";
                } else {
                    btn.className = "px-4 py-2 rounded-xl text-sm font-bold bg-slate-100 text-slate-600";
                }
            });
        }

        function loadVerse() {
            const v = verses[currentIndex];
            document.getElementById('verse-ref').innerText = v.ref;
            document.getElementById('verse-badge').innerText = v.id;
            document.getElementById('verse-num-label').innerText = `${v.id} 구절을 읽어보세요`;
            isVerseRevealed = false;
            
            const textBox = document.getElementById('verse-text');
            textBox.innerText = "여기를 눌러서 말씀을 확인해보세요";
            textBox.className = "text-lg font-bold text-slate-400";
        }

        function toggleVerseContent() {
            const v = verses[currentIndex];
            const textBox = document.getElementById('verse-text');
            isVerseRevealed = !isVerseRevealed;
            
            if (isVerseRevealed) {
                textBox.innerText = v.text;
                textBox.className = "text-lg font-bold text-slate-800 leading-snug";
            } else {
                textBox.innerText = "여기를 눌러서 말씀을 확인해보세요";
                textBox.className = "text-lg font-bold text-slate-400";
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
                
                const utterance = new SpeechSynthesisUtterance(`${spokenRef}. ${v.text}`);
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
            const words = v.text.split(' ');
            const blankIdx = Math.min(v.blankIdx, words.length - 1);
            const correctWord = words[blankIdx];
            
            const container = document.getElementById('blank1-container');
            const optionsContainer = document.getElementById('quiz1-options');
            document.getElementById('quiz1-result').classList.add('hidden');

            container.innerHTML = words.map((w, idx) => {
                if (idx === blankIdx) {
                    return `<span class="bg-white text-sky-600 px-3 py-1.5 rounded-xl border-2 border-dashed border-sky-400 font-black text-lg">빈칸</span>`;
                }
                return `<span class="text-lg">${w}</span>`;
            }).join(' ');

            let wrongs = fakeWordsPool.filter(w => w !== correctWord).sort(() => Math.random() - 0.5).slice(0, 3);
            let options = [correctWord, ...wrongs].sort(() => Math.random() - 0.5);

            optionsContainer.innerHTML = options.map(opt => `
                <button onclick="checkQuiz1('${opt}', '${correctWord}', ${blankIdx})" class="bounce-btn py-3 px-3 bg-sky-100 active:bg-sky-200 text-sky-900 rounded-xl text-base font-bold transition border border-sky-200">
                    ${opt}
                </button>
            `).join('');
        }

        function checkQuiz1(selected, correct, blankIdx) {
            const resultEl = document.getElementById('quiz1-result');
            resultEl.classList.remove('hidden');

            if (selected === correct) {
                resultEl.innerText = "참 잘했어요 정답이에요";
                resultEl.className = "text-base font-bold text-emerald-600 mb-1";
                
                const v = verses[currentIndex];
                const words = v.text.split(' ');
                const container = document.getElementById('blank1-container');
                container.innerHTML = words.map((w, idx) => {
                    if (idx === blankIdx) {
                        return `<span class="bg-emerald-500 text-white px-3 py-1.5 rounded-xl font-black text-lg">${w}</span>`;
                    }
                    return `<span class="text-lg">${w}</span>`;
                }).join(' ');

                setTimeout(() => {
                    nextVerse();
                    switchTab('study');
                }, 1500);
            } else {
                resultEl.innerText = "아쉬워요 다시 골라보세요";
                resultEl.className = "text-base font-bold text-rose-500 mb-1";
            }
        }

        function loadPuzzle() {
            const v = verses[currentIndex];
            userPuzzleChunks = [];
            const correctChunks = getChunks(v.text);
            shuffledPuzzleChunks = [...correctChunks].sort(() => Math.random() - 0.5);
            renderPuzzleBoard();
            document.getElementById('puzzle-result').classList.add('hidden');
        }

        function renderPuzzleBoard() {
            const sourceContainer = document.getElementById('puzzle-source');
            const targetContainer = document.getElementById('puzzle-target');

            sourceContainer.innerHTML = shuffledPuzzleChunks.map((chunk, i) => `
                <button onclick="selectPuzzleChunk('${chunk}', ${i}, 'source')" class="px-3.5 py-2 bg-emerald-100 active:bg-emerald-200 text-emerald-900 rounded-xl text-sm font-bold transition">${chunk}</button>
            `).join('');

            targetContainer.innerHTML = userPuzzleChunks.map((chunk, i) => `
                <button onclick="selectPuzzleChunk('${chunk}', ${i}, 'target')" class="px-3.5 py-2 bg-emerald-600 text-white rounded-xl text-sm font-bold transition">${chunk}</button>
            `).join('');
        }

        function selectPuzzleChunk(chunk, index, from) {
            if (from === 'source') {
                userPuzzleChunks.push(chunk);
                shuffledPuzzleChunks.splice(index, 1);
            } else {
                shuffledPuzzleChunks.push(chunk);
                userPuzzleChunks.splice(index, 1);
            }
            renderPuzzleBoard();
        }

        function resetPuzzle() {
            loadPuzzle();
        }

        function checkPuzzle() {
            const v = verses[currentIndex];
            const resultEl = document.getElementById('puzzle-result');
            resultEl.classList.add('hidden');

            const userStr = userPuzzleChunks.join(' ');
            const correctStr = getChunks(v.text).join(' ');

            if (userStr === correctStr) {
                resultEl.innerText = "모든 조각을 맞혔어요 참 잘했어요";
                resultEl.className = "mt-1 text-base font-bold text-emerald-600";
                setTimeout(() => {
                    nextVerse();
                    switchTab('study');
                }, 1500);
            } else {
                resultEl.innerText = "순서가 올바르지 않아요 다시 해보세요";
                resultEl.className = "mt-1 text-base font-bold text-rose-500";
            }
        }

        window.onload = loadVerse;
    </script>
</body>
</html>

