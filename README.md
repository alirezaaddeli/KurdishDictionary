# KurdishDictionary
<!DOCTYPE html>
<html lang="ckb" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>فەرهەنگی پێشکەوتووی ئینگلیزی - کوردی سۆرانی</title>
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet">
    <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css" rel="stylesheet">
    <link href="https://fonts.googleapis.com/css2?family=Noto+Sans+Arabic:wght@400;700&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/animate.css/4.1.1/animate.min.css" />
    <style>
        :root {
            --primary-color: #1E88E5;
            --secondary-color: #FFC107;
            --background-color: #F5F5F5;
            --text-color: #333;
            --card-bg-color: #ffffff;
            --border-color: #E0E0E0;
        }

        body {
            font-family: 'Noto Sans Arabic', sans-serif;
            background-color: var(--background-color);
            color: var(--text-color);
            line-height: 1.6;
        }

        .container {
            max-width: 1100px;
            margin: 2rem auto;
            padding: 2rem;
            background-color: var(--card-bg-color);
            border-radius: 15px;
            box-shadow: 0 10px 20px rgba(0, 0, 0, 0.1);
        }

        h1 {
            color: var(--primary-color);
            text-align: center;
            margin-bottom: 2rem;
        }

        .input-group {
            margin-bottom: 1.5rem;
        }

        .btn-primary {
            background-color: var(--primary-color);
            border-color: var(--primary-color);
            transition: all 0.3s ease;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
        }

        .btn-primary:hover {
            background-color: #0D47A1;
            border-color: #0D47A1;
            transform: translateY(-2px);
        }

        .card {
            border: none;
            border-radius: 15px;
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
            margin-bottom: 1.5rem;
            overflow: hidden;
            transition: all 0.3s ease;
        }

        .card-header {
            background-color: var(--primary-color);
            color: white;
            font-weight: bold;
            padding: 1rem;
        }

        .btn-secondary {
            background-color: var(--secondary-color);
            border-color: var(--secondary-color);
            color: var(--text-color);
        }

        .btn-secondary:hover {
            background-color: #FFA000;
            border-color: #FFA000;
        }
        
        .image-container {
            margin-top: 20px;
            text-align: center;
        }

        .image-container img {
            max-width: 100%;
            border-radius: 10px;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
            transition: all 0.3s ease;
        }

        .image-container img:hover {
            transform: scale(1.05);
            box-shadow: 0 8px 16px rgba(0, 0, 0, 0.2);
        }

        .error-message {
            color: #D32F2F;
            background-color: #FFCDD2;
            border: 1px solid #D32F2F;
            border-radius: 4px;
            padding: 10px;
            margin-top: 10px;
            display: none;
        }

        .pronunciation-options {
            display: flex;
            gap: 10px;
            margin-top: 10px;
        }

        .pronunciation-btn {
            padding: 5px 10px;
            border: 1px solid var(--primary-color);
            border-radius: 5px;
            background-color: #fff;
            color: var(--primary-color);
            cursor: pointer;
            transition: all 0.3s ease;
        }
        
        .pronunciation-btn:hover {
            background-color: var(--primary-color);
            color: #fff;
        }
    </style>
</head>
<body>
    <div class="container animate__animated animate__fadeIn">
        <h1>فەرهەنگی پێشکەوتووی ئینگلیزی - کوردی سۆرانی</h1>
        <div class="input-group mb-3">
            <input type="text" id="wordInput" class="form-control" placeholder="وشەیەکی ئینگلیزی بنووسە" />
            <button class="btn btn-primary" type="button" id="searchBtn">
                <i class="fas fa-search"></i> گەڕان
            </button>
        </div>

        <div id="loadingSpinner" class="text-center" style="display: none;">
            <div class="spinner-border text-primary" role="status">
                <span class="visually-hidden">چاوەڕوان بە...</span>
            </div>
        </div>

        <div id="errorMessage" class="error-message animate__animated animate__shakeX"></div>

        <div id="resultCard" class="card animate__animated animate__fadeIn" style="display: none;">
            <div class="card-header">
                <div class="word-header">
                    <div>
                        <span id="wordTitle" class="word-title"></span>
                        <span id="levelIndicator" class="level-indicator"></span>
                    </div>
                    <div class="pronunciation-container">
                        <span id="phonetic" class="phonetic"></span>
                        <div class="pronunciation-options">
                            <button class="pronunciation-btn" id="pronounceBtn-us">US 🇺🇸</button>
                            <button class="pronunciation-btn" id="pronounceBtn-uk">UK 🇬🇧</button>
                            <button class="pronunciation-btn" id="pronounceBtn-slow">Slow ⏳</button>
                        </div>
                    </div>
                </div>
            </div>
            <div class="card-body">
                <div id="imageContainer" class="image-container mb-4"></div>
                <div id="translationContainer">
                    <h3 id="translationTitle">وەرگێڕانی کوردی</h3>
                    <p id="translation"></p>
                </div>
                <div id="definitions"></div>
                <div id="examples"></div>
                <div id="idioms"></div>
                <h3>هاوواتاکان</h3>
                <div id="synonyms" class="synonyms"></div>
                <h3>دژواتاکان</h3>
                <div id="antonyms" class="antonyms"></div>
                <div id="wordForms" class="word-forms"></div>
                <div id="etymology" class="etymology"></div>
                <div id="usageNotes" class="usage-notes"></div>
                <h3>تێبینی</h3>
                <textarea id="noteInput" rows="3" placeholder="تێبینیەکانت لێرە بنووسە..."></textarea>
                <div class="btn-group mt-3">
                    <button class="btn btn-secondary" id="favoriteBtn">
                        <i class="fas fa-star"></i> زیادکردن بۆ دڵخوازەکان
                    </button>
                    <button class="btn btn-secondary" id="saveNoteBtn">
                        <i class="fas fa-save"></i> پاشەکەوتکردنی تێبینی
                    </button>
                </div>
            </div>
        </div>

        <div class="row">
            <div class="col-md-6">
                <div class="card animate__animated animate__fadeInLeft">
                    <div class="card-header">دڵخوازەکان</div>
                    <div class="card-body">
                        <ul id="favoritesList"></ul>
                    </div>
                </div>
            </div>
        </div>
    </div>

    <script>
        const DICTIONARY_API = 'https://api.dictionaryapi.dev/api/v2/entries/en/';
        const TRANSLATION_API = 'https://api.mymemory.translated.net/get?langpair=en|ckb&q=';
        const UNSPLASH_API = 'https://api.unsplash.com/search/photos';
        const UNSPLASH_ACCESS_KEY = 'YOUR_UNSPLASH_ACCESS_KEY'; // با کلید واقعی خود جایگزین کنید

        const elements = {
            wordInput: document.getElementById('wordInput'),
            searchBtn: document.getElementById('searchBtn'),
            resultCard: document.getElementById('resultCard'),
            wordTitle: document.getElementById('wordTitle'),
            levelIndicator: document.getElementById('levelIndicator'),
            phonetic: document.getElementById('phonetic'),
            definitions: document.getElementById('definitions'),
            translation: document.getElementById('translation'),
            examples: document.getElementById('examples'),
            synonyms: document.getElementById('synonyms'),
            antonyms: document.getElementById('antonyms'),
            wordForms: document.getElementById('wordForms'),
            idioms: document.getElementById('idioms'),
            etymology: document.getElementById('etymology'),
            usageNotes: document.getElementById('usageNotes'),
            imageContainer: document.getElementById('imageContainer'),
            noteInput: document.getElementById('noteInput'),
            pronounceBtnUs: document.getElementById('pronounceBtn-us'),
            pronounceBtnUk: document.getElementById('pronounceBtn-uk'),
            pronounceBtnSlow: document.getElementById('pronounceBtn-slow'),
            favoriteBtn: document.getElementById('favoriteBtn'),
            saveNoteBtn: document.getElementById('saveNoteBtn'),
            favoritesList: document.getElementById('favoritesList'),
            loadingSpinner: document.getElementById('loadingSpinner'),
            errorMessage: document.getElementById('errorMessage')
        };

        let state = {
            favorites: JSON.parse(localStorage.getItem('favorites')) || [],
            notes: JSON.parse(localStorage.getItem('notes')) || {},
            currentWord: '',
            wordData: null
        };

        async function searchWord() {
            const word = elements.wordInput.value.trim();
            if (!word) return;

            showLoading(true);
            hideError();

            try {
                const [dictionaryResponse, translationResponse, imageResponse] = await Promise.all([
                    fetch(DICTIONARY_API + word),
                    fetch(TRANSLATION_API + encodeURIComponent(word)),
                    fetch(`${UNSPLASH_API}?query=${word}&client_id=${UNSPLASH_ACCESS_KEY}`)
                ]);

                const dictionaryData = await dictionaryResponse.json();
                const translationData = await translationResponse.json();
                const imageData = await imageResponse.json();

                if (dictionaryResponse.ok && translationResponse.ok) {
                    state.wordData = dictionaryData[0];
                    displayResult(state.wordData, translationData.responseData.translatedText, imageData);
                    state.currentWord = word;
                    loadNote();
                } else {
                    throw new Error('وشەکە نەدۆزرایەوە');
                }
            } catch (error) {
                showError(error.message);
            } finally {
                showLoading(false);
            }
        }

        function displayResult(data, translatedText, imageData) {
            elements.wordTitle.textContent = data.word;
            elements.phonetic.textContent = data.phonetic || '';

            elements.definitions.innerHTML = '';
            data.meanings.forEach(meaning => {
                const defDiv = document.createElement('div');
                defDiv.className = 'definition animate__animated animate__fadeIn';
                defDiv.innerHTML = `
                    <div class="part-of-speech">${meaning.partOfSpeech}</div>
                    <ol>
                        ${meaning.definitions.map(def => `
                            <li>
                                ${def.definition}
                                ${def.example ? `<p class="example">Example: ${def.example}</p>` : ''}
                            </li>
                        `).join('')}
                    </ol>
                `;
                elements.definitions.appendChild(defDiv);
            });

            elements.translation.textContent = translatedText;

            elements.examples.innerHTML = '<h3>نموونەکان</h3>';
            const allExamples = data.meanings.flatMap(meaning => 
                meaning.definitions.filter(def => def.example).map(def => def.example)
            );
            if (allExamples.length > 0) {
                elements.examples.innerHTML += `<ul>${allExamples.map(ex => `<li class="example">${ex}</li>`).join('')}</ul>`;
            } else {
                elements.examples.innerHTML += '<p>هیچ نموونەیەک نەدۆزرایەوە</p>';
            }

            displayWordList(elements.synonyms, data.meanings.flatMap(meaning => meaning.synonyms));
            displayWordList(elements.antonyms, data.meanings.flatMap(meaning => meaning.antonyms));

            elements.wordForms.innerHTML = '<h3>فۆڕمەکانی وشە</h3>';
            const wordForms = getWordForms(data);
            if (Object.keys(wordForms).length > 0) {
                elements.wordForms.innerHTML += Object.entries(wordForms).map(([form, value]) => `
                    <div class="word-form">
                        <span class="word-form-title">${form}:</span> ${value}
                    </div>
                `).join('');
            } else {
                elements.wordForms.innerHTML += '<p>هیچ فۆڕمێکی تر نەدۆزرایەوە</p>';
            }

            elements.etymology.innerHTML = `<h3>ڕەچەڵەکناسی</h3><p>${data.etymology || 'بەردەست نییە'}</p>`;
            elements.usageNotes.innerHTML = '<h3 class="usage-title">تێبینیەکانی بەکارهێنان</h3>';
            elements.usageNotes.innerHTML += (data.usageNotes && data.usageNotes.length > 0) ?
                data.usageNotes.map(note => `<p>${note}</p>`).join('') :
                '<p>هیچ تێبینیەک نەدۆزرایەوە</p>';

            if (imageData.results && imageData.results.length > 0) {
                const img = document.createElement('img');
                img.src = imageData.results[0].urls.small;
                img.alt = data.word;
                img.classList.add('animate__animated', 'animate__fadeIn');
                elements.imageContainer.innerHTML = '';
                elements.imageContainer.appendChild(img);
            } else {
                elements.imageContainer.innerHTML = '<p>هیچ وێنەیەک نەدۆزرایەوە</p>';
            }

            setupPronunciation(data);    
            elements.resultCard.style.display = 'block';
            updateFavoriteButton();
        }

        function displayWordList(element, words) {
            element.innerHTML = '';
            if (words && words.length > 0) {
                words.forEach(word => {
                    const span = document.createElement('span');
                    span.textContent = word;
                    element.appendChild(span);
                });
            } else {
                element.textContent = 'بەردەست نییە';
            }
        }

        function getWordForms(data) {
            const forms = {};
            data.meanings.forEach(meaning => {
                if (meaning.partOfSpeech === 'verb') {
                    forms['Infinitive'] = data.word;
                } else if (meaning.partOfSpeech === 'noun') {
                    forms['Singular'] = data.word;
                } else if (meaning.partOfSpeech === 'adjective') {
                    forms['Positive'] = data.word;
                }
            });
            return forms;
        }

        function setupPronunciation(data) {
            const pronunciations = {
                us: data.phonetics.find(p => p.audio && p.audio.includes('-us.mp3'))?.audio,
                uk: data.phonetics.find(p => p.audio && p.audio.includes('-uk.mp3'))?.audio,
                default: data.phonetics.find(p => p.audio)?.audio
            };

            elements.pronounceBtnUs.onclick = () => playPronunciation('us', pronunciations);
            elements.pronounceBtnUk.onclick = () => playPronunciation('uk', pronunciations);
            elements.pronounceBtnSlow.onclick = () => playSlowPronunciation(data.word);
        }

        function playPronunciation(type, pronunciations) {
            const audioPath = pronunciations[type] || pronunciations.default || `https://api.dictionaryapi.dev/media/pronunciations/en/${state.currentWord}-${type}.mp3`;
            const audio = new Audio(audioPath);
            audio.play().catch(error => console.error('پخش صدا با خطا مواجه شد:', error));
        }

        function playSlowPronunciation(word) {
            const utterance = new SpeechSynthesisUtterance(word);
            utterance.rate = 0.5; 
            window.speechSynthesis.speak(utterance);
        }

        function toggleFavorite() {
            const word = elements.wordTitle.textContent;
            if (state.favorites.includes(word)) {
                state.favorites = state.favorites.filter(w => w !== word);
            } else {
                state.favorites.push(word);
            }
            localStorage.setItem('favorites', JSON.stringify(state.favorites));
            updateFavoriteButton();
        }

        function updateFavoriteButton() {
            const word = elements.wordTitle.textContent;
            elements.favoriteBtn.classList.toggle('btn-outline-secondary', state.favorites.includes(word));
        }

        function showLoading(isLoading) {
            elements.loadingSpinner.style.display = isLoading ? 'block' : 'none';
            elements.resultCard.style.display = isLoading ? 'none' : 'block';
        }

        function hideError() {
            elements.errorMessage.style.display = 'none';
        }

        function showError(message) {
            elements.errorMessage.textContent = message;
            elements.errorMessage.style.display = 'block';
        }
        
        function loadNote() {
            const note = state.notes[state.currentWord] || '';
            elements.noteInput.value = note;
        }

        elements.saveNoteBtn.onclick = () => {
            state.notes[state.currentWord] = elements.noteInput.value;
            localStorage.setItem('notes', JSON.stringify(state.notes));
            alert('تێبینی پاشەکەوتکرا');
        };

        elements.favoriteBtn.onclick = toggleFavorite;

        elements.searchBtn.onclick = searchWord;
    </script>
</body>
</html>