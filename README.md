<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Vocabulary Game: English Expressions Part 4</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #8e44ad 0%, #3498db 100%);
            min-height: 100vh;
            padding: 20px;
            color: #333;
        }

        .container {
            max-width: 1000px;
            margin: 0 auto;
            background: white;
            border-radius: 20px;
            box-shadow: 0 15px 35px rgba(0,0,0,0.2);
            overflow: hidden;
        }

        .header {
            background: linear-gradient(135deg, #8e44ad, #3498db);
            color: white;
            padding: 30px;
            text-align: center;
            position: relative;
        }

        .header::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background: url('data:image/svg+xml,<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 100 100"><circle cx="20" cy="20" r="2" fill="rgba(255,255,255,0.1)"/><circle cx="80" cy="30" r="1.5" fill="rgba(255,255,255,0.1)"/><circle cx="40" cy="70" r="1" fill="rgba(255,255,255,0.1)"/><circle cx="90" cy="80" r="2.5" fill="rgba(255,255,255,0.1)"/></svg>');
        }

        .header h1 {
            font-size: 2.5em;
            margin-bottom: 10px;
            position: relative;
            z-index: 1;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.2);
        }

        .header p {
            font-size: 1.2em;
            opacity: 0.9;
            position: relative;
            z-index: 1;
        }

        .nav-buttons {
            display: flex;
            justify-content: center;
            gap: 10px;
            padding: 20px;
            background: #f8f9fa;
            flex-wrap: wrap;
        }

        .nav-btn {
            padding: 12px 24px;
            border: none;
            border-radius: 25px;
            cursor: pointer;
            font-size: 16px;
            font-weight: bold;
            transition: all 0.3s ease;
            box-shadow: 0 4px 15px rgba(0,0,0,0.1);
        }

        .nav-btn.active {
            background: linear-gradient(135deg, #8e44ad, #3498db);
            color: white;
            transform: translateY(-2px);
            box-shadow: 0 6px 20px rgba(142, 68, 173, 0.4);
        }

        .nav-btn:not(.active) {
            background: white;
            color: #666;
        }

        .nav-btn:hover:not(.active) {
            background: #e9ecef;
            transform: translateY(-1px);
        }

        .game-section {
            display: none;
            padding: 30px;
            min-height: 400px;
        }

        .game-section.active {
            display: block;
            animation: fadeIn 0.5s ease-in;
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(20px); }
            to { opacity: 1; transform: translateY(0); }
        }

        .word-bank {
            background: linear-gradient(135deg, #f5f7fa, #e8f4f2);
            padding: 25px;
            border-radius: 15px;
            margin-bottom: 25px;
            border: 2px solid #8e44ad;
            box-shadow: 0 4px 15px rgba(142, 68, 173, 0.2);
        }

        .word-bank h3 {
            color: #8e44ad;
            margin-bottom: 15px;
            text-align: center;
            font-size: 1.4em;
        }

        .word-options {
            display: flex;
            flex-wrap: wrap;
            gap: 12px;
            justify-content: center;
        }

        .word-option {
            background: linear-gradient(135deg, #8e44ad, #3498db);
            color: white;
            padding: 10px 18px;
            border-radius: 20px;
            font-weight: bold;
            font-size: 16px;
            box-shadow: 0 3px 10px rgba(142, 68, 173, 0.3);
            transition: all 0.3s ease;
            cursor: default;
        }

        .word-option:hover {
            transform: translateY(-2px);
            box-shadow: 0 5px 15px rgba(142, 68, 173, 0.4);
        }

        .question {
            background: #f8f9fa;
            padding: 25px;
            border-radius: 15px;
            margin-bottom: 20px;
            border-left: 5px solid #8e44ad;
            box-shadow: 0 4px 15px rgba(0,0,0,0.05);
        }

        .question h3 {
            color: #8e44ad;
            margin-bottom: 15px;
            font-size: 1.3em;
        }

        .fill-blank {
            background: #fff;
            border: 2px solid #ddd;
            border-radius: 8px;
            padding: 8px 12px;
            font-size: 16px;
            margin: 0 5px;
            min-width: 120px;
            transition: border-color 0.3s ease;
        }

        .fill-blank.correct {
            border-color: #4CAF50;
            background: #e8f5e8;
        }

        .fill-blank.incorrect {
            border-color: #f44336;
            background: #ffeaea;
        }

        .options {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 15px;
            margin-top: 15px;
        }

        .option {
            padding: 15px 20px;
            border: 2px solid #ddd;
            border-radius: 10px;
            cursor: pointer;
            transition: all 0.3s ease;
            background: white;
            text-align: center;
            font-weight: 500;
        }

        .option:hover {
            border-color: #8e44ad;
            transform: translateY(-2px);
            box-shadow: 0 4px 15px rgba(142, 68, 173, 0.2);
        }

        .option.selected {
            background: #8e44ad;
            color: white;
            border-color: #8e44ad;
        }

        .option.correct {
            background: #4CAF50;
            color: white;
            border-color: #4CAF50;
        }

        .option.incorrect {
            background: #f44336;
            color: white;
            border-color: #f44336;
        }

        .matching-container {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 30px;
            margin-top: 20px;
        }

        .match-column h4 {
            text-align: center;
            margin-bottom: 15px;
            color: #8e44ad;
            font-size: 1.2em;
        }

        .match-item {
            padding: 15px;
            margin: 8px 0;
            border: 2px solid #ddd;
            border-radius: 10px;
            cursor: pointer;
            transition: all 0.3s ease;
            background: white;
            text-align: center;
            font-weight: 500;
        }

        .match-item:hover {
            border-color: #8e44ad;
            transform: translateY(-1px);
            box-shadow: 0 4px 15px rgba(142, 68, 173, 0.2);
        }

        .match-item.selected {
            background: #e8f4f2;
            border-color: #8e44ad;
        }

        .match-item.matched {
            background: #4CAF50;
            color: white;
            border-color: #4CAF50;
            cursor: default;
        }

        .check-btn {
            background: linear-gradient(135deg, #8e44ad, #3498db);
            color: white;
            border: none;
            padding: 15px 30px;
            border-radius: 25px;
            cursor: pointer;
            font-size: 16px;
            font-weight: bold;
            margin: 20px auto;
            display: block;
            transition: all 0.3s ease;
            box-shadow: 0 4px 15px rgba(142, 68, 173, 0.3);
        }

        .check-btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 6px 20px rgba(142, 68, 173, 0.4);
        }

        .feedback {
            margin-top: 15px;
            padding: 15px;
            border-radius: 10px;
            font-weight: bold;
            text-align: center;
            animation: slideIn 0.3s ease;
        }

        @keyframes slideIn {
            from { transform: translateX(-20px); opacity: 0; }
            to { transform: translateX(0); opacity: 1; }
        }

        .feedback.correct {
            background: #d4edda;
            color: #155724;
            border: 1px solid #c3e6cb;
        }

        .feedback.incorrect {
            background: #f8d7da;
            color: #721c24;
            border: 1px solid #f5c6cb;
        }

        .score {
            position: fixed;
            top: 20px;
            right: 20px;
            background: linear-gradient(135deg, #8e44ad, #3498db);
            color: white;
            padding: 15px 20px;
            border-radius: 25px;
            font-weight: bold;
            box-shadow: 0 4px 15px rgba(142, 68, 173, 0.3);
            z-index: 1000;
        }

        @media (max-width: 768px) {
            .matching-container {
                grid-template-columns: 1fr;
                gap: 20px;
            }
            
            .nav-buttons {
                flex-direction: column;
                align-items: center;
            }
            
            .nav-btn {
                width: 200px;
            }
            
            .score {
                position: static;
                margin: 20px auto;
                display: block;
                width: fit-content;
            }
        }
    </style>
</head>
<body>
    <div class="score">Score: <span id="score">0</span>/27</div>
    
    <div class="container">
        <div class="header">
            <h1>📚 English Expressions Game: Part 4</h1>
            <p>Test your knowledge of these useful English expressions!</p>
        </div>

        <div class="nav-buttons">
            <button class="nav-btn active" onclick="showSection('fill-gaps')">Fill in the Gaps</button>
            <button class="nav-btn" onclick="showSection('matching')">Match Meanings</button>
            <button class="nav-btn" onclick="showSection('multiple-choice')">Multiple Choice</button>
        </div>

        <!-- Fill in the Gaps Section -->
        <div id="fill-gaps" class="game-section active">
            <div class="word-bank">
                <h3>📝 Word Bank - Choose from these words:</h3>
                <div class="word-options">
                    <span class="word-option">freelancer</span>
                    <span class="word-option">hard</span>
                    <span class="word-option">expect</span>
                    <span class="word-option">argue</span>
                    <span class="word-option">tell off</span>
                    <span class="word-option">commute</span>
                    <span class="word-option">town</span>
                    <span class="word-option">petrol</span>
                    <span class="word-option">retire</span>
                </div>
            </div>

            <div class="question">
                <h3>Question 1:</h3>
                <p>My father plans to <input type="text" class="fill-blank" data-answer="retire" placeholder="answer"> next year when he turns 65.</p>
                <div class="feedback" id="feedback-1" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 2:</h3>
                <p>As a <input type="text" class="fill-blank" data-answer="freelancer" placeholder="answer">, she enjoys the flexibility of choosing her own projects.</p>
                <div class="feedback" id="feedback-2" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 3:</h3>
                <p>I had to <input type="text" class="fill-blank" data-answer="tell off" placeholder="answer"> my son for not doing his homework.</p>
                <div class="feedback" id="feedback-3" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 4:</h3>
                <p>My daily <input type="text" class="fill-blank" data-answer="commute" placeholder="answer"> to work takes about 45 minutes each way.</p>
                <div class="feedback" id="feedback-4" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 5:</h3>
                <p>We need to stop at the station to fill up the car with <input type="text" class="fill-blank" data-answer="petrol" placeholder="answer">.</p>
                <div class="feedback" id="feedback-5" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 6:</h3>
                <p>It's <input type="text" class="fill-blank" data-answer="hard" placeholder="answer"> to find a parking space in the city center.</p>
                <div class="feedback" id="feedback-6" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 7:</h3>
                <p>I <input type="text" class="fill-blank" data-answer="expect" placeholder="answer"> this project to be completed by Friday.</p>
                <div class="feedback" id="feedback-7" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 8:</h3>
                <p>My brother and I used to <input type="text" class="fill-blank" data-answer="argue" placeholder="answer"> about everything when we were children.</p>
                <div class="feedback" id="feedback-8" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 9:</h3>
                <p>The nearest <input type="text" class="fill-blank" data-answer="town" placeholder="answer"> is about 10 miles from our village.</p>
                <div class="feedback" id="feedback-9" style="display: none;"></div>
            </div>

            <button class="check-btn" onclick="checkFillBlanks()">Check Answers</button>
        </div>

        <!-- Matching Section -->
        <div id="matching" class="game-section">
            <h2 style="text-align: center; margin-bottom: 20px; color: #8e44ad;">Match the expressions with their meanings</h2>
            <div class="matching-container">
                <div class="match-column">
                    <h4>Words</h4>
                    <div class="match-item" data-word="freelancer" onclick="selectMatch(this)">freelancer</div>
                    <div class="match-item" data-word="hard" onclick="selectMatch(this)">hard</div>
                    <div class="match-item" data-word="expect" onclick="selectMatch(this)">expect</div>
                    <div class="match-item" data-word="argue" onclick="selectMatch(this)">argue</div>
                    <div class="match-item" data-word="tell off" onclick="selectMatch(this)">tell off</div>
                    <div class="match-item" data-word="commute" onclick="selectMatch(this)">commute</div>
                    <div class="match-item" data-word="town" onclick="selectMatch(this)">town</div>
                    <div class="match-item" data-word="petrol" onclick="selectMatch(this)">petrol</div>
                    <div class="match-item" data-word="retire" onclick="selectMatch(this)">retire</div>
                </div>
                <div class="match-column">
                    <h4>Meanings</h4>
                    <div class="match-item" data-meaning="retire" onclick="selectMatch(this)">To leave one's job and cease to work, typically upon reaching a certain age</div>
                    <div class="match-item" data-meaning="freelancer" onclick="selectMatch(this)">A person who works on a self-employed basis for multiple clients</div>
                    <div class="match-item" data-meaning="tell off" onclick="selectMatch(this)">To scold or reprimand someone angrily</div>
                    <div class="match-item" data-meaning="commute" onclick="selectMatch(this)">To travel some distance between one's home and place of work regularly</div>
                    <div class="match-item" data-meaning="petrol" onclick="selectMatch(this)">A fuel derived from petroleum, used in internal combustion engines</div>
                    <div class="match-item" data-meaning="hard" onclick="selectMatch(this)">Difficult to do or accomplish; requiring great effort</div>
                    <div class="match-item" data-meaning="expect" onclick="selectMatch(this)">To regard something as likely to happen; to anticipate</div>
                    <div class="match-item" data-meaning="argue" onclick="selectMatch(this)">To exchange opposing viewpoints; to dispute or quarrel</div>
                    <div class="match-item" data-meaning="town" onclick="selectMatch(this)">An urban area that is larger than a village but smaller than a city</div>
                </div>
            </div>
            <div class="feedback" id="matching-feedback" style="display: none;"></div>
        </div>

        <!-- Multiple Choice Section -->
        <div id="multiple-choice" class="game-section">
            <div class="question">
                <h3>Question 1: What does "freelancer" mean?</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">A person who works for free</div>
                    <div class="option" onclick="selectOption(this, true)">A self-employed person working for multiple clients</div>
                    <div class="option" onclick="selectOption(this, false)">A person who works in freedom advocacy</div>
                    <div class="option" onclick="selectOption(this, false)">A person who works without a schedule</div>
                </div>
                <div class="feedback" id="mc-feedback-1" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 2: "Hard" means:</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">Easy to accomplish</div>
                    <div class="option" onclick="selectOption(this, true)">Difficult; requiring great effort</div>
                    <div class="option" onclick="selectOption(this, false)">Solid in substance</div>
                    <div class="option" onclick="selectOption(this, false)">Not soft</div>
                </div>
                <div class="feedback" id="mc-feedback-2" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 3: "Expect" refers to:</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">To hope for something unlikely</div>
                    <div class="option" onclick="selectOption(this, true)">To regard something as likely to happen</div>
                    <div class="option" onclick="selectOption(this, false)">To remember something</div>
                    <div class="option" onclick="selectOption(this, false)">To fear something</div>
                </div>
                <div class="feedback" id="mc-feedback-3" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 4: "Argue" means:</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">To agree with someone</div>
                    <div class="option" onclick="selectOption(this, true)">To exchange opposing viewpoints; to dispute</div>
                    <div class="option" onclick="selectOption(this, false)">To present a legal case in court</div>
                    <div class="option" onclick="selectOption(this, false)">To suggest an idea</div>
                </div>
                <div class="feedback" id="mc-feedback-4" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 5: "Tell off" refers to:</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">To inform someone about something</div>
                    <div class="option" onclick="selectOption(this, true)">To scold or reprimand someone angrily</div>
                    <div class="option" onclick="selectOption(this, false)">To say goodbye to someone</div>
                    <div class="option" onclick="selectOption(this, false)">To share a story</div>
                </div>
                <div class="feedback" id="mc-feedback-5" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 6: "Commute" means:</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">To reduce a judicial sentence</div>
                    <div class="option" onclick="selectOption(this, true)">To travel regularly between home and workplace</div>
                    <div class="option" onclick="selectOption(this, false)">To change one form of transportation for another</div>
                    <div class="option" onclick="selectOption(this, false)">To communicate with others</div>
                </div>
                <div class="feedback" id="mc-feedback-6" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 7: "Town" refers to:</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">A very large urban area</div>
                    <div class="option" onclick="selectOption(this, true)">An urban area larger than a village but smaller than a city</div>
                    <div class="option" onclick="selectOption(this, false)">A rural area with few buildings</div>
                    <div class="option" onclick="selectOption(this, false)">A suburban neighborhood</div>
                </div>
                <div class="feedback" id="mc-feedback-7" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 8: "Petrol" means:</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">A type of cooking oil</div>
                    <div class="option" onclick="selectOption(this, true)">Fuel for vehicles derived from petroleum</div>
                    <div class="option" onclick="selectOption(this, false)">A cleaning solvent</div>
                    <div class="option" onclick="selectOption(this, false)">A type of natural gas</div>
                </div>
                <div class="feedback" id="mc-feedback-8" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 9: "Retire" refers to:</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">To go to bed for the night</div>
                    <div class="option" onclick="selectOption(this, true)">To leave one's job and cease working, typically upon reaching a certain age</div>
                    <div class="option" onclick="selectOption(this, false)">To withdraw from a competition</div>
                    <div class="option" onclick="selectOption(this, false)">To move to a quieter place</div>
                </div>
                <div class="feedback" id="mc-feedback-9" style="display: none;"></div>
            </div>
        </div>
    </div>

    <script>
        let score = 0;
        let selectedWord = null;
        let selectedMeaning = null;
        let matchedPairs = [];

        function showSection(sectionId) {
            // Hide all sections
            document.querySelectorAll('.game-section').forEach(section => {
                section.classList.remove('active');
            });
            
            // Remove active class from all buttons
            document.querySelectorAll('.nav-btn').forEach(btn => {
                btn.classList.remove('active');
            });
            
            // Show selected section
            document.getElementById(sectionId).classList.add('active');
            
            // Add active class to clicked button
            event.target.classList.add('active');
        }

        function checkFillBlanks() {
            const blanks = document.querySelectorAll('.fill-blank');
            let correctCount = 0;
            
            blanks.forEach((blank, index) => {
                const userAnswer = blank.value.toLowerCase().trim();
                const correctAnswer = blank.dataset.answer.toLowerCase();
                
                if (userAnswer === correctAnswer) {
                    blank.classList.remove('incorrect');
                    blank.classList.add('correct');
                    correctCount++;
                } else {
                    blank.classList.remove('correct');
                    blank.classList.add('incorrect');
                }
                
                // Show feedback for each question
                const feedback = document.getElementById(`feedback-${index+1}`);
                if (userAnswer === correctAnswer) {
                    feedback.textContent = '✅ Correct!';
                    feedback.className = 'feedback correct';
                } else {
                    feedback.textContent = `❌ Incorrect. The correct answer is: "${blank.dataset.answer}"`;
                    feedback.className = 'feedback incorrect';
                }
                feedback.style.display = 'block';
            });
            
            updateScore();
        }

        function selectMatch(element) {
            if (element.classList.contains('matched')) return;
            
            if (element.dataset.word) {
                // Word selected
                if (selectedWord) selectedWord.classList.remove('selected');
                selectedWord = element;
                element.classList.add('selected');
            } else {
                // Meaning selected
                if (selectedMeaning) selectedMeaning.classList.remove('selected');
                selectedMeaning = element;
                element.classList.add('selected');
            }
            
            // Check if we have both word and meaning selected
            if (selectedWord && selectedMeaning) {
                checkMatch();
            }
        }

        function checkMatch() {
            const feedback = document.getElementById('matching-feedback');
            
            if (selectedWord.dataset.word === selectedMeaning.dataset.meaning) {
                // Correct match
                selectedWord.classList.remove('selected');
                selectedWord.classList.add('matched');
                selectedMeaning.classList.remove('selected');
                selectedMeaning.classList.add('matched');
                
                matchedPairs.push(selectedWord.dataset.word);
                
                feedback.textContent = '✅ Correct match!';
                feedback.className = 'feedback correct';
                
                // Check if all matches are complete
                if (matchedPairs.length === 9) {
                    feedback.textContent = '🎉 Congratulations! You matched all terms correctly!';
                }
            } else {
                // Incorrect match
                feedback.textContent = '❌ Incorrect match. Try again.';
                feedback.className = 'feedback incorrect';
            }
            
            feedback.style.display = 'block';
            selectedWord = null;
            selectedMeaning = null;
            
            updateScore();
        }

        function selectOption(element, isCorrect) {
            // Remove selection from all options in this question
            const options = element.parentElement.querySelectorAll('.option');
            options.forEach(opt => {
                opt.classList.remove('selected');
                opt.classList.remove('correct');
                opt.classList.remove('incorrect');
            });
            
            // Mark the selected option
            element.classList.add('selected');
            
            const questionNumber = element.closest('.question').querySelector('h3').textContent.match(/\d+/)[0];
            const feedback = document.getElementById(`mc-feedback-${questionNumber}`);
            
            if (isCorrect) {
                element.classList.add('correct');
                feedback.textContent = '✅ Correct!';
                feedback.className = 'feedback correct';
            } else {
                element.classList.add('incorrect');
                feedback.textContent = '❌ Incorrect. Try again.';
                feedback.className = 'feedback incorrect';
                
                // Show the correct answer
                options.forEach(opt => {
                    if (opt.onclick.toString().includes('true')) {
                        opt.classList.add('correct');
                    }
                });
            }
            
            feedback.style.display = 'block';
            updateScore();
        }

        function updateScore() {
            // Calculate score for fill-in-the-blank
            let fillScore = 0;
            document.querySelectorAll('.fill-blank.correct').forEach(blank => {
                if (!blank.classList.contains('counted')) {
                    fillScore++;
                    blank.classList.add('counted');
                }
            });
            
            // Calculate score for matching (each pair is 1 point)
            const matchScore = matchedPairs.length;
            
            // Calculate score for multiple choice (each correct is 1 point)
            let mcScore = 0;
            document.querySelectorAll('.option.correct.selected').forEach(opt => {
                mcScore++;
            });
            
            // Total score
            score = fillScore + matchScore + mcScore;
            document.getElementById('score').textContent = score;
        }
    </script>
</body>
</html>
