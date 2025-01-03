<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <title>Qui est-ce ? - Équipe Communication</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #f4f4f9;
            color: #333;
            text-align: center;
            padding: 20px;
        }
        h1 {
            color: #003369;
        }
        .instructions {
            font-size: 18px;
            margin-bottom: 20px;
            color: #0099da;
        }
        .card-container {
            perspective: 1000px;
            display: inline-block;
            margin: 20px;
        }
        .member-card {
            width: 200px;
            height: 300px;
            position: relative;
            transform-style: preserve-3d;
            transition: transform 0.6s;
            cursor: pointer;
        }
        .member-card.is-flipped {
            transform: rotateY(180deg);
        }
        .card-face {
            position: absolute;
            width: 100%;
            height: 100%;
            backface-visibility: hidden;
            border-radius: 10px;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
        }
        .card-front {
            background-color: #FFFFFF;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
        }
        .card-front img {
            width: 150px;
            height: 150px;
            border-radius: 50%;
            margin-bottom: 10px;
        }
        .card-back {
            background-color: #003369;
            color: white;
            transform: rotateY(180deg);
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            padding: 20px;
        }
        .hidden {
            display: none;
        }
        #description {
            margin-top: 20px;
        }
        button {
            background-color: #08c792;
            color: white;
            border: none;
            padding: 10px 20px;
            text-align: center;
            text-decoration: none;
            display: inline-block;
            font-size: 16px;
            margin: 4px 2px;
            cursor: pointer;
            border-radius: 5px;
            transition: background-color 0.3s;
        }
        button:hover {
            background-color: #08c792;
        }
        .logo {
            width: 150px;
            margin-bottom: 20px;
        }
        .score {
            font-size: 18px;
            color: #003369;
            margin-top: 20px;
        }
    </style>
</head>
<body>
    <img src="https://i.imgur.com/YWt1xPU.png" alt="Kuehne+Nagel Logo" class="logo">
    <h1>Qui est-ce ? - Équipe Communication</h1>
    <p class="instructions">Cliquez sur un avatar pour découvrir les indices et tentez de deviner le prénom du collaborateur.</p>
    <div id="game">
        <!-- Les cartes des membres de l'équipe seront générées ici -->
    </div>
    <div class="score">Score: <span id="score">0</span></div>

    <script>
        const teamMembers = [
            { name: "Jean-Baptiste", role: "Directeur Communication", description: "Il supervise l'ensemble des activités de communication.", avatar: "https://i.imgur.com/Fl10YRX.jpg" },
            { name: "Laurie", role: "Responsable Communication Externe", description: "Elle gère les relations avec les médias et les partenaires externes.", avatar: "https://i.imgur.com/aeB7tiO.jpg" },
            { name: "Natasa", role: "Responsable Communication Interne", description: "Elle s'assure que les communications internes sont efficaces et engageantes.", avatar: "https://i.imgur.com/sxbDSt7.jpg" },
            { name: "Mathieu", role: "Responsable Marketing", description: "Il développe et met en œuvre des stratégies marketing.", avatar: "https://i.imgur.com/x7bauBO.jpg" },
            { name: "Albane", role: "Alternante Communication Externe", description: "Elle assiste Laurie dans la gestion des communications externes.", avatar: "https://i.imgur.com/qe7vQTd.jpg" },
            { name: "Diane", role: "Alternante Communication Interne", description: "Elle aide Natasa avec les communications internes.", avatar: "https://i.imgur.com/eB2VSZA.jpg" }
        ];

        const gameDiv = document.getElementById('game');
        const scoreDisplay = document.getElementById('score');
        let currentMember = null;
        let score = 0;

        teamMembers.forEach(member => {
            const cardContainer = document.createElement('div');
            cardContainer.className = 'card-container';

            const memberCard = document.createElement('div');
            memberCard.className = 'member-card';
            memberCard.innerHTML = `
                <div class="card-face card-front">
                    <img src="${member.avatar}" alt="Avatar">
                </div>
                <div class="card-face card-back">
                    <p>${member.description}</p>
                    <button onclick="guessMember('${member.name}')">Deviner</button>
                </div>
            `;
            cardContainer.appendChild(memberCard);
            gameDiv.appendChild(cardContainer);

            memberCard.addEventListener('click', () => {
                memberCard.classList.toggle('is-flipped');
                currentMember = member;
            });
        });

        function guessMember(name) {
            const guess = prompt("Quel est son prénom ?");
            if (guess && guess.toLowerCase() === name.toLowerCase()) {
                alert("Bravo ! Vous avez deviné correctement.");
                score++;
            } else {
                alert("Dommage, ce n'est pas la bonne personne.");
            }
            scoreDisplay.textContent = score;
        }
    </script>
</body>
</html>
