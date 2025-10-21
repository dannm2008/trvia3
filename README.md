<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="utf-8" />
<meta name="viewport" content="width=device-width,initial-scale=1" />
<title>💖 TriviLocura 💖</title>
<style>
    /* Reset */
    *{box-sizing:border-box;margin:0;padding:0;font-family:'Segoe UI',Tahoma,Geneva,Verdana,sans-serif}

    /* Animated rainbow background */
    :root{
        --card-bg: rgba(255,255,255,0.95);
    }
    body{
        min-height:100vh;
        display:flex;
        align-items:center;
        justify-content:center;
        padding:20px;
        background: linear-gradient(120deg,#ff9a9e 0%, #fecfef 10%, #f6d365 20%, #fda085 30%, #a1c4fd 45%, #c2e9fb 55%, #d4fc79 70%, #96e6a1 85%, #fbc2eb 100%);
        background-size: 400% 400%;
        animation: rainbow 18s linear infinite;
    }
    @keyframes rainbow{
        0%{background-position:0% 50%}
        50%{background-position:100% 50%}
        100%{background-position:0% 50%}
    }

    /* Container */
    .container{
        width:100%;
        max-width:980px;
        background: var(--card-bg);
        border-radius:16px;
        box-shadow:0 15px 40px rgba(0,0,0,0.18);
        overflow:hidden;
        position:relative;
    }

    /* Header */
    .header{
        padding:18px 22px;
        text-align:center;
        background: linear-gradient(90deg, rgba(255,255,255,0.06), rgba(255,255,255,0));
        border-bottom: 1px solid rgba(0,0,0,0.06);
    }
    .title{
        font-size:1.9rem;
        font-weight:800;
        letter-spacing:0.6px;
        display:flex;
        justify-content:center;
        align-items:center;
        gap:10px;
    }
    .title .heart{
        color:#ff5c9e;
        font-size:1.3rem;
        transform:translateY(-2px);
    }
    .subtitle{ color:#666; margin-top:6px; font-size:0.95rem; opacity:0.95 }

    /* Timer / progress */
    .timer-container{
        display:flex;
        justify-content:space-between;
        align-items:center;
        padding:12px 20px;
        background:linear-gradient(to right, rgba(255,255,255,0.6), rgba(255,255,255,0.4));
        border-bottom:1px solid rgba(0,0,0,0.04);
    }
    .timer{ font-weight:700; color:#d6336c; background:#fff; padding:6px 12px;border-radius:20px; box-shadow:0 2px 6px rgba(0,0,0,0.06)}
    .progress{ font-weight:600; color:#333 }

    /* Selection screen */
    .category-selection{ padding:26px; text-align:center }
    .category-title{ font-size:1.4rem; font-weight:700; margin-bottom:16px; color:#222 }
    .categories-container{ display:grid; gap:12px; grid-template-columns:repeat(auto-fit,minmax(160px,1fr)); margin:14px 0 22px }
    .category-card{
        background:linear-gradient(180deg,rgba(255,255,255,0.7),rgba(255,255,255,0.5));
        padding:14px;border-radius:12px;border:2px solid rgba(0,0,0,0.04);
        cursor:pointer;transition:transform .18s ease, box-shadow .18s ease;
        display:flex;flex-direction:column;align-items:center;gap:8px;
        min-height:84px;justify-content:center;
    }
    .category-card:hover{ transform:translateY(-6px); box-shadow:0 10px 25px rgba(0,0,0,0.08) }
    .category-card.selected{ outline:3px solid rgba(0,0,0,0.06); transform:translateY(-2px); }
    .category-icon{ font-size:1.6rem }
    .category-name{ font-weight:700 }

    /* Quiz screen */
    .quiz-container{ padding:22px 26px 30px }
    .question-container{ margin-bottom:18px }
    .question-number{ color:#6c757d; margin-bottom:6px }
    .question-text{ font-size:1.25rem; font-weight:700; color:#222; line-height:1.4; margin-bottom:10px }
    .category-tag{ display:inline-block; padding:6px 10px; border-radius:999px; font-weight:700; color:#fff; margin-bottom:10px }

    .options-container{ display:flex; flex-direction:column; gap:12px; margin-top:10px }
    .option{
        display:flex;align-items:center;gap:12px;padding:12px;border-radius:10px;border:2px solid rgba(0,0,0,0.06);
        background:linear-gradient(180deg, #fff, #f8f9fb); cursor:pointer; transition:transform .12s ease, box-shadow .12s ease;
    }
    .option:hover{ transform:translateY(-4px); box-shadow:0 8px 20px rgba(0,0,0,0.06) }
    .option.selected{ background: linear-gradient(90deg,#6a11cb,#2575fc); color:#fff; border-color:transparent }
    .option-letter{ width:34px;height:34px;border-radius:50%;display:inline-flex;align-items:center;justify-content:center;font-weight:800;background:#eef2ff }
    .option.selected .option-letter{ background: rgba(255,255,255,0.25) }

    /* Navigation buttons */
    .navigation{ display:flex; justify-content:space-between; gap:8px; margin-top:18px }
    .btn{ padding:12px 20px;border-radius:10px;border:none;font-weight:800; cursor:pointer; box-shadow:0 6px 18px rgba(0,0,0,0.06) }
    .btn:disabled{ opacity:0.5; cursor:not-allowed; transform:none; box-shadow:none }
    .btn-prev{ background:#adb5bd; color:#fff }
    .btn-next{ background: linear-gradient(90deg,#4a00e0,#8e2de2); color:#fff }
    .btn-start{ background: linear-gradient(90deg,#ff7eb3,#ff758c); color:#fff; padding:14px 28px; font-size:1.05rem }

    /* Result screen */
    .results-container{ padding:22px }
    .results-title{ font-size:1.6rem; color:#6a11cb; font-weight:800; text-align:center }
    .score{ font-size:2.4rem; font-weight:900; color:#4a00e0; text-align:center; margin:10px 0 6px }
    .results-summary{ margin-top:18px; background:#fff; padding:16px; border-radius:10px; max-height:360px; overflow:auto; border:1px solid rgba(0,0,0,0.04) }
    .result-item{ padding:12px;border-bottom:1px dashed rgba(0,0,0,0.04) }
    .result-question{ font-weight:800; margin-bottom:6px }
    .correct{ color:#28a745; font-weight:800 }
    .incorrect{ color:#dc3545; font-weight:800 }

    /* Feedback overlay */
    .feedback{
        position: absolute;
        left:50%;
        transform:translateX(-50%);
        top:26%;
        z-index:60;
        min-width:260px;
        max-width:80%;
        text-align:center;
        padding:14px 18px;
        border-radius:12px;
        display:none;
        align-items:center;
        gap:10px;
        box-shadow:0 14px 40px rgba(0,0,0,0.18);
        font-weight:900;
        font-size:1.05rem;
    }
    .feedback.show{ display:flex; animation:pop .32s ease both }
    @keyframes pop{ from{ transform:translateX(-50%) scale(0.8); opacity:0 } to{ transform:translateX(-50%) scale(1); opacity:1 } }

    .feedback.correct{ background: linear-gradient(90deg,#e9ffea,#d6ffe0); color:#1f7a3a }
    .feedback.incorrect{ background: linear-gradient(90deg,#ffe7e7,#ffdcdc); color:#8a1f2b }

    /* Confetti canvas covers whole container */
    #confetti-canvas{ position:absolute; inset:0; pointer-events:none; z-index:50 }

    /* Shake animation for incorrect */
    .shake{ animation:shake .45s ease both }
    @keyframes shake{
        10%,90%{ transform:translateX(-1px) }
        20%,80%{ transform:translateX(2px) }
        30%,50%,70%{ transform:translateX(-4px) }
        40%,60%{ transform:translateX(4px) }
    }

    /* Mobile tweaks */
    @media(max-width:640px){
        .title{ font-size:1.4rem }
        .question-text{ font-size:1.05rem }
        .btn{ padding:10px 14px }
    }
</style>
</head>
<body>
<div class="container" id="app">
    <canvas id="confetti-canvas"></canvas>

    <div class="header">
        <div class="title">
            <span class="heart">💗</span>
            <span>TriviLocura</span>
            <span class="heart">💗</span>
        </div>
        <div class="subtitle">Elige una categoría y demuestra lo que sabes — ¡diviértete! 🎉</div>
    </div>

    <!-- Timer / progress -->
    <div class="timer-container">
        <div class="progress">Pregunta <span id="current-question">1</span> de 10</div>
        <div class="timer">Tiempo: <span id="time">01:00</span></div>
    </div>

    <!-- Category selection -->
    <div id="category-screen" class="category-selection">
        <h2 class="category-title">💖 Elige una categoría para estudiar</h2>
        <div class="categories-container" id="categories-container"></div>
        <button id="start-btn" class="btn btn-start" disabled>Comenzar Cuestionario</button>
    </div>

    <!-- Quiz screen -->
    <div id="quiz-screen" class="quiz-container hidden" style="display:none">
        <div class="question-container">
            <div class="question-number">Pregunta <span id="question-number">1</span></div>
            <div class="category-tag" id="question-category"></div>
            <div class="question-text" id="question-text"></div>
        </div>

        <div id="feedback" class="feedback" role="status" aria-live="polite"></div>

        <div class="options-container" id="options-container"></div>

        <div class="navigation">
            <button id="prev-btn" class="btn btn-prev" disabled>Anterior</button>
            <button id="next-btn" class="btn btn-next">Siguiente</button>
        </div>
    </div>

    <!-- Results screen -->
    <div id="results-screen" class="results-container hidden" style="display:none">
        <h2 class="results-title">Resultados del Cuestionario</h2>
        <div class="score" id="final-score">0/10</div>
        <p id="result-message" style="text-align:center"></p>
        <div class="results-summary" id="results-summary"></div>
        <div style="text-align:center; margin-top:14px;">
            <button id="restart-btn" class="btn btn-start">Volver a Seleccionar Categorías</button>
        </div>
    </div>
</div>

<script>
/* -------------------------
   Datos de categorías y preguntas (sin imágenes)
   ------------------------- */
const categories = [
    { id: 'matematicas', name: 'Matemáticas', color: '#FF6B6B', icon: '∑' },
    { id: 'ciencias', name: 'Ciencias', color: '#4ECDC4', icon: '🔬' },
    { id: 'historia', name: 'Historia', color: '#FFD166', icon: '📜' },
    { id: 'geografia', name: 'Geografía', color: '#06D6A0', icon: '🌎' },
    { id: 'literatura', name: 'Literatura', color: '#118AB2', icon: '📚' },
    { id: 'arte', name: 'Arte', color: '#073B4C', icon: '🎨' },
    { id: 'deportes', name: 'Deportes', color: '#EF476F', icon: '⚽' },
    { id: 'tecnologia', name: 'Tecnología', color: '#7209B7', icon: '💻' },
    { id: 'mixtas', name: 'Preguntas Mixtas', color: '#FF9E64', icon: '🎲' }
];

function generateQuestions(){
    return [
        // MATEMÁTICAS (10)
        { id:1, question:"¿Cuál es el resultado de 15 + 27?", options:["40","42","38","45"], correct:1, explanation:"15 + 27 = 42", category:"matematicas" },
        { id:2, question:"¿Cuánto es 8 × 7?", options:["54","56","58","60"], correct:1, explanation:"8 × 7 = 56", category:"matematicas" },
        { id:3, question:"¿Cuál es el valor de π (pi) aproximadamente?", options:["2.14","3.14","4.14","3.41"], correct:1, explanation:"π ≈ 3.14159", category:"matematicas" },
        { id:4, question:"¿Cuánto es 144 ÷ 12?", options:["10","11","12","13"], correct:2, explanation:"144 ÷ 12 = 12", category:"matematicas" },
        { id:5, question:"¿Cuál es el área de un cuadrado de 5 cm de lado?", options:["20 cm²","25 cm²","30 cm²","35 cm²"], correct:1, explanation:"Área = 5 × 5 = 25 cm²", category:"matematicas" },
        { id:6, question:"¿Qué porcentaje es 25 de 100?", options:["15%","20%","25%","30%"], correct:2, explanation:"25/100 = 25%", category:"matematicas" },
        { id:7, question:"¿Cuánto es 3² + 4²?", options:["12","18","24","25"], correct:3, explanation:"9 + 16 = 25", category:"matematicas" },
        { id:8, question:"¿Qué fracción es equivalente a 0.75?", options:["1/4","1/2","3/4","4/5"], correct:2, explanation:"0.75 = 3/4", category:"matematicas" },
        { id:9, question:"¿Cuál es el MCD de 12 y 18?", options:["2","3","6","9"], correct:2, explanation:"MCD(12,18) = 6", category:"matematicas" },
        { id:10, question:"¿Cuánto es 7 × 8 + 5?", options:["56","61","66","71"], correct:1, explanation:"7×8=56; 56+5=61", category:"matematicas" },

        // CIENCIAS (10)
        { id:11, question:"¿Qué planeta es conocido como el planeta rojo?", options:["Venus","Júpiter","Marte","Saturno"], correct:2, explanation:"Marte es el planeta rojo", category:"ciencias" },
        { id:12, question:"¿Qué gas necesitan las plantas para realizar la fotosíntesis?", options:["Oxígeno","Nitrógeno","Dióxido de carbono","Hidrógeno"], correct:2, explanation:"Las plantas usan dióxido de carbono", category:"ciencias" },
        { id:13, question:"¿Cuál es el elemento químico más abundante en el universo?", options:["Oxígeno","Carbono","Hierro","Hidrógeno"], correct:3, explanation:"El hidrógeno es el más abundante", category:"ciencias" },
        { id:14, question:"¿Qué partícula subatómica tiene carga positiva?", options:["Electrón","Neutrón","Protón","Fotón"], correct:2, explanation:"El protón tiene carga positiva", category:"ciencias" },
        { id:15, question:"¿Qué órgano bombea sangre en el cuerpo humano?", options:["Pulmón","Hígado","Corazón","Cerebro"], correct:2, explanation:"El corazón bombea la sangre", category:"ciencias" },
        { id:16, question:"¿Qué planeta tiene anillos visibles?", options:["Marte","Venus","Saturno","Mercurio"], correct:2, explanation:"Saturno tiene anillos visibles", category:"ciencias" },
        { id:17, question:"¿Qué científico formuló la teoría de la relatividad?", options:["Newton","Einstein","Galileo","Darwin"], correct:1, explanation:"Albert Einstein", category:"ciencias" },
        { id:18, question:"¿Qué gas es esencial para la respiración humana?", options:["Nitrógeno","Oxígeno","Dióxido de carbono","Hidrógeno"], correct:1, explanation:"El oxígeno es esencial", category:"ciencias" },
        { id:19, question:"¿Qué planeta es el más cercano al Sol?", options:["Venus","Mercurio","Tierra","Marte"], correct:1, explanation:"Mercurio es el más cercano", category:"ciencias" },
        { id:20, question:"¿Qué tipo de animal es una ballena?", options:["Pez","Anfibio","Mamífero","Reptil"], correct:2, explanation:"La ballena es un mamífero", category:"ciencias" },

        // HISTORIA (10)
        { id:21, question:"¿En qué año llegó Colón a América?", options:["1492","1502","1482","1512"], correct:0, explanation:"Cristóbal Colón llegó en 1492", category:"historia" },
        { id:22, question:"¿Quién pintó la Mona Lisa?", options:["Miguel Ángel","Leonardo da Vinci","Picasso","Van Gogh"], correct:1, explanation:"Leonardo da Vinci", category:"historia" },
        { id:23, question:"¿En qué año comenzó la Primera Guerra Mundial?", options:["1912","1914","1916","1918"], correct:1, explanation:"Comenzó en 1914", category:"historia" },
        { id:24, question:"¿Quién fue el primer presidente de Estados Unidos?", options:["Thomas Jefferson","Abraham Lincoln","George Washington","John Adams"], correct:2, explanation:"George Washington", category:"historia" },
        { id:25, question:"¿Qué civilización construyó las pirámides de Egipto?", options:["Romanos","Griegos","Egipcios","Mayas"], correct:2, explanation:"Los egipcios", category:"historia" },
        { id:26, question:"¿En qué año cayó el Imperio Romano de Occidente?", options:["376 d.C.","476 d.C.","576 d.C.","676 d.C."], correct:1, explanation:"Cayó en 476 d.C.", category:"historia" },
        { id:27, question:"¿Quién escribió 'El Quijote'?", options:["Miguel de Cervantes","Lope de Vega","Calderón de la Barca","Garcilaso de la Vega"], correct:0, explanation:"Miguel de Cervantes", category:"historia" },
        { id:28, question:"¿Qué evento histórico ocurrió en 1789?", options:["Revolución Francesa","Independencia de EE.UU.","Revolución Industrial","Descubrimiento de América"], correct:0, explanation:"Revolución Francesa", category:"historia" },
        { id:29, question:"¿Quién fue el primer hombre en pisar la Luna?", options:["Neil Armstrong","Buzz Aldrin","Yuri Gagarin","John Glenn"], correct:0, explanation:"Neil Armstrong en 1969", category:"historia" },
        { id:30, question:"¿En qué año terminó la Segunda Guerra Mundial?", options:["1943","1944","1945","1946"], correct:2, explanation:"Terminó en 1945", category:"historia" },

        // GEOGRAFÍA (10)
        { id:31, question:"¿Cuál es el río más largo del mundo?", options:["Nilo","Amazonas","Misisipi","Yangtsé"], correct:1, explanation:"Amazonas (aprox. 7,062 km)", category:"geografia" },
        { id:32, question:"¿Qué montaña es la más alta del mundo?", options:["K2","Monte Everest","Kilimanjaro","Aconcagua"], correct:1, explanation:"Monte Everest (≈8,848 m)", category:"geografia" },
        { id:33, question:"¿Cuál es el país más grande del mundo por área?", options:["China","Estados Unidos","Canadá","Rusia"], correct:3, explanation:"Rusia (≈17 millones km²)", category:"geografia" },
        { id:34, question:"¿Qué océano es el más grande?", options:["Atlántico","Índico","Pacífico","Ártico"], correct:2, explanation:"Océano Pacífico", category:"geografia" },
        { id:35, question:"¿Cuál es la capital de Australia?", options:["Sídney","Melbourne","Canberra","Brisbane"], correct:2, explanation:"Canberra", category:"geografia" },
        { id:36, question:"¿Qué desierto es el más grande del mundo?", options:["Sahara","Gobi","Kalahari","Antártico"], correct:3, explanation:"El desierto Antártico es el más grande", category:"geografia" },
        { id:37, question:"¿Qué país tiene forma de bota?", options:["Grecia","Italia","España","Francia"], correct:1, explanation:"Italia", category:"geografia" },
        { id:38, question:"¿Cuál es el país más poblado del mundo?", options:["India","Estados Unidos","China","Indonesia"], correct:2, explanation:"China", category:"geografia" },
        { id:39, question:"¿Qué montaña separa Europa de Asia?", options:["Alpes","Himalaya","Urales","Andes"], correct:2, explanation:"Montes Urales", category:"geografia" },
        { id:40, question:"¿Cuál es la capital de Canadá?", options:["Toronto","Vancouver","Ottawa","Montreal"], correct:2, explanation:"Ottawa", category:"geografia" },

        // LITERATURA (10)
        { id:41, question:"¿Quién escribió 'Cien años de soledad'?", options:["Jorge Luis Borges","Pablo Neruda","Gabriel García Márquez","Mario Vargas Llosa"], correct:2, explanation:"Gabriel García Márquez", category:"literatura" },
        { id:42, question:"¿Qué obra comienza con 'En un lugar de la Mancha...'?", options:["El Lazarillo de Tormes","La Celestina","Don Quijote de la Mancha","Fuenteovejuna"], correct:2, explanation:"Don Quijote de la Mancha", category:"literatura" },
        { id:43, question:"¿Quién escribió 'Romeo y Julieta'?", options:["Charles Dickens","William Shakespeare","Jane Austen","Mark Twain"], correct:1, explanation:"William Shakespeare", category:"literatura" },
        { id:44, question:"¿Qué autor escribió '1984'?", options:["Aldous Huxley","George Orwell","Ray Bradbury","H.G. Wells"], correct:1, explanation:"George Orwell", category:"literatura" },
        { id:45, question:"¿Quién escribió 'La Odisea'?", options:["Sófocles","Homero","Virgilio","Esquilo"], correct:1, explanation:"Homero", category:"literatura" },
        { id:46, question:"¿Qué escritor creó el personaje de Sherlock Holmes?", options:["Agatha Christie","Arthur Conan Doyle","Edgar Allan Poe","Charles Dickens"], correct:1, explanation:"Arthur Conan Doyle", category:"literatura" },
        { id:47, question:"¿Quién escribió 'Orgullo y prejuicio'?", options:["Charlotte Brontë","Jane Austen","Emily Brontë","Virginia Woolf"], correct:1, explanation:"Jane Austen", category:"literatura" },
        { id:48, question:"¿Qué poeta chileno ganó el Premio Nobel de Literatura?", options:["Jorge Luis Borges","Octavio Paz","Pablo Neruda","Gabriela Mistral"], correct:2, explanation:"Pablo Neruda (1971)", category:"literatura" },
        { id:49, question:"¿Quién escribió 'El principito'?", options:["Jules Verne","Antoine de Saint-Exupéry","Victor Hugo","Albert Camus"], correct:1, explanation:"Antoine de Saint-Exupéry", category:"literatura" },
        { id:50, question:"¿Qué autor escribió 'Crimen y castigo'?", options:["León Tolstói","Fiódor Dostoyevski","Antón Chéjov","Nikolái Gógol"], correct:1, explanation:"Fiódor Dostoyevski", category:"literatura" },

        // ARTE (10)
        { id:51, question:"¿Quién pintó 'La noche estrellada'?", options:["Pablo Picasso","Claude Monet","Vincent van Gogh","Salvador Dalí"], correct:2, explanation:"Vincent van Gogh", category:"arte" },
        { id:52, question:"¿Qué estilo artístico se caracteriza por formas geométricas y colores planos?", options:["Impresionismo","Cubismo","Surrealismo","Expresionismo"], correct:1, explanation:"Cubismo", category:"arte" },
        { id:53, question:"¿Quién esculpió 'El David'?", options:["Donatello","Miguel Ángel","Leonardo da Vinci","Bernini"], correct:1, explanation:"Miguel Ángel", category:"arte" },
        { id:54, question:"¿Qué artista es conocido por sus obras de arte pop como 'Latas de sopa Campbell'?", options:["Andy Warhol","Roy Lichtenstein","Keith Haring","Jackson Pollock"], correct:0, explanation:"Andy Warhol", category:"arte" },
        { id:55, question:"¿Quién pintó 'El grito'?", options:["Vincent van Gogh","Edvard Munch","Pablo Picasso","Salvador Dalí"], correct:1, explanation:"Edvard Munch", category:"arte" },
        { id:56, question:"¿Qué artista español es conocido por su periodo azul y rosa?", options:["Salvador Dalí","Pablo Picasso","Joan Miró","Diego Velázquez"], correct:1, explanation:"Pablo Picasso", category:"arte" },
        { id:57, question:"¿Qué pintor impresionista pintó 'Nenúfares'?", options:["Claude Monet","Pierre-Auguste Renoir","Edgar Degas","Paul Cézanne"], correct:0, explanation:"Claude Monet", category:"arte" },
        { id:58, question:"¿Qué artista pintó 'La última cena'?", options:["Miguel Ángel","Rafael","Leonardo da Vinci","Caravaggio"], correct:2, explanation:"Leonardo da Vinci", category:"arte" },
        { id:59, question:"¿Qué movimiento artístico se caracteriza por representar sueños y el subconsciente?", options:["Cubismo","Surrealismo","Expresionismo","Dadaísmo"], correct:1, explanation:"Surrealismo", category:"arte" },
        { id:60, question:"¿Quién es el autor de 'Las meninas'?", options:["Francisco de Goya","Diego Velázquez","El Greco","Bartolomé Esteban Murillo"], correct:1, explanation:"Diego Velázquez", category:"arte" },

        // DEPORTES (10)
        { id:61, question:"¿En qué deporte se utiliza un bate y una pelota?", options:["Fútbol","Béisbol","Baloncesto","Tenis"], correct:1, explanation:"Béisbol", category:"deportes" },
        { id:62, question:"¿Cuántos jugadores hay en un equipo de fútbol en el campo?", options:["9","10","11","12"], correct:2, explanation:"11 jugadores", category:"deportes" },
        { id:63, question:"¿En qué deporte se anotan 'canastas'?", options:["Fútbol","Baloncesto","Tenis","Voleibol"], correct:1, explanation:"Baloncesto", category:"deportes" },
        { id:64, question:"¿Qué país ha ganado más Copas del Mundo de fútbol?", options:["Alemania","Italia","Brasil","Argentina"], correct:2, explanation:"Brasil (5)", category:"deportes" },
        { id:65, question:"¿En qué deporte se usa una raqueta y una pelota amarilla?", options:["Bádminton","Tenis","Ping pong","Squash"], correct:1, explanation:"Tenis", category:"deportes" },
        { id:66, question:"¿Cuántos jugadores hay en un equipo de baloncesto en la cancha?", options:["4","5","6","7"], correct:1, explanation:"5 jugadores", category:"deportes" },
        { id:67, question:"¿Qué deporte practica Tiger Woods?", options:["Tenis","Golf","Fútbol","Béisbol"], correct:1, explanation:"Golf", category:"deportes" },
        { id:68, question:"¿En qué deporte se nada en diferentes estilos como mariposa y espalda?", options:["Natación","Waterpolo","Buceo","Esquí acuático"], correct:0, explanation:"Natación", category:"deportes" },
        { id:69, question:"¿Qué país organizó los Juegos Olímpicos de 2016?", options:["China","Reino Unido","Brasil","Rusia"], correct:2, explanation:"Brasil (Río de Janeiro)", category:"deportes" },
        { id:70, question:"¿En qué deporte se lanza un disco y una jabalina?", options:["Atletismo","Gimnasia","Halterofilia","Ciclismo"], correct:0, explanation:"Atletismo", category:"deportes" },

        // TECNOLOGÍA (10)
        { id:71, question:"¿Qué compañía creó el iPhone?", options:["Samsung","Microsoft","Apple","Google"], correct:2, explanation:"Apple", category:"tecnologia" },
        { id:72, question:"¿Qué significa HTML?", options:["HyperText Markup Language","HighTech Modern Language","HyperTransfer Machine Learning","Home Tool Markup Language"], correct:0, explanation:"HyperText Markup Language", category:"tecnologia" },
        { id:73, question:"¿Qué compañía es dueña de Android?", options:["Apple","Microsoft","Google","Samsung"], correct:2, explanation:"Google", category:"tecnologia" },
        { id:74, question:"¿Qué significa 'URL'?", options:["Universal Resource Locator","Uniform Resource Locator","Universal Reference Link","Uniform Reference Link"], correct:1, explanation:"Uniform Resource Locator", category:"tecnologia" },
        { id:75, question:"¿Qué empresa fundó Mark Zuckerberg?", options:["Twitter","Facebook","Instagram","WhatsApp"], correct:1, explanation:"Facebook", category:"tecnologia" },
        { id:76, question:"¿Qué significa 'Wi-Fi'?", options:["Wireless Fidelity","Wide Fidelity","Wireless Frequency","Wide Frequency"], correct:0, explanation:"Wireless Fidelity", category:"tecnologia" },
        { id:77, question:"¿Qué compañía desarrolló el sistema operativo Windows?", options:["Apple","Microsoft","Google","IBM"], correct:1, explanation:"Microsoft", category:"tecnologia" },
        { id:78, question:"¿Qué significa 'CPU'?", options:["Central Processing Unit","Computer Processing Unit","Central Program Unit","Computer Program Unit"], correct:0, explanation:"Central Processing Unit", category:"tecnologia" },
        { id:79, question:"¿Qué navegador web desarrolló Google?", options:["Firefox","Safari","Chrome","Edge"], correct:2, explanation:"Chrome", category:"tecnologia" },
        { id:80, question:"¿Qué empresa creó el PlayStation?", options:["Microsoft","Nintendo","Sony","Sega"], correct:2, explanation:"Sony", category:"tecnologia" }
    ];
}

/* -------------------------
   Estado y elementos DOM
   ------------------------- */
const allQuestions = generateQuestions();
let currentQuestions = [];
let currentQuestionIndex = 0;
let userAnswers = [];
let timer, timeLeft = 60;
let selectedCategory = null;

/* DOM */
const categoryScreen = document.getElementById('category-screen');
const quizScreen = document.getElementById('quiz-screen');
const resultsScreen = document.getElementById('results-screen');
const categoriesContainer = document.getElementById('categories-container');
const startBtn = document.getElementById('start-btn');
const questionText = document.getElementById('question-text');
const questionCategory = document.getElementById('question-category');
const optionsContainer = document.getElementById('options-container');
const prevBtn = document.getElementById('prev-btn');
const nextBtn = document.getElementById('next-btn');
const questionNumber = document.getElementById('question-number');
const currentQuestionSpan = document.getElementById('current-question');
const timeDisplay = document.getElementById('time');
const finalScore = document.getElementById('final-score');
const resultMessage = document.getElementById('result-message');
const resultsSummary = document.getElementById('results-summary');
const restartBtn = document.getElementById('restart-btn');
const feedbackDiv = document.getElementById('feedback');
const confettiCanvas = document.getElementById('confetti-canvas');
const app = document.getElementById('app');

/* -------------------------
   Inicializar app
   ------------------------- */
function initApp(){
    renderCategories();
    setupEventListeners();
}
window.onload = initApp;

/* -------------------------
   Render categorías
   ------------------------- */
function renderCategories(){
    categoriesContainer.innerHTML = '';
    categories.forEach(cat=>{
        const card = document.createElement('div');
        card.className = 'category-card';
        card.dataset.id = cat.id;
        card.innerHTML = `<div class="category-icon">${cat.icon}</div><div class="category-name">${cat.name}</div>`;
        card.addEventListener('click', ()=> selectCategory(cat.id, card));
        categoriesContainer.appendChild(card);
    });
}

function selectCategory(categoryId, cardEl){
    document.querySelectorAll('.category-card').forEach(c=>c.classList.remove('selected'));
    cardEl.classList.add('selected');
    selectedCategory = categoryId;
    startBtn.disabled = false;
}

/* -------------------------
   Event listeners
   ------------------------- */
function setupEventListeners(){
    startBtn.addEventListener('click', startQuiz);
    prevBtn.addEventListener('click', prevQuestion);
    nextBtn.addEventListener('click', nextQuestion);
    restartBtn.addEventListener('click', restartQuiz);
}

/* -------------------------
   Iniciar cuestionario
   ------------------------- */
function startQuiz(){
    if(selectedCategory === 'mixtas'){
        currentQuestions = getRandomQuestions(allQuestions, 10);
    } else {
        const pool = allQuestions.filter(q=> q.category === selectedCategory);
        currentQuestions = getRandomQuestions(pool, 10);
    }
    currentQuestionIndex = 0;
    userAnswers = Array(10).fill(null);
    startTimer();
    showQuestion();
    categoryScreen.style.display = 'none';
    quizScreen.style.display = 'block';
    resultsScreen.style.display = 'none';
}

/* -------------------------
   Random questions
   ------------------------- */
function getRandomQuestions(questions, count){
    if(questions.length <= count) return [...questions];
    return [...questions].sort(()=>0.5 - Math.random()).slice(0,count);
}

/* -------------------------
   Mostrar pregunta
   ------------------------- */
function showQuestion(){
    const q = currentQuestions[currentQuestionIndex];
    const catInfo = categories.find(c=> c.id === q.category) || {name:'', color:'#888'};

    questionText.textContent = q.question;
    questionNumber.textContent = currentQuestionIndex + 1;
    currentQuestionSpan.textContent = currentQuestionIndex + 1;

    questionCategory.textContent = catInfo.name;
    questionCategory.style.backgroundColor = catInfo.color;
    questionCategory.style.color = '#fff';

    // opciones
    optionsContainer.innerHTML = '';
    q.options.forEach((opt, idx)=>{
        const el = document.createElement('div');
        el.className = 'option';
        if(userAnswers[currentQuestionIndex] === idx) el.classList.add('selected');

        const letter = document.createElement('div');
        letter.className = 'option-letter';
        letter.textContent = String.fromCharCode(65 + idx);

        const text = document.createElement('div');
        text.textContent = opt;

        el.appendChild(letter);
        el.appendChild(text);

        el.addEventListener('click', ()=> selectOption(idx));
        optionsContainer.appendChild(el);
    });

    prevBtn.disabled = currentQuestionIndex === 0;
    nextBtn.textContent = currentQuestionIndex === 9 ? 'Finalizar' : 'Siguiente';
}

/* -------------------------
   Seleccionar opción (feedback inmediato)
   ------------------------- */
function selectOption(optionIndex){
    const q = currentQuestions[currentQuestionIndex];

    // Guardar respuesta
    userAnswers[currentQuestionIndex] = optionIndex;

    // Marcar seleccionado visualmente
    // (re-render opciones)
    showQuestion();

    // Mostrar feedback inmediato
    if(optionIndex === q.correct){
        showFeedbackCorrect();
    } else {
        showFeedbackIncorrect();
    }
}

/* -------------------------
   Feedback: Correcto (confeti + cohete)
   ------------------------- */
function showFeedbackCorrect(){
    // texto
    feedbackDiv.className = 'feedback correct show';
    feedbackDiv.innerHTML = `✅ ¡Correcto! <span style="margin-left:8px">🎉🚀</span>`;

    // confetti por toda la pantalla
    confettiBurst(80);

    // ocultar después
    setTimeout(()=>{ feedbackDiv.classList.remove('show'); }, 1600);
}

/* -------------------------
   Feedback: Incorrecto (X roja + carita triste + vibración)
   ------------------------- */
function showFeedbackIncorrect(){
    feedbackDiv.className = 'feedback incorrect show';
    feedbackDiv.innerHTML = `❌ Incorrecto <span style="margin-left:8px">😢</span>`;

    // efecto de temblor en contenedor de opciones
    optionsContainer.classList.add('shake');
    setTimeout(()=>{ optionsContainer.classList.remove('shake'); }, 480);

    // vibrar si el dispositivo lo permite
    if(window.navigator && navigator.vibrate){
        navigator.vibrate([80,40,80]);
    }

    setTimeout(()=>{ feedbackDiv.classList.remove('show'); }, 1400);
}

/* -------------------------
   Navegación preguntas
   ------------------------- */
function prevQuestion(){ if(currentQuestionIndex > 0){ currentQuestionIndex--; showQuestion(); } }
function nextQuestion(){ if(currentQuestionIndex < 9){ currentQuestionIndex++; showQuestion(); } else { finishQuiz(); } }

/* -------------------------
   Temporizador
   ------------------------- */
function startTimer(){
    clearInterval(timer);
    timeLeft = 60;
    updateTimerDisplay();
    timer = setInterval(()=>{
        timeLeft--;
        updateTimerDisplay();
        if(timeLeft <= 0){ clearInterval(timer); finishQuiz(); }
    },1000);
}
function updateTimerDisplay(){
    const m = Math.floor(timeLeft/60);
    const s = timeLeft%60;
    timeDisplay.textContent = `${String(m).padStart(2,'0')}:${String(s).padStart(2,'0')}`;
    if(timeLeft <= 10){ timeDisplay.style.color = '#dc3545'; } else { timeDisplay.style.color = ''; }
}

/* -------------------------
   Finalizar y mostrar resultados
   ------------------------- */
function finishQuiz(){
    clearInterval(timer);
    let score = 0;
    currentQuestions.forEach((q,i)=>{ if(userAnswers[i] === q.correct) score++; });

    finalScore.textContent = `${score}/10`;
    if(score >= 9) resultMessage.textContent = "¡Excelente! Has demostrado un gran conocimiento.";
    else if(score >= 7) resultMessage.textContent = "¡Buen trabajo! Tienes un buen nivel de conocimiento.";
    else if(score >= 5) resultMessage.textContent = "Resultado aceptable. Sigue practicando para mejorar.";
    else resultMessage.textContent = "Necesitas repasar más. ¡No te rindas!";

    // Resumen
    resultsSummary.innerHTML = '';
    currentQuestions.forEach((q,i)=>{
        const isCorrect = userAnswers[i] === q.correct;
        const userAnsText = userAnswers[i] !== null ? `${String.fromCharCode(65+userAnswers[i])}. ${q.options[userAnswers[i]]}` : 'Sin responder';
        const correctText = `${String.fromCharCode(65+q.correct)}. ${q.options[q.correct]}`;
        const catInfo = categories.find(c=> c.id === q.category) || {color:'#999', name:q.category};

        const item = document.createElement('div');
        item.className = 'result-item';
        item.innerHTML = `
            <div style="display:flex;justify-content:space-between;align-items:center;gap:10px;">
                <div style="min-width:60%"><div class="result-question">${i+1}. ${q.question}</div>
                <div style="margin-top:6px;"><span class="category-tag" style="background:${catInfo.color};color:#fff;padding:6px 10px;border-radius:999px;font-weight:700">${catInfo.name}</span></div></div>
                <div style="text-align:right;min-width:30%">
                    <div style="font-weight:900; font-size:1.05rem; ${isCorrect ? 'color:#28a745' : 'color:#dc3545'}">
                        ${isCorrect ? '✅ Correcto 😁' : '❌ Incorrecto 😞'}
                    </div>
                </div>
            </div>
            <div style="margin-top:8px; display:flex; justify-content:space-between; gap:10px; flex-wrap:wrap;">
                <div>Tu respuesta: <strong class="${isCorrect ? 'correct' : 'incorrect'}">${userAnsText}</strong></div>
                <div>Respuesta correcta: <strong class="correct">${correctText}</strong></div>
            </div>
            <div style="margin-top:8px;"><small>${q.explanation}</small></div>
        `;
        resultsSummary.appendChild(item);
    });

    // Cambiar pantallas
    quizScreen.style.display = 'none';
    resultsScreen.style.display = 'block';
}

/* -------------------------
   Reiniciar
   ------------------------- */
function restartQuiz(){
    selectedCategory = null;
    document.querySelectorAll('.category-card').forEach(c=>c.classList.remove('selected'));
    startBtn.disabled = true;
    categoryScreen.style.display = 'block';
    quizScreen.style.display = 'none';
    resultsScreen.style.display = 'none';
}

/* -------------------------
   Confetti system (canvas particles)
   ------------------------- */
(function setupConfetti(){
    const ctx = confettiCanvas.getContext('2d');
    let W = confettiCanvas.width = app.clientWidth;
    let H = confettiCanvas.height = app.clientHeight;
    const particles = [];
    let animating = false;

    // Resize canvas with container
    function resize(){
        W = confettiCanvas.width = app.clientWidth;
        H = confettiCanvas.height = app.clientHeight;
    }
    window.addEventListener('resize', resize);

    // Colors for confetti
    const COLORS = ['#ff5c9e','#ffd166','#4ecdc4','#7209b7','#ff9e64','#4a00e0','#2575fc','#ffd6e0'];

    function random(min, max){ return Math.random()*(max-min)+min; }

    // Create burst
    window.confettiBurst = function(count=60){
        for(let i=0;i<count;i++){
            particles.push({
                x: random(0, W),
                y: random(-20, H/3),
                w: random(6,12),
                h: random(8,14),
                vx: random(-3.5,3.5),
                vy: random(1,5),
                angle: random(0, Math.PI*2),
                angularVel: random(-0.15,0.15),
                color: COLORS[Math.floor(Math.random()*COLORS.length)],
                ttl: random(80,160),
                gravity: random(0.02,0.12),
                drag: 0.995
            });
        }
        if(!animating){ animating = true; requestAnimationFrame(update); }
    };

    // Animation loop
    function update(){
        ctx.clearRect(0,0,W,H);
        for(let i=particles.length-1;i>=0;i--){
            const p = particles[i];
            p.vy += p.gravity;
            p.vx *= p.drag;
            p.vy *= p.drag;
            p.x += p.vx;
            p.y += p.vy;
            p.angle += p.angularVel;
            p.ttl--;

            ctx.save();
            ctx.translate(p.x, p.y);
            ctx.rotate(p.angle);
            ctx.fillStyle = p.color;
            ctx.fillRect(-p.w/2, -p.h/2, p.w, p.h);
            ctx.restore();

            if(p.y > H + 40 || p.ttl <= 0) particles.splice(i,1);
        }

        if(particles.length>0){ requestAnimationFrame(update); } else { animating = false; ctx.clearRect(0,0,W,H); }
    }
})();

/* -------------------------
   Fin del script
   ------------------------- */
</script>
</body>
</html>
