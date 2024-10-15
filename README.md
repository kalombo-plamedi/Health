# Health
<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>santé et sécurité.com</title>
    <style>
        :root {
            --primary-color: #2980b9;
            --secondary-color: #27ae60;
            --accent-color: #c0392b;
            --text-color: #333;
            --header-bg-color: linear-gradient(to right, #7b4397, #dc2430);
        }

        body {
            font-family: 'Montserrat', sans-serif;
            margin: 0;
            padding: 0;
            background-color: #f5f5f5;
            color: var(--text-color);
        }

        header {
            background: var(--header-bg-color);
            color: #fff;
            padding: 20px;
            text-align: center;
            width: 100%;
            position: relative;
        }

        h1 {
            margin: 0;
            font-size: 48px;
            font-family: 'Satisfy', cursive;
            text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.5);
        }

        .menu-toggle {
            cursor: pointer;
            font-size: 24px;
            position: absolute;
            left: 20px;
            top: 20px;
            z-index: 10;
            color: #fff;
        }

        nav {
            background-color: white;
            padding: 15px;
            border-radius: 5px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
            position: fixed;
            left: 20px;
            top: 100px;
            width: 200px;
            z-index: 10;
            transform: translateX(-100%);
            transition: transform 0.3s ease;
        }

        nav.show {
            transform: translateX(0);
        }

        nav a {
            display: block;
            margin: 10px 0;
            text-decoration: none;
            color: var(--primary-color);
            font-weight: bold;
        }

        .container {
            max-width: 800px;
            margin: 20px auto;
            background-color: white;
            padding: 20px;
            border-radius: 5px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
        }

        label {
            display: block;
            margin-bottom: 10px;
        }

        input[type="number"], input[type="date"], input[type="email"], input[type="password"] {
            width: 100%;
            padding: 10px;
            border: 1px solid #ccc;
            border-radius: 4px;
            box-sizing: border-box;
            margin-bottom: 20px;
        }

        button {
            background-color: var(--secondary-color);
            color: white;
            padding: 10px 20px;
            border: none;
            border-radius: 4px;
            cursor: pointer;
            display: block;
            margin: 0 auto;
        }

        button:hover {
            background-color: var(--accent-color);
        }

        .advice {
            margin-top: 20px;
            font-size: 16px;
            color: var(--text-color);
        }

        .warning {
            color: red;
        }

        .result {
            margin-top: 20px;
            padding: 10px;
            border: 1px solid #ccc;
            background-color: #f9f9f9;
        }

        .hidden {
            display: none;
        }
    </style>
    <link href="https://fonts.googleapis.com/css2?family=Montserrat:wght@400;700&family=Satisfy&display=swap" rel="stylesheet">
</head>
<body>

<header>
    <div class="menu-toggle" onclick="toggleMenu()">&#9776;</div>
    <h1>s<span style="color:var(--secondary-color)">a</span>n<span style="color:var(--accent-color)">t</span><span style="color:var(--primary-color)">é</span> et sécurité<span style="color:var(--secondary-color)">.c</span>om</h1>
</header>

<nav id="menu"></nav>

<div id="accueil" class="container">
    <h1>Bienvenue sur santé et sécurité.com</h1>
    <p>Nous sommes heureux de vous accueillir sur notre site. Ici, vous trouverez des ressources précieuses pour vous aider à prendre soin de votre santé et bien-être.</p>
    <p>Pour nous contacter :</p>
    <p>Email : <a href="mailto:kalomboplamsdy@gmail.com">kalomboplamsdy@gmail.com</a></p>
    <p>Téléphone : <a href="tel:+243820814400">+243 820 814 400</a></p>
</div>

<div id="signup" class="container">
    <h1>Créer un Compte</h1>
    <label for="signupEmail">Email :</label>
    <input type="email" id="signupEmail" required>
    <label for="signupPassword">Mot de passe :</label>
    <input type="password" id="signupPassword" required>
    <button onclick="createAccount()">Créer un Compte</button>
    <div id="signupResult"></div>
</div>

<div id="cycle" class="container">
    <h1>Calculateur de Cycle Menstruel</h1>
    <label for="lastPeriod">Dernier jour de vos règles :</label>
    <input type="date" id="lastPeriod">
    <label for="cycleLength">Durée de votre cycle (jours) :</label>
    <input type="number" id="cycleLength" value="28" min="21" max="35">
    <button onclick="calculateCycle()">Calculer</button>
    <div id="cycleResult"></div>
</div>

<div id="imc" class="container">
    <h1>Calcul de l'Indice de Masse Corporelle</h1>
    <label for="height">Taille (m) :</label>
    <input type="number" id="height" step="0.01" required>
    <label for="weight">Poids (kg) :</label>
    <input type="number" id="weight" step="0.1" required>
    <button onclick="calculateBMI()">Calculer l'IMC</button>
    <div id="imcResult"></div>
    <div id="healthAdvice" class="advice"></div>
</div>

<!-- Nouvelle section pour Symptômes et Maladies -->
<div id="symptomes" class="container">
    <h1>Choisissez vos Symptômes</h1>
    <p>Sélectionnez au moins 6 symptômes :</p>
    <form id="symptomForm">
        <div>
            <label><input type="checkbox" class="symptom" value="Fièvre"> Fièvre</label><br>
            <label><input type="checkbox" class="symptom" value="Toux"> Toux</label><br>
            <label><input type="checkbox" class="symptom" value="Fatigue"> Fatigue</label><br>
            <label><input type="checkbox" class="symptom" value="Douleurs musculaires"> Douleurs musculaires</label><br>
            <label><input type="checkbox" class="symptom" value="Maux de tête"> Maux de tête</label><br>
            <label><input type="checkbox" class="symptom" value="Essoufflement"> Essoufflement</label><br>
            <label><input type="checkbox" class="symptom" value="Nausées"> Nausées</label><br>
            <label><input type="checkbox" class="symptom" value="Diarrhée"> Diarrhée</label><br>
            <label><input type="checkbox" class="symptom" value="Douleur thoracique"> Douleur thoracique</label><br>
            <label><input type="checkbox" class="symptom" value="Démangeaisons"> Démangeaisons</label><br>
            <label><input type="checkbox" class="symptom" value="Rougeurs"> Rougeurs</label><br>
            <label><input type="checkbox" class="symptom" value="Perte de poids"> Perte de poids</label><br>
            <label><input type="checkbox" class="symptom" value="Troubles du sommeil"> Troubles du sommeil</label><br>
            <label><input type="checkbox" class="symptom" value="Engourdissement"> Engourdissement</label><br>
            <label><input type="checkbox" class="symptom" value="Rougeur des yeux"> Rougeur des yeux</label><br>
            <label><input type="checkbox" class="symptom" value="Crampe abdominale"> Crampe abdominale</label><br>
            <label><input type="checkbox" class="symptom" value="Irritabilité"> Irritabilité</label><br>
            <label><input type="checkbox" class="symptom" value="Vomissements"> Vomissements</label><br>
            <label><input type="checkbox" class="symptom" value="Frissons"> Frissons</label><br>
            <label><input type="checkbox" class="symptom" value="Saignement rectal"> Saignement rectal</label><br>
            <label><input type="checkbox" class="symptom" value="Douleur abdominale"> Douleur abdominale</label><br>
            <label><input type="checkbox" class="symptom" value="Perte d'appétit"> Perte d'appétit</label><br>
            <label><input type="checkbox" class="symptom" value="Hypertension"> Hypertension</label><br>
        </div>
        <button type="submit">Soumettre</button>
    </form>
    <div id="result" class="result hidden"></div>
</div>
<script>
    const sections = [
        { id: 'accueil', name: 'Accueil' },
        { id: 'signup', name: 'Créer un Compte' },
        { id: 'cycle', name: 'Calcul de Cycle Menstruel' },
        { id: 'imc', name: "Calcul de l'IMC" },
        { id: 'symptomes', name: 'Symptômes et Maladies' }
    ];

    function generateMenu() {
        const menu = document.getElementById('menu');
        sections.forEach(section => {
            const link = document.createElement('a');
            link.href = `#${section.id}`;
            link.textContent = section.name;
            menu.appendChild(link);
        });
    }

    window.onload = function() {
        generateMenu();
        const userEmail = localStorage.getItem('userEmail');
        if (userEmail) {
            document.getElementById('signup').style.display = 'none';
            document.getElementById('accueil').innerHTML += `<p>Bienvenue, ${userEmail} !</p>`;
        }
    };

    function toggleMenu() {
        const menu = document.getElementById('menu');
        menu.classList.toggle('show');
    }

    function createAccount() {
        const email = document.getElementById('signupEmail').value;
        const password = document.getElementById('signupPassword').value;

        if (!email || !password) {
            document.getElementById('signupResult').innerHTML = "Veuillez remplir tous les champs.";
            return;
        }

        localStorage.setItem('userEmail', email);
        localStorage.setItem('userPassword', password);

        document.getElementById('signupResult').innerHTML = "Compte créé avec succès ! Vous êtes maintenant connecté.";
    }

    function calculateCycle() {
        const lastPeriod = new Date(document.getElementById('lastPeriod').value);
        const cycleLength = parseInt(document.getElementById('cycleLength').value);
        const ovulationDay = lastPeriod.getDate() + (cycleLength - 14);
        const nextPeriodStart = new Date(lastPeriod);
        nextPeriodStart.setDate(lastPeriod.getDate() + cycleLength);

        const ovulationStart = new Date(nextPeriodStart);
        ovulationStart.setDate(ovulationDay - 1);
        const ovulationEnd = new Date(ovulationStart);
        ovulationEnd.setDate(ovulationStart.getDate() + 2);

        const safeDaysStart = new Date(ovulationStart);
        safeDaysStart.setDate(ovulationStart.getDate() - 4);
        const safeDaysEnd = new Date(ovulationEnd);
        safeDaysEnd.setDate(ovulationEnd.getDate() + 1);

        const girlDaysStart = new Date(ovulationStart);
        girlDaysStart.setDate(ovulationStart.getDate() - 1);
        const girlDaysEnd = new Date(ovulationStart);
        girlDaysEnd.setDate(ovulationStart.getDate() + 1);

        const boyDaysStart = new Date(ovulationEnd);
        boyDaysStart.setDate(ovulationEnd.getDate() - 1);
        const boyDaysEnd = new Date(ovulationEnd);
        boyDaysEnd.setDate(ovulationEnd.getDate() + 1);

        const resultDiv = document.getElementById('cycleResult');
        resultDiv.innerHTML = `
            <h3>Résultats :</h3>
            <p><strong>Prochain jour de règles :</strong> ${nextPeriodStart.toLocaleDateString()}</p>
            <p><strong>Jours d'ovulation :</strong> ${ovulationStart.toLocaleDateString()} à ${ovulationEnd.toLocaleDateString()}</p>
            <p><strong>Jours à éviter pour tomber enceinte :</strong> ${safeDaysStart.toLocaleDateString()} à ${safeDaysEnd.toLocaleDateString()}</p>
            <h4>Pour concevoir :</h4>
            <p><strong>Une fille :</strong> Avoir des rapports entre le ${girlDaysStart.toLocaleDateString()} et le ${girlDaysEnd.toLocaleDateString()}.</p>
            <p><strong>Un garçon :</strong> Avoir des rapports entre le ${boyDaysStart.toLocaleDateString()} et le ${boyDaysEnd.toLocaleDateString()}.</p>
        `;
    }

    function calculateBMI() {
        const height = parseFloat(document.getElementById("height").value);
        const weight = parseFloat(document.getElementById("weight").value);
        
        if (isNaN(height) || isNaN(weight) || height <= 0 || weight <= 0) {
            document.getElementById("imcResult").innerHTML = "Veuillez saisir des valeurs valides.";
            return;
        }

        const bmi = weight / (height * height);
        let bmiStatus;
        let healthAdvice = "";

        if (bmi < 18.5) {
            bmiStatus = "Vous êtes en sous-poids.";
            healthAdvice = "Il est conseillé d'augmenter votre apport calorique. Consommez des aliments riches en nutriments et envisagez de consulter un professionnel de la santé.";
        } else if (bmi < 25) {
            bmiStatus = "Votre poids est normal.";
            healthAdvice = "Continuez à maintenir une alimentation équilibrée et à faire de l'exercice régulièrement.";
        } else if (bmi < 30) {
            bmiStatus = "Vous êtes en surpoids.";
            healthAdvice = "Considérez une alimentation équilibrée et un programme d'exercice. Consultez un nutritionniste pour des conseils personnalisés.";
        } else {
            bmiStatus = "Vous êtes obèse.";
            healthAdvice = "Il est fortement recommandé de consulter un professionnel de la santé pour élaborer un plan de gestion du poids adapté.";
        }

        document.getElementById("imcResult").innerHTML = "Votre IMC est de " + bmi.toFixed(2) + ". " + bmiStatus;
        document.getElementById("healthAdvice").innerHTML = healthAdvice;
    }

    // Script du programme Symptômes et Maladies
    const symptomsToConditions = {
        "Fièvre": ["Grippe", "Infection urinaire", "Typhoïde", "Paludisme", "Coronavirus"],
        "Toux": ["Grippe", "Asthme", "Infection virale", "Coronavirus"],
        "Fatigue": ["Dépression", "Anémie", "Insuffisance cardiaque", "Diabète"],
        "Douleurs musculaires": ["Grippe", "Fibromyalgie"],
        "Maux de tête": ["Dépression", "Migraine"],
        "Essoufflement": ["Asthme", "Insuffisance cardiaque"],
        "Nausées": ["Infection virale", "Pancréatite", "Typhoïde"],
        "Diarrhée": ["Maladie de Crohn", "Infection urinaire", "Typhoïde"],
        "Douleur thoracique": ["Maladie coronarienne", "Anxiété"],
        "Démangeaisons": ["Allergies", "Eczéma"],
        "Rougeurs": ["Allergies", "Psoriasis"],
        "Perte de poids": ["Diabète de type 2", "Cancer", "Hypertension"],
        "Troubles du sommeil": ["Dépression", "Anxiété"],
        "Engourdissement": ["Sclérose en plaques", "Diabète de type 2"],
        "Rougeur des yeux": ["Conjonctivite", "Allergies"],
        "Crampe abdominale": ["Maladie de Crohn", "Syndrome du côlon irritable", "Typhoïde", "Appendicite"],
        "Irritabilité": ["Dépression", "Anxiété"],
        "Vomissements": ["Infection virale", "Typhoïde", "Appendicite"],
        "Frissons": ["Grippe", "Paludisme", "Typhoïde"],
        "Saignement rectal": ["Hémorroïdes", "Maladie inflammatoire de l'intestin"]
    };

    document.getElementById('symptomForm').onsubmit = function(event) {
        event.preventDefault();

        const selectedSymptoms = Array.from(document.querySelectorAll('.symptom:checked')).map(el => el.value);

                if (selectedSymptoms.length < 6) {
            alert("Veuillez sélectionner au moins 6 symptômes.");
            return;
        }

        const conditions = new Set();
        selectedSymptoms.forEach(symptom => {
            if (symptomsToConditions[symptom]) {
                symptomsToConditions[symptom].forEach(condition => conditions.add(condition));
            }
        });

        const mostLikelyCondition = [...conditions][0]; // Prendre la première condition comme la plus probable
        const advice = `La maladie ayant le plus de probabilité est ${mostLikelyCondition}. En cas de symptômes persistants, il est conseillé de consulter un professionnel de santé.`;

        const resultDiv = document.getElementById('result');
        resultDiv.classList.remove('hidden');
        resultDiv.innerHTML = `<h3>Conditions possibles :</h3><p>${Array.from(conditions).join(', ')}</p><p class="advice">${advice}</p>`;
    };
</script>

</body>
</html>

