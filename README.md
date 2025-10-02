<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title> Trivilocura </title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }

        body {
            background: linear-gradient(135deg, #6a11cb 0%, #2575fc 100%);
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            padding: 20px;
        }

        .container {
            background-color: white;
            border-radius: 15px;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.2);
            width: 100%;
            max-width: 900px;
            overflow: hidden;
        }

        .header {
            background: linear-gradient(to right, #4a00e0, #8e2de2);
            color: white;
            padding: 20px;
            text-align: center;
        }

        .header h1 {
            font-size: 1.8rem;
            margin-bottom: 10px;
        }

        .header p {
            font-size: 1rem;
            opacity: 0.9;
        }

        .timer-container {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 10px 20px;
            background-color: #f8f9fa;
            border-bottom: 1px solid #e9ecef;
        }

        .timer {
            font-size: 1.2rem;
            font-weight: bold;
            color: #dc3545;
            background-color: #fff;
            padding: 5px 15px;
            border-radius: 20px;
            box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
        }

        .progress {
            font-size: 1rem;
            color: #495057;
        }

        .category-selection {
            padding: 30px;
            text-align: center;
        }

        .category-title {
            font-size: 1.5rem;
            color: #343a40;
            margin-bottom: 20px;
        }

        .categories-container {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
            gap: 15px;
            margin-bottom: 30px;
        }

        .category-card {
            background-color: #f8f9fa;
            border: 2px solid #e9ecef;
            border-radius: 10px;
            padding: 15px;
            cursor: pointer;
            transition: all 0.3s ease;
            text-align: center;
        }

        .category-card:hover {
            transform: translateY(-5px);
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.1);
        }

        .category-card.selected {
            border-color: #4a00e0;
            background-color: #e8e2ff;
        }

        .category-icon {
            font-size: 2rem;
            margin-bottom: 10px;
        }

        .category-name {
            font-weight: 600;
            color: #343a40;
        }

        .quiz-container {
            padding: 30px;
        }

        .question-container {
            margin-bottom: 25px;
        }

        .question-number {
            font-size: 0.9rem;
            color: #6c757d;
            margin-bottom: 5px;
        }

        .question-text {
            font-size: 1.3rem;
            font-weight: 600;
            color: #343a40;
            margin-bottom: 20px;
            line-height: 1.4;
        }

        .question-image {
            width: 100%;
            max-height: 250px;
            object-fit: cover;
            border-radius: 10px;
            margin-bottom: 20px;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
        }

        .options-container {
            display: flex;
            flex-direction: column;
            gap: 12px;
        }

        .option {
            padding: 15px;
            background-color: #f8f9fa;
            border: 2px solid #e9ecef;
            border-radius: 10px;
            cursor: pointer;
            transition: all 0.3s ease;
            font-size: 1rem;
            display: flex;
            align-items: center;
        }

        .option:hover {
            background-color: #e9ecef;
            transform: translateY(-2px);
        }

        .option.selected {
            background-color: #4a00e0;
            color: white;
            border-color: #4a00e0;
        }

        .option-letter {
            display: inline-flex;
            justify-content: center;
            align-items: center;
            width: 30px;
            height: 30px;
            background-color: #e9ecef;
            border-radius: 50%;
            margin-right: 10px;
            font-weight: bold;
        }

        .option.selected .option-letter {
            background-color: rgba(255, 255, 255, 0.3);
        }

        .navigation {
            display: flex;
            justify-content: space-between;
            margin-top: 30px;
        }

        .btn {
            padding: 12px 25px;
            border: none;
            border-radius: 8px;
            font-size: 1rem;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.3s ease;
        }

        .btn-prev {
            background-color: #6c757d;
            color: white;
        }

        .btn-next {
            background-color: #4a00e0;
            color: white;
        }

        .btn-start {
            background-color: #4a00e0;
            color: white;
            padding: 15px 40px;
            font-size: 1.1rem;
        }

        .btn:hover {
            opacity: 0.9;
            transform: translateY(-2px);
        }

        .btn:disabled {
            background-color: #e9ecef;
            color: #adb5bd;
            cursor: not-allowed;
            transform: none;
        }

        .results-container {
            padding: 30px;
            text-align: center;
        }

        .results-title {
            font-size: 2rem;
            color: #4a00e0;
            margin-bottom: 20px;
        }

        .score {
            font-size: 3rem;
            font-weight: bold;
            color: #4a00e0;
            margin: 20px 0;
        }

        .results-summary {
            text-align: left;
            margin-top: 30px;
            background-color: #f8f9fa;
            padding: 20px;
            border-radius: 10px;
            max-height: 400px;
            overflow-y: auto;
        }

        .result-item {
            padding: 15px;
            border-bottom: 1px solid #e9ecef;
        }

        .result-item:last-child {
            border-bottom: none;
        }

        .result-question {
            font-weight: 600;
            margin-bottom: 8px;
        }

        .result-image {
            width: 100%;
            max-height: 150px;
            object-fit: cover;
            border-radius: 8px;
            margin: 10px 0;
        }

        .result-answer {
            display: flex;
            justify-content: space-between;
            margin-top: 5px;
        }

        .correct {
            color: #28a745;
        }

        .incorrect {
            color: #dc3545;
        }

        .btn-restart {
            background-color: #4a00e0;
            color: white;
            margin-top: 20px;
        }

        .hidden {
            display: none;
        }

        .category-tag {
            display: inline-block;
            background-color: #e9ecef;
            padding: 5px 10px;
            border-radius: 15px;
            font-size: 0.8rem;
            margin-bottom: 10px;
        }

        @media (max-width: 600px) {
            .header h1 {
                font-size: 1.5rem;
            }
            
            .quiz-container {
                padding: 20px;
            }
            
            .question-text {
                font-size: 1.1rem;
            }
            
            .btn {
                padding: 10px 20px;
            }
            
            .score {
                font-size: 2.5rem;
            }
            
            .result-answer {
                flex-direction: column;
                gap: 5px;
            }
            
            .categories-container {
                grid-template-columns: 1fr;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="header">
            <h1>Selecciona una categoría o elige preguntas mixtas</h1>

        </div>
        
        <!-- Pantalla de selección de categorías -->
        <div id="category-screen" class="category-selection">
            <h2 class="category-title">Elige una categoría para estudiar</h2>
            <div class="categories-container" id="categories-container">
                <!-- Las categorías se generarán con JavaScript -->
            </div>
            <button id="start-btn" class="btn btn-start" disabled>Comenzar Cuestionario</button>
        </div>
        
        <!-- Pantalla del cuestionario -->
        <div id="quiz-screen" class="quiz-container hidden">
            <div class="timer-container">
                <div class="progress">Pregunta <span id="current-question">1</span> de 10</div>
                <div class="timer">Tiempo: <span id="time">01:00</span></div>
            </div>
            
            <div class="question-container">
                <div class="question-number">Pregunta <span id="question-number">1</span></div>
                <div class="category-tag" id="question-category"></div>
                <div class="question-text" id="question-text"></div>
                <img class="question-image" id="question-image" src="" alt="Imagen de la pregunta">
            </div>
            
            <div class="options-container" id="options-container"></div>
            
            <div class="navigation">
                <button id="prev-btn" class="btn btn-prev" disabled>Anterior</button>
                <button id="next-btn" class="btn btn-next">Siguiente</button>
            </div>
        </div>
        
        <!-- Pantalla de resultados -->
        <div id="results-screen" class="results-container hidden">
            <h2 class="results-title">Resultados del Cuestionario</h2>
            <div class="score" id="final-score">0/10</div>
            <p id="result-message"></p>
            
            <div class="results-summary" id="results-summary"></div>
            
            <button id="restart-btn" class="btn btn-restart">Volver a Seleccionar Categorías</button>
        </div>
    </div>

    <script>
        // Definición de categorías disponibles
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

        // Generar 10 preguntas para cada categoría
        function generateQuestions() {
            return [
                // MATEMÁTICAS (10 preguntas)
                {
                    id: 1,
                    question: "¿Cuál es el resultado de 15 + 27?",
                    options: ["40", "42", "38", "45"],
                    correct: 1,
                    explanation: "15 + 27 = 42",
                    category: "matematicas",
                    image: "https://images.unsplash.com/photo-1635070041078-e363dbe005cb?ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60"
                },
                {
                    id: 2,
                    question: "¿Cuánto es 8 × 7?",
                    options: ["54", "56", "58", "60"],
                    correct: 1,
                    explanation: "8 × 7 = 56",
                    category: "matematicas",
                    image: "https://images.unsplash.com/photo-1509228468518-180dd4864904?ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60"
                },
                {
                    id: 3,
                    question: "¿Cuál es el valor de π (pi) aproximadamente?",
                    options: ["2.14", "3.14", "4.14", "3.41"],
                    correct: 1,
                    explanation: "π (pi) es aproximadamente 3.14159",
                    category: "matematicas",
                    image: "https://images.unsplash.com/photo-1528459801416-a9e53bbf4e17?ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60"
                },
                {
                    id: 4,
                    question: "¿Cuánto es 144 ÷ 12?",
                    options: ["10", "11", "12", "13"],
                    correct: 2,
                    explanation: "144 ÷ 12 = 12",
                    category: "matematicas",
                    image: "https://images.unsplash.com/photo-1596495577886-d920f1fb7238?ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60"
                },
                {
                    id: 5,
                    question: "¿Cuál es el área de un cuadrado de 5 cm de lado?",
                    options: ["20 cm²", "25 cm²", "30 cm²", "35 cm²"],
                    correct: 1,
                    explanation: "Área = lado × lado = 5 × 5 = 25 cm²",
                    category: "matematicas",
                    image: "https://images.unsplash.com/photo-1588666309990-d68f08e3d4a6?ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60"
                },
                {
                    id: 6,
                    question: "¿Qué porcentaje es 25 de 100?",
                    options: ["15%", "20%", "25%", "30%"],
                    correct: 2,
                    explanation: "25/100 = 0.25 = 25%",
                    category: "matematicas",
                    image: "https://images.unsplash.com/photo-1587440871875-191322ee64b0?ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60"
                },
                {
                    id: 7,
                    question: "¿Cuánto es 3² + 4²?",
                    options: ["12", "18", "24", "25"],
                    correct: 3,
                    explanation: "3² = 9, 4² = 16, 9 + 16 = 25",
                    category: "matematicas",
                    image: "https://images.unsplash.com/photo-1546833999-b9f581a1996d?ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60"
                },
                {
                    id: 8,
                    question: "¿Qué fracción es equivalente a 0.75?",
                    options: ["1/4", "1/2", "3/4", "4/5"],
                    correct: 2,
                    explanation: "0.75 = 75/100 = 3/4",
                    category: "matematicas",
                    image: "https://images.unsplash.com/photo-1509228468518-180dd4864904?ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60"
                },
                {
                    id: 9,
                    question: "¿Cuál es el MCD de 12 y 18?",
                    options: ["2", "3", "6", "9"],
                    correct: 2,
                    explanation: "Máximo Común Divisor de 12 y 18 es 6",
                    category: "matematicas",
                    image: "https://images.unsplash.com/photo-1635070041078-e363dbe005cb?ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60"
                },
                {
                    id: 10,
                    question: "¿Cuánto es 7 × 8 + 5?",
                    options: ["56", "61", "66", "71"],
                    correct: 1,
                    explanation: "7 × 8 = 56, 56 + 5 = 61",
                    category: "matematicas",
                    image: "https://images.unsplash.com/photo-1509228468518-180dd4864904?ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60"
                },

                // CIENCIAS (10 preguntas)
                {
                    id: 11,
                    question: "¿Qué planeta es conocido como el planeta rojo?",
                    options: ["Venus", "Júpiter", "Marte", "Saturno"],
                    correct: 2,
                    explanation: "Marte es conocido como el planeta rojo debido a su apariencia rojiza",
                    category: "ciencias",
                    image: "https://images.unsplash.com/photo-1614314107768-6018061b5b6e?ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60"
                },
                {
                    id: 12,
                    question: "¿Qué gas necesitan las plantas para realizar la fotosíntesis?",
                    options: ["Oxígeno", "Nitrógeno", "Dióxido de carbono", "Hidrógeno"],
                    correct: 2,
                    explanation: "Las plantas utilizan dióxido de carbono para la fotosíntesis",
                    category: "ciencias",
                    image: "https://images.unsplash.com/photo-1416879595882-3373a0480b5b?ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60"
                },
                {
                    id: 13,
                    question: "¿Cuál es el elemento químico más abundante en el universo?",
                    options: ["Oxígeno", "Carbono", "Hierro", "Hidrógeno"],
                    correct: 3,
                    explanation: "El hidrógeno es el elemento más abundante en el universo",
                    category: "ciencias",
                    image: "https://images.unsplash.com/photo-1532094349884-543bc11b234d?ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60"
                },
                {
                    id: 14,
                    question: "¿Qué partícula subatómica tiene carga positiva?",
                    options: ["Electrón", "Neutrón", "Protón", "Fotón"],
                    correct: 2,
                    explanation: "El protón tiene carga positiva",
                    category: "ciencias",
                    image: "https://images.unsplash.com/photo-1507146426996-ef05306b995a?ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60"
                },
                {
                    id: 15,
                    question: "¿Qué órgano bombea sangre en el cuerpo humano?",
                    options: ["Pulmón", "Hígado", "Corazón", "Cerebro"],
                    correct: 2,
                    explanation: "El corazón es el órgano que bombea sangre por todo el cuerpo",
                    category: "ciencias",
                    image: "https://images.unsplash.com/photo-1559757175-0eb30cd8c063?ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60"
                },
                {
                    id: 16,
                    question: "¿Qué planeta tiene anillos visibles?",
                    options: ["Marte", "Venus", "Saturno", "Mercurio"],
                    correct: 2,
                    explanation: "Saturno tiene anillos visibles desde la Tierra con telescopio",
                    category: "ciencias",
                    image: "https://images.unsplash.com/photo-1446776653964-20c1d3a81b06?ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60"
                },
                {
                    id: 17,
                    question: "¿Qué científico formuló la teoría de la relatividad?",
                    options: ["Newton", "Einstein", "Galileo", "Darwin"],
                    correct: 1,
                    explanation: "Albert Einstein formuló la teoría de la relatividad",
                    category: "ciencias",
                    image: "https://images.unsplash.com/photo-1635070041078-e363dbe005cb?ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60"
                },
                {
                    id: 18,
                    question: "¿Qué gas es esencial para la respiración humana?",
                    options: ["Nitrógeno", "Oxígeno", "Dióxido de carbono", "Hidrógeno"],
                    correct: 1,
                    explanation: "El oxígeno es esencial para la respiración humana",
                    category: "ciencias",
                    image: "https://images.unsplash.com/photo-1559757148-5c350d0d3c56?ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60"
                },
                {
                    id: 19,
                    question: "¿Qué planeta es el más cercano al Sol?",
                    options: ["Venus", "Mercurio", "Tierra", "Marte"],
                    correct: 1,
                    explanation: "Mercurio es el planeta más cercano al Sol",
                    category: "ciencias",
                    image: "https://images.unsplash.com/photo-1614314107768-6018061b5b6e?ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60"
                },
                {
                    id: 20,
                    question: "¿Qué tipo de animal es una ballena?",
                    options: ["Pez", "Anfibio", "Mamífero", "Reptil"],
                    correct: 2,
                    explanation: "La ballena es un mamífero marino",
                    category: "ciencias",
                    image: "https://images.unsplash.com/photo-1551966775-a4ddc8df052b?ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60"
                },

                // HISTORIA (10 preguntas)
                {
                    id: 21,
                    question: "¿En qué año llegó Colón a América?",
                    options: ["1492", "1502", "1482", "1512"],
                    correct: 0,
                    explanation: "Cristóbal Colón llegó a América en 1492",
                    category: "historia",
                    image: "https://images.unsplash.com/photo-1577985057588-882ec0b8c0b0?ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60"
                },
                {
                    id: 22,
                    question: "¿Quién pintó la Mona Lisa?",
                    options: ["Miguel Ángel", "Leonardo da Vinci", "Picasso", "Van Gogh"],
                    correct: 1,
                    explanation: "La Mona Lisa fue pintada por Leonardo da Vinci",
                    category: "historia",
                    image: "https://images.unsplash.com/photo-1541961017774-22349e4a1262?ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60"
                },
                {
                    id: 23,
                    question: "¿En qué año comenzó la Primera Guerra Mundial?",
                    options: ["1912", "1914", "1916", "1918"],
                    correct: 1,
                    explanation: "La Primera Guerra Mundial comenzó en 1914",
                    category: "historia",
                    image: "https://images.unsplash.com/photo-1589656043592-47d46f5982d6?ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60"
                },
                {
                    id: 24,
                    question: "¿Quién fue el primer presidente de Estados Unidos?",
                    options: ["Thomas Jefferson", "Abraham Lincoln", "George Washington", "John Adams"],
                    correct: 2,
                    explanation: "George Washington fue el primer presidente de Estados Unidos",
                    category: "historia",
                    image: "https://images.unsplash.com/photo-1565374397291-abf6075d6a0b?ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60"
                },
                {
                    id: 25,
                    question: "¿Qué civilización construyó las pirámides de Egipto?",
                    options: ["Romanos", "Griegos", "Egipcios", "Mayas"],
                    correct: 2,
                    explanation: "Los antiguos egipcios construyeron las pirámides",
                    category: "historia",
                    image: "https://images.unsplash.com/photo-1539650116574-75c0c6d73f6e?ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60"
                },
                {
                    id: 26,
                    question: "¿En qué año cayó el Imperio Romano de Occidente?",
                    options: ["376 d.C.", "476 d.C.", "576 d.C.", "676 d.C."],
                    correct: 1,
                    explanation: "El Imperio Romano de Occidente cayó en el año 476 d.C.",
                    category: "historia",
                    image: "https://images.unsplash.com/photo-1603561591411-07134e71a2a9?ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60"
                },
                {
                    id: 27,
                    question: "¿Quién escribió 'El Quijote'?",
                    options: ["Miguel de Cervantes", "Lope de Vega", "Calderón de la Barca", "Garcilaso de la Vega"],
                    correct: 0,
                    explanation: "Miguel de Cervantes escribió 'El Quijote'",
                    category: "historia",
                    image: "https://images.unsplash.com/photo-1512820790803-83ca734da794?ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60"
                },
                {
                    id: 28,
                    question: "¿Qué evento histórico ocurrió en 1789?",
                    options: ["Revolución Francesa", "Independencia de EE.UU.", "Revolución Industrial", "Descubrimiento de América"],
                    correct: 0,
                    explanation: "La Revolución Francesa comenzó en 1789",
                    category: "historia",
                    image: "https://images.unsplash.com/photo-1577985057588-882ec0b8c0b0?ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60"
                },
                {
                    id: 29,
                    question: "¿Quién fue el primer hombre en pisar la Luna?",
                    options: ["Neil Armstrong", "Buzz Aldrin", "Yuri Gagarin", "John Glenn"],
                    correct: 0,
                    explanation: "Neil Armstrong fue el primer hombre en pisar la Luna en 1969",
                    category: "historia",
                    image: "https://images.unsplash.com/photo-1446776877081-d282a0f896e2?ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60"
                },
                {
                    id: 30,
                    question: "¿En qué año terminó la Segunda Guerra Mundial?",
                    options: ["1943", "1944", "1945", "1946"],
                    correct: 2,
                    explanation: "La Segunda Guerra Mundial terminó en 1945",
                    category: "historia",
                    image: "https://images.unsplash.com/photo-1589656043592-47d46f5982d6?ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60"
                },

                // GEOGRAFÍA (10 preguntas)
                {
                    id: 31,
                    question: "¿Cuál es el río más largo del mundo?",
                    options: ["Nilo", "Amazonas", "Misisipi", "Yangtsé"],
                    correct: 1,
                    explanation: "El río Amazonas es el más largo del mundo con aproximadamente 7,062 km",
                    category: "geografia",
                    image: "https://images.unsplash.com/photo-1544551763-46a013bb70d5?ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60"
                },
                {
                    id: 32,
                    question: "¿Qué montaña es la más alta del mundo?",
                    options: ["K2", "Monte Everest", "Kilimanjaro", "Aconcagua"],
                    correct: 1,
                    explanation: "El Monte Everest es la montaña más alta del mundo con 8,848 metros",
                    category: "geografia",
                    image: "https://images.unsplash.com/photo-1464822759849-e41f5bc90477?ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60"
                },
                {
                    id: 33,
                    question: "¿Cuál es el país más grande del mundo por área?",
                    options: ["China", "Estados Unidos", "Canadá", "Rusia"],
                    correct: 3,
                    explanation: "Rusia es el país más grande del mundo con más de 17 millones de km²",
                    category: "geografia",
                    image: "https://images.unsplash.com/photo-1526772662000-3f88f10405ff?ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60"
                },
                {
                    id: 34,
                    question: "¿Qué océano es el más grande?",
                    options: ["Atlántico", "Índico", "Pacífico", "Ártico"],
                    correct: 2,
                    explanation: "El océano Pacífico es el más grande, cubriendo aproximadamente un tercio de la superficie terrestre",
                    category: "geografia",
                    image: "https://images.unsplash.com/photo-1559827260-dc66d52bef19?ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60"
                },
                {
                    id: 35,
                    question: "¿Cuál es la capital de Australia?",
                    options: ["Sídney", "Melbourne", "Canberra", "Brisbane"],
                    correct: 2,
                    explanation: "Canberra es la capital de Australia",
                    category: "geografia",
                    image: "https://images.unsplash.com/photo-1506905925346-21bda4d32df4?ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60"
                },
                {
                    id: 36,
                    question: "¿Qué desierto es el más grande del mundo?",
                    options: ["Sahara", "Gobi", "Kalahari", "Antártico"],
                    correct: 3,
                    explanation: "El desierto Antártico es el más grande del mundo",
                    category: "geografia",
                    image: "https://images.unsplash.com/photo-1416879595882-3373a0480b5b?ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60"
                },
                {
                    id: 37,
                    question: "¿Qué país tiene forma de bota?",
                    options: ["Grecia", "Italia", "España", "Francia"],
                    correct: 1,
                    explanation: "Italia tiene forma de bota",
                    category: "geografia",
                    image: "https://images.unsplash.com/photo-1515542622106-78bda8ba0e5b?ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60"
                },
                {
                    id: 38,
                    question: "¿Cuál es el país más poblado del mundo?",
                    options: ["India", "Estados Unidos", "China", "Indonesia"],
                    correct: 2,
                    explanation: "China es el país más poblado del mundo",
                    category: "geografia",
                    image: "https://images.unsplash.com/photo-1508804185872-d7badad00f7d?ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60"
                },
                {
                    id: 39,
                    question: "¿Qué montaña separa Europa de Asia?",
                    options: ["Alpes", "Himalaya", "Urales", "Andes"],
                    correct: 2,
                    explanation: "Los montes Urales separan Europa de Asia",
                    category: "geografia",
                    image: "https://images.unsplash.com/photo-1464822759849-e41f5bc90477?ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60"
                },
                {
                    id: 40,
                    question: "¿Cuál es la capital de Canadá?",
                    options: ["Toronto", "Vancouver", "Ottawa", "Montreal"],
                    correct: 2,
                    explanation: "Ottawa es la capital de Canadá",
                    category: "geografia",
                    image: "https://images.unsplash.com/photo-1517935706615-2717063c2225?ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60"
                },

                // LITERATURA (10 preguntas)
                {
                    id: 41,
                    question: "¿Quién escribió 'Cien años de soledad'?",
                    options: ["Jorge Luis Borges", "Pablo Neruda", "Gabriel García Márquez", "Mario Vargas Llosa"],
                    correct: 2,
                    explanation: "'Cien años de soledad' fue escrita por Gabriel García Márquez",
                    category: "literatura",
                    image: "https://images.unsplash.com/photo-1481627834876-b7833e8f5570?ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60"
                },
                {
                    id: 42,
                    question: "¿Qué obra comienza con 'En un lugar de la Mancha...'?",
                    options: ["El Lazarillo de Tormes", "La Celestina", "Don Quijote de la Mancha", "Fuenteovejuna"],
                    correct: 2,
                    explanation: "Don Quijote de la Mancha comienza con esas palabras",
                    category: "literatura",
                    image: "https://images.unsplash.com/photo-1512820790803-83ca734da794?ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60"
                },
                {
                    id: 43,
                    question: "¿Quién escribió 'Romeo y Julieta'?",
                    options: ["Charles Dickens", "William Shakespeare", "Jane Austen", "Mark Twain"],
                    correct: 1,
                    explanation: "'Romeo y Julieta' fue escrita por William Shakespeare",
                    category: "literatura",
                    image: "https://images.unsplash.com/photo-1544716278-ca5e3f4abd8c?ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60"
                },
                {
                    id: 44,
                    question: "¿Qué autor escribió '1984'?",
                    options: ["Aldous Huxley", "George Orwell", "Ray Bradbury", "H.G. Wells"],
                    correct: 1,
                    explanation: "'1984' fue escrita por George Orwell",
                    category: "literatura",
                    image: "https://images.unsplash.com/photo-1507003211169-0a1dd7228f2d?ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60"
                },
                {
                    id: 45,
                    question: "¿Quién escribió 'La Odisea'?",
                    options: ["Sófocles", "Homero", "Virgilio", "Esquilo"],
                    correct: 1,
                    explanation: "'La Odisea' fue escrita por Homero",
                    category: "literatura",
                    image: "https://images.unsplash.com/photo-1481627834876-b7833e8f5570?ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60"
                },
                {
                    id: 46,
                    question: "¿Qué escritor creó el personaje de Sherlock Holmes?",
                    options: ["Agatha Christie", "Arthur Conan Doyle", "Edgar Allan Poe", "Charles Dickens"],
                    correct: 1,
                    explanation: "Arthur Conan Doyle creó a Sherlock Holmes",
                    category: "literatura",
                    image: "https://images.unsplash.com/photo-1544716278-ca5e3f4abd8c?ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60"
                },
                {
                    id: 47,
                    question: "¿Quién escribió 'Orgullo y prejuicio'?",
                    options: ["Charlotte Brontë", "Jane Austen", "Emily Brontë", "Virginia Woolf"],
                    correct: 1,
                    explanation: "'Orgullo y prejuicio' fue escrita por Jane Austen",
                    category: "literatura",
                    image: "https://images.unsplash.com/photo-1481627834876-b7833e8f5570?ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60"
                },
                {
                    id: 48,
                    question: "¿Qué poeta chileno ganó el Premio Nobel de Literatura?",
                    options: ["Jorge Luis Borges", "Octavio Paz", "Pablo Neruda", "Gabriela Mistral"],
                    correct: 2,
                    explanation: "Pablo Neruda ganó el Premio Nobel de Literatura en 1971",
                    category: "literatura",
                    image: "https://images.unsplash.com/photo-1507003211169-0a1dd7228f2d?ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60"
                },
                {
                    id: 49,
                    question: "¿Quién escribió 'El principito'?",
                    options: ["Jules Verne", "Antoine de Saint-Exupéry", "Victor Hugo", "Albert Camus"],
                    correct: 1,
                    explanation: "'El principito' fue escrito por Antoine de Saint-Exupéry",
                    category: "literatura",
                    image: "https://images.unsplash.com/photo-1544716278-ca5e3f4abd8c?ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60"
                },
                {
                    id: 50,
                    question: "¿Qué autor escribió 'Crimen y castigo'?",
                    options: ["León Tolstói", "Fiódor Dostoyevski", "Antón Chéjov", "Nikolái Gógol"],
                    correct: 1,
                    explanation: "'Crimen y castigo' fue escrita por Fiódor Dostoyevski",
                    category: "literatura",
                    image: "https://images.unsplash.com/photo-1481627834876-b7833e8f5570?ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60"
                },

                // ARTE (10 preguntas)
                {
                    id: 51,
                    question: "¿Quién pintó 'La noche estrellada'?",
                    options: ["Pablo Picasso", "Claude Monet", "Vincent van Gogh", "Salvador Dalí"],
                    correct: 2,
                    explanation: "'La noche estrellada' fue pintada por Vincent van Gogh",
                    category: "arte",
                    image: "https://images.unsplash.com/photo-1578301978693-85fa9c0320b9?ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60"
                },
                {
                    id: 52,
                    question: "¿Qué estilo artístico se caracteriza por formas geométricas y colores planos?",
                    options: ["Impresionismo", "Cubismo", "Surrealismo", "Expresionismo"],
                    correct: 1,
                    explanation: "El cubismo se caracteriza por formas geométricas y colores planos",
                    category: "arte",
                    image: "https://images.unsplash.com/photo-1541961017774-22349e4a1262?ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60"
                },
                {
                    id: 53,
                    question: "¿Quién esculpió 'El David'?",
                    options: ["Donatello", "Miguel Ángel", "Leonardo da Vinci", "Bernini"],
                    correct: 1,
                    explanation: "'El David' fue esculpido por Miguel Ángel",
                    category: "arte",
                    image: "https://images.unsplash.com/photo-1595435934249-5df7ed86e1c0?ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60"
                },
                {
                    id: 54,
                    question: "¿Qué artista es conocido por sus obras de arte pop como 'Latas de sopa Campbell'?",
                    options: ["Andy Warhol", "Roy Lichtenstein", "Keith Haring", "Jackson Pollock"],
                    correct: 0,
                    explanation: "Andy Warhol es conocido por sus obras de arte pop como 'Latas de sopa Campbell'",
                    category: "arte",
                    image: "https://images.unsplash.com/photo-1578303512596-44d7e896c8e7?ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60"
                },
                {
                    id: 55,
                    question: "¿Quién pintó 'El grito'?",
                    options: ["Vincent van Gogh", "Edvard Munch", "Pablo Picasso", "Salvador Dalí"],
                    correct: 1,
                    explanation: "'El grito' fue pintado por Edvard Munch",
                    category: "arte",
                    image: "https://images.unsplash.com/photo-1578301978693-85fa9c0320b9?ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60"
                },
                {
                    id: 56,
                    question: "¿Qué artista español es conocido por su periodo azul y rosa?",
                    options: ["Salvador Dalí", "Pablo Picasso", "Joan Miró", "Diego Velázquez"],
                    correct: 1,
                    explanation: "Pablo Picasso es conocido por sus periodos azul y rosa",
                    category: "arte",
                    image: "https://images.unsplash.com/photo-1541961017774-22349e4a1262?ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60"
                },
                {
                    id: 57,
                    question: "¿Qué pintor impresionista pintó 'Nenúfares'?",
                    options: ["Claude Monet", "Pierre-Auguste Renoir", "Edgar Degas", "Paul Cézanne"],
                    correct: 0,
                    explanation: "Claude Monet pintó la serie 'Nenúfares'",
                    category: "arte",
                    image: "https://images.unsplash.com/photo-1578301978693-85fa9c0320b9?ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60"
                },
                {
                    id: 58,
                    question: "¿Qué artista pintó 'La última cena'?",
                    options: ["Miguel Ángel", "Rafael", "Leonardo da Vinci", "Caravaggio"],
                    correct: 2,
                    explanation: "'La última cena' fue pintada por Leonardo da Vinci",
                    category: "arte",
                    image: "https://images.unsplash.com/photo-1541961017774-22349e4a1262?ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60"
                },
                {
                    id: 59,
                    question: "¿Qué movimiento artístico se caracteriza por representar sueños y el subconsciente?",
                    options: ["Cubismo", "Surrealismo", "Expresionismo", "Dadaísmo"],
                    correct: 1,
                    explanation: "El surrealismo se caracteriza por representar sueños y el subconsciente",
                    category: "arte",
                    image: "https://images.unsplash.com/photo-1578301978693-85fa9c0320b9?ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60"
                },
                {
                    id: 60,
                    question: "¿Quién es el autor de 'Las meninas'?",
                    options: ["Francisco de Goya", "Diego Velázquez", "El Greco", "Bartolomé Esteban Murillo"],
                    correct: 1,
                    explanation: "'Las meninas' fue pintada por Diego Velázquez",
                    category: "arte",
                    image: "https://images.unsplash.com/photo-1541961017774-22349e4a1262?ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60"
                },

                // DEPORTES (10 preguntas)
                {
                    id: 61,
                    question: "¿En qué deporte se utiliza un bate y una pelota?",
                    options: ["Fútbol", "Béisbol", "Baloncesto", "Tenis"],
                    correct: 1,
                    explanation: "En el béisbol se utiliza un bate para golpear la pelota",
                    category: "deportes",
                    image: "https://images.unsplash.com/photo-1549638441-b787d2e11f14?ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60"
                },
                {
                    id: 62,
                    question: "¿Cuántos jugadores hay en un equipo de fútbol en el campo?",
                    options: ["9", "10", "11", "12"],
                    correct: 2,
                    explanation: "Un equipo de fútbol tiene 11 jugadores en el campo",
                    category: "deportes",
                    image: "https://images.unsplash.com/photo-1575361204480-aadea25e6e68?ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60"
                },
                {
                    id: 63,
                    question: "¿En qué deporte se anotan 'canastas'?",
                    options: ["Fútbol", "Baloncesto", "Tenis", "Voleibol"],
                    correct: 1,
                    explanation: "En el baloncesto se anotan canastas",
                    category: "deportes",
                    image: "https://images.unsplash.com/photo-1546519638-68e109498ffc?ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60"
                },
                {
                    id: 64,
                    question: "¿Qué país ha ganado más Copas del Mundo de fútbol?",
                    options: ["Alemania", "Italia", "Brasil", "Argentina"],
                    correct: 2,
                    explanation: "Brasil ha ganado 5 Copas del Mundo de fútbol",
                    category: "deportes",
                    image: "https://images.unsplash.com/photo-1599058917212-d750089bc07e?ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60"
                },
                {
                    id: 65,
                    question: "¿En qué deporte se usa una raqueta y una pelota amarilla?",
                    options: ["Bádminton", "Tenis", "Ping pong", "Squash"],
                    correct: 1,
                    explanation: "En el tenis se usa una raqueta y una pelota amarilla",
                    category: "deportes",
                    image: "https://images.unsplash.com/photo-1595435934249-5df7ed86e1c0?ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60"
                },
                {
                    id: 66,
                    question: "¿Cuántos jugadores hay en un equipo de baloncesto en la cancha?",
                    options: ["4", "5", "6", "7"],
                    correct: 1,
                    explanation: "En baloncesto hay 5 jugadores por equipo en la cancha",
                    category: "deportes",
                    image: "https://images.unsplash.com/photo-1546519638-68e109498ffc?ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60"
                },
                {
                    id: 67,
                    question: "¿Qué deporte practica Tiger Woods?",
                    options: ["Tenis", "Golf", "Fútbol", "Béisbol"],
                    correct: 1,
                    explanation: "Tiger Woods es un famoso golfista",
                    category: "deportes",
                    image: "https://images.unsplash.com/photo-1575361204480-aadea25e6e68?ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60"
                },
                {
                    id: 68,
                    question: "¿En qué deporte se nada en diferentes estilos como mariposa y espalda?",
                    options: ["Natación", "Waterpolo", "Buceo", "Esquí acuático"],
                    correct: 0,
                    explanation: "En natación se compite en diferentes estilos",
                    category: "deportes",
                    image: "https://images.unsplash.com/photo-1544551763-46a013bb70d5?ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60"
                },
                {
                    id: 69,
                    question: "¿Qué país organizó los Juegos Olímpicos de 2016?",
                    options: ["China", "Reino Unido", "Brasil", "Rusia"],
                    correct: 2,
                    explanation: "Brasil organizó los Juegos Olímpicos de 2016 en Río de Janeiro",
                    category: "deportes",
                    image: "https://images.unsplash.com/photo-1599058917212-d750089bc07e?ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60"
                },
                {
                    id: 70,
                    question: "¿En qué deporte se lanza un disco y una jabalina?",
                    options: ["Atletismo", "Gimnasia", "Halterofilia", "Ciclismo"],
                    correct: 0,
                    explanation: "En atletismo se lanzan disco y jabalina",
                    category: "deportes",
                    image: "https://images.unsplash.com/photo-1549638441-b787d2e11f14?ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60"
                },

                // TECNOLOGÍA (10 preguntas)
                {
                    id: 71,
                    question: "¿Qué compañía creó el iPhone?",
                    options: ["Samsung", "Microsoft", "Apple", "Google"],
                    correct: 2,
                    explanation: "Apple creó el iPhone",
                    category: "tecnologia",
                    image: "https://images.unsplash.com/photo-1511707171634-5f897ff02aa9?ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60"
                },
                {
                    id: 72,
                    question: "¿Qué significa HTML?",
                    options: ["HyperText Markup Language", "HighTech Modern Language", "HyperTransfer Machine Learning", "Home Tool Markup Language"],
                    correct: 0,
                    explanation: "HTML significa HyperText Markup Language",
                    category: "tecnologia",
                    image: "https://images.unsplash.com/photo-1542831371-29b0f74f9713?ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60"
                },
                {
                    id: 73,
                    question: "¿Qué compañía es dueña de Android?",
                    options: ["Apple", "Microsoft", "Google", "Samsung"],
                    correct: 2,
                    explanation: "Google es dueño del sistema operativo Android",
                    category: "tecnologia",
                    image: "https://images.unsplash.com/photo-1517077304055-6e89abbf09b0?ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60"
                },
                {
                    id: 74,
                    question: "¿Qué significa 'URL'?",
                    options: ["Universal Resource Locator", "Uniform Resource Locator", "Universal Reference Link", "Uniform Reference Link"],
                    correct: 1,
                    explanation: "URL significa Uniform Resource Locator",
                    category: "tecnologia",
                    image: "https://images.unsplash.com/photo-1551288049-bebda4e38f71?ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60"
                },
                {
                    id: 75,
                    question: "¿Qué empresa fundó Mark Zuckerberg?",
                    options: ["Twitter", "Facebook", "Instagram", "WhatsApp"],
                    correct: 1,
                    explanation: "Mark Zuckerberg fundó Facebook",
                    category: "tecnologia",
                    image: "https://images.unsplash.com/photo-1511707171634-5f897ff02aa9?ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60"
                },
                {
                    id: 76,
                    question: "¿Qué significa 'Wi-Fi'?",
                    options: ["Wireless Fidelity", "Wide Fidelity", "Wireless Frequency", "Wide Frequency"],
                    correct: 0,
                    explanation: "Wi-Fi significa Wireless Fidelity",
                    category: "tecnologia",
                    image: "https://images.unsplash.com/photo-1542831371-29b0f74f9713?ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60"
                },
                {
                    id: 77,
                    question: "¿Qué compañía desarrolló el sistema operativo Windows?",
                    options: ["Apple", "Microsoft", "Google", "IBM"],
                    correct: 1,
                    explanation: "Microsoft desarrolló Windows",
                    category: "tecnologia",
                    image: "https://images.unsplash.com/photo-1517077304055-6e89abbf09b0?ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60"
                },
                {
                    id: 78,
                    question: "¿Qué significa 'CPU'?",
                    options: ["Central Processing Unit", "Computer Processing Unit", "Central Program Unit", "Computer Program Unit"],
                    correct: 0,
                    explanation: "CPU significa Central Processing Unit",
                    category: "tecnologia",
                    image: "https://images.unsplash.com/photo-1551288049-bebda4e38f71?ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60"
                },
                {
                    id: 79,
                    question: "¿Qué navegador web desarrolló Google?",
                    options: ["Firefox", "Safari", "Chrome", "Edge"],
                    correct: 2,
                    explanation: "Google desarrolló Chrome",
                    category: "tecnologia",
                    image: "https://images.unsplash.com/photo-1511707171634-5f897ff02aa9?ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60"
                },
                {
                    id: 80,
                    question: "¿Qué empresa creó el PlayStation?",
                    options: ["Microsoft", "Nintendo", "Sony", "Sega"],
                    correct: 2,
                    explanation: "Sony creó PlayStation",
                    category: "tecnologia",
                    image: "https://images.unsplash.com/photo-1542831371-29b0f74f9713?ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60"
                }
            ];
        }

        // Variables globales
        const allQuestions = generateQuestions();
        let currentQuestions = [];
        let currentQuestionIndex = 0;
        let userAnswers = [];
        let timer;
        let timeLeft = 60; // 1 minuto en segundos
        let selectedCategory = null;

        // Elementos DOM
        const categoryScreen = document.getElementById('category-screen');
        const quizScreen = document.getElementById('quiz-screen');
        const resultsScreen = document.getElementById('results-screen');
        const categoriesContainer = document.getElementById('categories-container');
        const startBtn = document.getElementById('start-btn');
        const questionText = document.getElementById('question-text');
        const questionImage = document.getElementById('question-image');
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

        // Inicializar la aplicación
        function initApp() {
            renderCategories();
            setupEventListeners();
        }

        // Renderizar las categorías en la pantalla de selección
        function renderCategories() {
            categoriesContainer.innerHTML = '';
            
            categories.forEach(category => {
                const categoryCard = document.createElement('div');
                categoryCard.classList.add('category-card');
                categoryCard.dataset.id = category.id;
                
                categoryCard.innerHTML = `
                    <div class="category-icon">${category.icon}</div>
                    <div class="category-name">${category.name}</div>
                `;
                
                categoryCard.addEventListener('click', () => selectCategory(category.id));
                categoriesContainer.appendChild(categoryCard);
            });
        }

        // Seleccionar categoría
        function selectCategory(categoryId) {
            // Deseleccionar todas las categorías
            document.querySelectorAll('.category-card').forEach(card => {
                card.classList.remove('selected');
            });
            
            // Seleccionar la categoría clickeada
            const categoryCard = document.querySelector(`.category-card[data-id="${categoryId}"]`);
            categoryCard.classList.add('selected');
            
            selectedCategory = categoryId;
            startBtn.disabled = false;
        }

        // Configurar event listeners
        function setupEventListeners() {
            startBtn.addEventListener('click', startQuiz);
            prevBtn.addEventListener('click', prevQuestion);
            nextBtn.addEventListener('click', nextQuestion);
            restartBtn.addEventListener('click', restartQuiz);
        }

        // Iniciar el cuestionario
        function startQuiz() {
            // Obtener preguntas según la categoría seleccionada
            if (selectedCategory === 'mixtas') {
                // Para preguntas mixtas, seleccionar de todas las categorías
                currentQuestions = getRandomQuestions(allQuestions, 10);
            } else {
                // Para categorías específicas, obtener solo preguntas de esa categoría
                const questionsFromCategory = allQuestions.filter(question => 
                    question.category === selectedCategory
                );
                currentQuestions = getRandomQuestions(questionsFromCategory, 10);
            }
            
            currentQuestionIndex = 0;
            userAnswers = Array(10).fill(null);
            
            // Iniciar temporizador
            startTimer();
            
            // Mostrar primera pregunta
            showQuestion();
            
            // Cambiar a pantalla de cuestionario
            categoryScreen.classList.add('hidden');
            quizScreen.classList.remove('hidden');
            resultsScreen.classList.add('hidden');
        }

        // Obtener preguntas aleatorias
        function getRandomQuestions(questions, count) {
            if (questions.length <= count) return questions;
            
            const shuffled = [...questions].sort(() => 0.5 - Math.random());
            return shuffled.slice(0, count);
        }

        // Mostrar pregunta actual
        function showQuestion() {
            const question = currentQuestions[currentQuestionIndex];
            const categoryInfo = categories.find(cat => cat.id === question.category);
            
            questionText.textContent = question.question;
            questionNumber.textContent = currentQuestionIndex + 1;
            currentQuestionSpan.textContent = currentQuestionIndex + 1;
            
            // Mostrar categoría
            questionCategory.textContent = categoryInfo.name;
            questionCategory.style.backgroundColor = categoryInfo.color;
            questionCategory.style.color = 'white';
            
            // Mostrar imagen
            questionImage.src = question.image;
            questionImage.alt = `Imagen para pregunta sobre ${categoryInfo.name}`;
            
            // Limpiar opciones anteriores
            optionsContainer.innerHTML = '';
            
            // Agregar nuevas opciones
            question.options.forEach((option, index) => {
                const optionElement = document.createElement('div');
                optionElement.classList.add('option');
                
                if (userAnswers[currentQuestionIndex] === index) {
                    optionElement.classList.add('selected');
                }
                
                const optionLetter = document.createElement('span');
                optionLetter.classList.add('option-letter');
                optionLetter.textContent = String.fromCharCode(65 + index);
                
                const optionText = document.createElement('span');
                optionText.textContent = option;
                
                optionElement.appendChild(optionLetter);
                optionElement.appendChild(optionText);
                optionElement.addEventListener('click', () => selectOption(index));
                
                optionsContainer.appendChild(optionElement);
            });
            
            // Actualizar botones de navegación
            prevBtn.disabled = currentQuestionIndex === 0;
            
            if (currentQuestionIndex === 9) {
                nextBtn.textContent = 'Finalizar';
            } else {
                nextBtn.textContent = 'Siguiente';
            }
        }

        // Seleccionar una opción
        function selectOption(optionIndex) {
            userAnswers[currentQuestionIndex] = optionIndex;
            showQuestion();
        }

        // Navegar a la pregunta anterior
        function prevQuestion() {
            if (currentQuestionIndex > 0) {
                currentQuestionIndex--;
                showQuestion();
            }
        }

        // Navegar a la siguiente pregunta o finalizar
        function nextQuestion() {
            if (currentQuestionIndex < 9) {
                currentQuestionIndex++;
                showQuestion();
            } else {
                finishQuiz();
            }
        }

        // Iniciar temporizador
        function startTimer() {
            clearInterval(timer);
            timeLeft = 60;
            updateTimerDisplay();
            
            timer = setInterval(() => {
                timeLeft--;
                updateTimerDisplay();
                
                if (timeLeft <= 0) {
                    clearInterval(timer);
                    finishQuiz();
                }
            }, 1000);
        }

        // Actualizar display del temporizador
        function updateTimerDisplay() {
            const minutes = Math.floor(timeLeft / 60);
            const seconds = timeLeft % 60;
            timeDisplay.textContent = `${minutes.toString().padStart(2, '0')}:${seconds.toString().padStart(2, '0')}`;
            
            // Cambiar color cuando quede poco tiempo
            if (timeLeft <= 10) {
                timeDisplay.style.color = '#dc3545';
            }
        }

        // Finalizar cuestionario
        function finishQuiz() {
            clearInterval(timer);
            
            // Calcular puntuación
            let score = 0;
            currentQuestions.forEach((question, index) => {
                if (userAnswers[index] === question.correct) {
                    score++;
                }
            });
            
            // Mostrar resultados
            finalScore.textContent = `${score}/10`;
            
            // Mensaje según la puntuación
            if (score >= 9) {
                resultMessage.textContent = "¡Excelente! Has demostrado un gran conocimiento.";
            } else if (score >= 7) {
                resultMessage.textContent = "¡Buen trabajo! Tienes un buen nivel de conocimiento.";
            } else if (score >= 5) {
                resultMessage.textContent = "Resultado aceptable. Sigue practicando para mejorar.";
            } else {
                resultMessage.textContent = "Necesitas repasar más. ¡No te rindas!";
            }
            
            // Mostrar resumen de respuestas
            resultsSummary.innerHTML = '';
            currentQuestions.forEach((question, index) => {
                const resultItem = document.createElement('div');
                resultItem.classList.add('result-item');
                
                const isCorrect = userAnswers[index] === question.correct;
                const answerClass = isCorrect ? 'correct' : 'incorrect';
                const userAnswerText = userAnswers[index] !== null ? 
                    `${String.fromCharCode(65 + userAnswers[index])}. ${question.options[userAnswers[index]]}` : 
                    'Sin responder';
                const correctAnswerText = `${String.fromCharCode(65 + question.correct)}. ${question.options[question.correct]}`;
                const categoryInfo = categories.find(cat => cat.id === question.category);
                
                resultItem.innerHTML = `
                    <div class="result-question">${index + 1}. ${question.question}</div>
                    <div class="category-tag" style="background-color: ${categoryInfo.color}; color: white;">${categoryInfo.name}</div>
                    <img class="result-image" src="${question.image}" alt="Imagen de la pregunta">
                    <div class="result-answer">
                        <span>Tu respuesta: <span class="${answerClass}">${userAnswerText}</span></span>
                        <span>Respuesta correcta: <span class="correct">${correctAnswerText}</span></span>
                    </div>
                    <div><small>${question.explanation}</small></div>
                `;
                
                resultsSummary.appendChild(resultItem);
            });
            
            // Cambiar a pantalla de resultados
            quizScreen.classList.add('hidden');
            resultsScreen.classList.remove('hidden');
        }

        // Reiniciar cuestionario
        function restartQuiz() {
            // Limpiar selección
            selectedCategory = null;
            document.querySelectorAll('.category-card').forEach(card => {
                card.classList.remove('selected');
            });
            startBtn.disabled = true;
            
            // Volver a pantalla de selección de categorías
            categoryScreen.classList.remove('hidden');
            quizScreen.classList.add('hidden');
            resultsScreen.classList.add('hidden');
        }

        // Iniciar la aplicación
        window.onload = initApp;
    </script>
</body>
</html>
