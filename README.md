<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Pour mon amie Ariane</title>
  <link rel="icon" href="data:image/svg+xml,<svg xmlns=%22http://www.w3.org/2000/svg%22 viewBox=%220 0 100 100%22><text y=%22.9em%22 font-size=%2290%22>❤️</text></svg>">
  <style>
    @import url('https://fonts.googleapis.com/css2?family=Poppins:ital,wght@1,400&display=swap');

    html, body {
      margin: 0;
      padding: 0;
      overflow: hidden;
      font-family: 'Poppins', sans-serif;
      background-color: black;
    }

    #diaporama-container {
      position: absolute;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
      width: 900px;
      height: 900px;
      border-radius: 50%;
      overflow: hidden;
      z-index: 0;
    }

    #cadre-fleur {
      position: absolute;
      top: 0;
      left: 0;
      width: 100vw;
      height: 100vh;
      background: url('cadre-fleur.png') no-repeat center/cover;
      z-index: 1;
      pointer-events: none;
    }

    #diaporama {
      width: 100%;
      height: 100%;
      object-fit: cover;
      transition: opacity 1s ease-in-out;
    }

    #citation {
      position: absolute;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
      background-color: black;
      color: white;
      padding: 20px;
      max-width: 80%;
      font-style: italic;
      font-size: 1.2em;
      text-align: center;
      font-family: 'Poppins', sans-serif;
      display: none;
      z-index: 3;
    }

    #btn-container {
      position: absolute;
      top: 5%;
      left: 50%;
      transform: translateX(-50%);
      text-align: center;
      z-index: 4;
    }

    #btn {
      width: 80px;
      height: 80px;
      background: #000 url('icon-01.png') no-repeat center/40px 40px;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      opacity: 0.8;
    }

    #btn:hover {
      animation: blink 1s infinite;
    }

    @keyframes blink {
      0%, 100% { opacity: 1; }
      50% { opacity: 0.5; }
    }

    #text-flottant {
      font-family: 'Poppins', sans-serif;
      font-size: 1.2em;
      color: white;
      opacity: 0;
      transition: opacity 0.5s;
      animation: floatText 2s infinite ease-in-out;
    }

    #btn-container:hover #text-flottant {
      opacity: 1;
    }

    @keyframes floatText {
      0%, 100% { transform: translateY(0); }
      50% { transform: translateY(-5px); }
    }

    .coeur {
      position: absolute;
      color: pink;
      font-size: 80px;
      animation: floatUp 2s ease-out forwards;
      z-index: 5;
    }

    @keyframes floatUp {
      0% {
        opacity: 1;
        transform: translateY(0) scale(1);
      }
      100% {
        opacity: 0;
        transform: translateY(-100px) scale(1.5);
      }
    }

    #popup-message {
      position: absolute;
      top: 30%;
      left: 50%;
      transform: translateX(-50%);
      background: rgba(0, 0, 0, 0.3);
      color: white;
      font-family: 'Poppins', sans-serif;
      padding: 20px;
      border-radius: 8px;
      display: none;
      z-index: 10;
    }
  </style>
</head>
<body>
  <div id="diaporama-container">
    <img id="diaporama" src="fond.jpg" alt="Fond" />
  </div>

  <div id="cadre-fleur"></div>

  <div id="btn-container">
    <button id="btn"></button>
    <div id="text-flottant">click mon mimi</div>
  </div>

  <div id="citation"></div>
  <div id="popup-message"></div>

  <audio id="musique" autoplay loop>
    <source src="musique.mp3" type="audio/mpeg">
    Votre navigateur ne supporte pas l'audio.
  </audio>

  <script>
    const btn = document.getElementById("btn");
    const citationBox = document.getElementById("citation");
    const popup = document.getElementById("popup-message");

const citations = [

"Tu peux être brillante et fatiguée. En même temps.",
  "Pas besoin de tout comprendre, parfois faut juste danser.",
  "Gémeaux : l’art de changer d’avis avec élégance.",
  "Tu ne t’es pas perdue, tu explores les détours jolis.",
  "Même sans stream, t’existes et c’est déjà immense.",
  "T’es pas faible, t’es juste humaine avec un cœur fluo.",
  "Tu mérites un Oscar pour avoir survécu à cette journée.",
  "Les Gémeaux, c’est le Wi-Fi de l’univers : instable mais vital.",
  "Tu rayonnes même en pyjama dépareillé.",
  "Ton anxiété n’est pas toi. Juste une passagère bruyante.",
  "Parfois, respirer est une victoire secrète.",
  "Le monde a besoin de ta lumière maladroite.",
  "Tu peux tout recommencer. Même un mardi à 15h17.",
  "Gémeaux : météo intérieure variable, mais ciel toujours magique.",
  "Aujourd’hui, ton seul job : être douce avec toi.",
  "Si t’as besoin de rien faire, c’est déjà un plan.",
  "T’es pas trop, t’es trop cool.",
  "Même quand t’y crois pas, le ciel croit en toi.",
  "On peut être cassée et lumineuse. Regarde les étoiles.",
  "T’es pas une erreur système. Juste une version rare.",
  "Gémeaux : mi-caos, mi-génie, 100% magnifique.",
  "Ton cerveau court un marathon. Laisse-lui des pauses sucrées.",
  "Ta seule mission aujourd’hui : respirer avec tendresse.",
  "Tu vaux plus qu’un algorithme.",
  "Ta voix compte, même si elle tremble.",
  "Pas besoin d’avoir le moral pour être formidable.",
  "T’es le genre de personne qu’on n’oublie jamais.",
  "T’as le droit de briller à ta manière.",
  "Twitch ou pas Twitch, t’es une étoile en streaming.",
  "Sois patiente avec toi. Tu pousses en silence.",
  "Ton anxiété ne pourra jamais éteindre ta gentillesse.",
  "Gémeaux : capable de changer le monde ET de zapper le dentifrice.",
  "Ta douceur est un super-pouvoir.",
  "Même sans énergie, t’as une aura de feu de camp.",
  "T’es pas en retard, t’es en expansion.",
  "T’as le droit de mettre pause sur tout.",
  "Tu mérites de te choisir en premier.",
  "Ton chaos est une forme d’art brut.",
  "T’as une galaxie dans la tête, et des fleurs dans les doigts.",
  "Ton anxiété te ment, ton cœur te guide.",
  "Aujourd’hui, ton courage c’est de rester là.",
  "T’es un horoscope vivant : imprévisible et fascinant.",
  "Même quand tu doutes, tu fais du bien aux autres.",
  "T’as pas besoin de glow pour être lumineuse.",
  "Si tu respires, t’avances déjà.",
  "Tu peux aimer fort et garder ton énergie.",
  "T’es une playlist cosmique entre deux silences.",
  "Tu peux tout changer ou ne rien faire, t’es aimée quand même.",
  "Chaque sourire que tu offres est une révolution tranquille.",
  "Ton âme mérite des couvertures et du chocolat.",
  "Tu mérites d’exister même sans rendre service.",
  "Sois douce avec la fille que t’étais hier.",
  "Ton rire c’est du miel dans une journée acide.",
  "Gémeaux : drama queen céleste et messagère des lunes.",
  "Tu fais de ton mieux. Et c’est déjà énorme.",
  "Pas besoin de like pour valider ton existence.",
  "T’es pas paumée, t’es en transition cosmique.",
  "Ton énergie douce est une rébellion magnifique.",
  "T’as survécu à hier. T’as déjà gagné.",
  "Même au ralenti, t’es bouleversante.",
  "Gémeaux : ambassadrice officielle du chaos poétique.",
  "Chaque jour tu fais un miracle que tu ne vois pas.",
  "Tu mérites le calme autant que l’enthousiasme.",
  "T’es pas nulle. T’es juste fatiguée et brillante.",
  "Ton anxiété n’annule pas ta magie.",
  "Le ciel t’applaudit même les jours sans like.",
  "Tu peux pleurer et être puissante à la fois.",
  "T’es une respiration précieuse dans ce monde pressé.",
  "Sois douce avec toi. Tu contiens des orages et des chants.",
  "T’as le droit de déconnecter. On t’aime toujours.",
  "Même tes silences inspirent.",
  "Tu n’es pas ton productivité. T’es un miracle ambulant.",
  "Tu mérites de te reposer sans t’expliquer.",
  "T’es un trésor planqué derrière une fatigue cosmique.",
  "Gémeaux : l’équilibre instable qu’on adore.",
  "T’as le droit d’aller lentement. T’as le droit d’exister.",
  "Même dans le brouillard, tu guides les autres.",
  "T’es un remède vivant à la tristesse du monde.",
  "T’as pas besoin de courage en majuscule. Juste d’un souffle.",
  "Tu mérites une médaille pour t’être levée.",
  "Gémeaux : double cœur, triple humour, zéro filtre.",
  "Même tes doutes ont une poésie particulière.",
  "T’es un soleil masqué par une couverture.",
  "Tu n’es pas vide. Tu guéris, doucement.",
  "T’as survécu à tous tes orages. Respire.",
  "T’as pas besoin d’un plan. Juste de croire en ton pas suivant.",
  "Même floue, tu fais du bien.",
  "Tu mérites un monde à ton rythme.",
  "T’as le droit de ne pas performer aujourd’hui.",
  "T’es pas faible, t’as juste un cœur géant à porter.",
  "Même sans maquillage, tu rayonnes d’âme.",
  "Ta présence soigne plus qu’un tuto YouTube.",
  "Gémeaux : tempête et arc-en-ciel dans le même stream.",
  "Tu vaux plus que tes statistiques du mois.",
  "Ton cœur mérite de la musique douce.",
  "T’es une œuvre en cours, et c’est magnifique.",
  "T’es le genre de personne qui rend les autres meilleurs.",
  "Même les pauses font partie du rythme.",
  "T’as rien à prouver. Juste à respirer.",
  "Tu fais de ton mieux, et c’est plus que suffisant.",
  "Ta lumière n’a besoin de l’accord de personne.",
  "Même les Gémeaux ont le droit de ne pas savoir quoi faire aujourd’hui.",
  "Respire, t’as survécu à pire.",
  "T’es pas en retard, t’es en orbite.",
  "Ta lumière est plus forte que tes doutes, même en pyjama.",
  "Gémeaux un jour, étoile toujours.",
  "C’est pas une mauvaise journée, c’est juste une intro confuse.",
  "Ton rire guérit les dimanches moroses.",
  "Tu n’es pas perdue, tu explores.",
  "Aujourd’hui c’est toi le soleil, même sans filtre.",
  "Un pas à la fois, même si tu marches en moonwalk.",
  "Tu n’as pas besoin d’être productive pour mériter l’amour.",
  "Le chaos, c’est ton superpouvoir de Gémeaux.",
  "Ton anxiété ment. Moi non. T’es géniale.",
  "Ta gentillesse est un sortilège permanent.",
  "Rien que ta présence rend le monde plus doux.",
  "Tu n’es pas trop. C’est juste que le monde est pas prêt.",
  "Tu peux douter, mais n’oublie pas : t’as survécu à Mercure rétrograde.",
  "Même si tu pleures, t’as toujours l’énergie d’une playlist de combat.",
  "Ta fragilité est une force. Et ton humour une armure rose fluo.",
  "Gémeaux = 2 cerveaux pour 1000 idées.",
  "Tu peux faire une pause. Le monde attendra ton retour.",
  "Tu n’as pas besoin de briller tous les jours. Parfois, tu scintilles en douce.",
  "C’est pas de la procrastination, c’est de la recharge astrale.",
  "Twitch n’est pas prêt pour ton glow-up.",
  "Si tu doutes de toi, relis ce message : TU DÉCHIRES.",
  "T’es une étoile filante : rare, brillante, imprévisible.",
  "Ta voix est douce comme un cookie chaud dans une tempête.",
  "Même les reines ont besoin de siestes imprévues.",
  "T’es plus forte que ce que ton anxiété te laisse croire.",
  "Ton cerveau va vite, laisse ton cœur le rattraper.",
  "Tu transformes la mélancolie en blague magique.",
  "Sois douce avec toi-même. Tu fais de ton mieux.",
  "Ton énergie est unique, comme un mème parfait à 3h du mat.",
  "Rien ne presse. Ton timing est céleste.",
  "Tu n’es pas en retard, tu construis ton mythe.",
  "Aucune planète ne peut stopper ton destin.",
  "Parfois ne rien faire, c’est guérir en douce.",
  "Rappelle-toi que tu es ton endroit sûr.",
  "T’as le droit d’avoir peur ET de foncer quand même.",
  "Même les étoiles ont besoin de repos cosmique.",
  "Chaque jour tu crées un peu plus ta propre légende.",
  "C’est pas toi qui es trop sensible, c’est le monde qui est mal réglé.",
  "T’es une poésie vivante avec des gifs animés en bonus.",
  "Gémeaux = génie chaotique avec un cœur en marshmallow.",
  "T’as pas besoin de permission pour être toi.",
  "T’es pas cassée, t’es en mise à jour.",
  "T’as le droit de changer d’avis, d’humeur et de destin.",
  "Sois aussi tendre avec toi que tu l’es avec les autres.",
  "Tu n’as pas besoin d’être aimée de tous. Juste de toi.",
  "Le courage c’est pas d’avoir pas peur, c’est d’appuyer sur « go live » quand même.",
  "T’es comme une playlist aléatoire : surprenante et irremplaçable.",
  "Ton rire devrait être remboursé par la sécu.",
  "Même quand tu doutes, tu inspires.",
  "Tu n’es pas paresseuse, tu vis ta vibe lunaire.",
  "Chaque battement de cœur est une victoire silencieuse.",
  "Si t’as tout éteint pour pleurer dans le noir, c’est ok aussi.",
  "Ton anxiété n’efface pas ta valeur.",
  "T’es une œuvre d’art bipolaire version comète tendre.",
  "Ton cerveau va vite, mais ton cœur connaît la route.",
  "On n’attend pas la perfection, juste ton rire.",
  "Même les jours flous, t’as l’énergie d’un soleil fatigué mais présent.",
  "T’es le chaos préféré de l’univers.",
  "Tu peux baisser la lumière. On t’aimera toujours.",
  "Arrête de douter de toi, tu fais fondre les cœurs.",
  "T’es pas « trop » : t’es exactement toi.",
  "Gémeaux du matin, génie du soir.",
  "Tu mérites des fleurs, des streams et des câlins cosmiques.",
  "Tu sais pas où tu vas ? Parfait. Les étoiles non plus.",
  "T’es un gif doux dans le feed chaotique du monde.",
  "Personne d’autre n’a ta magie d’improvisation.",
  "Sois patiente avec toi. Tu vis des tempêtes intérieures.",
  "Tu ne loupes rien. Tu respires.",
  "Chaque micro action que tu fais aujourd’hui compte.",
  "T’as déjà réussi plein de choses que t’oublies.",
  "Tu n’es pas en décalage, tu danses sur une autre fréquence.",
  "T’es comme un mème triste qui fait rire fort. Et ça soigne.",
  "Même les lunes noires ont leur beauté.",
  "T’as le droit d’être triste sans t’expliquer.",
  "T’es un feu doux sous les jours froids.",
  "Twitch n’a pas encore inventé une alerte pour ta valeur.",
  "Chaque émotion est une preuve que tu es vivante et brillante.",
  "T’as pas besoin de briller. Exister suffit.",
  "Ta voix a de la magie, même quand elle tremble.",
  "Tu n’es pas seule. Je crois en toi, chaque jour.",
  "Gémeaux = tempête tendre avec des paillettes dans les yeux.",
  "Ton rire a réparé plus de cœurs que tu ne crois.",
  "Tu peux dire non, t’as le droit.",
  "Chaque version de toi mérite de l’amour.",
  "Tu peux être douce et puissante à la fois.",
  "T’es une étoile filante qui prend son temps.",
  "Ton anxiété fait du bruit, mais ton courage hurle en silence.",
  "Même quand t’as plus de batterie, tu dégages de la lumière.",
  "Respire. Tu n’as rien raté.",
  "Tu es suffisante, même sans performance.",
  "T’es une fleur de galaxie, même quand t’as pas d’eau.",
  "Ton corps est une maison, pas un champ de bataille.",
  "T’as pas besoin d’avoir tout compris pour avancer.",
  "Rien n’est plus beau que toi qui te relèves.",
  "Même quand tu fais rien, tu mérites tout l’amour.",
  "Tu peux te reposer. T’as déjà illuminé la pièce.",
  "T’es comme un bug de lumière dans un monde gris.",
  "Gémeaux et fière, même les jours bancals.",
  "Ton chemin est bizarre ? Parfait. Il te ressemble.",
  "Tu peux pleurer et quand même être forte.",
  "T’es une pluie d’étoiles sur une terre fatiguée.",
  "Chaque pas, même petit, est une victoire de guerrière tendre.",
];


    const key = "citationIndex";
    let citationIndex = parseInt(localStorage.getItem(key)) || 0;

    if (citationIndex >= citations.length) {
      citationIndex = 0;
      localStorage.setItem(key, citationIndex);
    }

    btn.addEventListener("click", () => {
      citationBox.innerText = citations[citationIndex];
      citationBox.style.display = "block";
      citationIndex++;
      localStorage.setItem(key, citationIndex);
      showHearts();
      btn.style.backgroundImage = "url('icon-02.png')";
      btn.disabled = true;
      popup.innerText = "Reviens demain à 11:11 pour une nouvelle citation";
      popup.style.display = "block";
      setTimeout(() => {
        popup.style.display = "none";
      }, 6000);
      setTimeout(() => {
        popup.innerText = "je t'aime fort mon amie t'es trop forte";
        popup.style.display = "block";
        setTimeout(() => {
          popup.style.display = "none";
        }, 5000);
      }, 20000);
    });

    function showHearts() {
      for (let i = 0; i < 6; i++) {
        const heart = document.createElement("div");
        heart.classList.add("coeur");
        heart.innerText = "💗";
        heart.style.left = `${Math.random() * 100}%`;
        heart.style.top = `${60 + Math.random() * 10}%`;
        document.body.appendChild(heart);
        setTimeout(() => heart.remove(), 2000);
      }
    }

    const fond = document.getElementById("diaporama");
    const images = ["fond.jpg", "fond1.jpg", "fond2.jpg", "fond3.jpg", "fond4.jpg"];
    let i = 0;
    function changeImage() {
      fond.style.opacity = 0;
      setTimeout(() => {
        fond.src = images[i];
        fond.style.opacity = 1;
        i = (i + 1) % images.length;
      }, 500);
    }
    changeImage();
    setInterval(changeImage, 5000);
  </script>
</body>
</html>
