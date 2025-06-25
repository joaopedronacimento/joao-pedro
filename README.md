# joao-pedro
const story = {
    start: {
        text: "Você se encontra em uma encruzilhada em uma floresta escura. Para onde você vai?",
        choices: [
            { text: "Seguir o caminho à esquerda.", next: "leftPath" },
            { text: "Seguir o caminho à direita.", next: "rightPath" }
        ]
    },
    leftPath: {
        text: "Você encontra um rio caudaloso. Há uma ponte quebrada e um barco velho. O que você faz?",
        choices: [
            { text: "Tentar consertar a ponte.", next: "fixBridge" },
            { text: "Tentar usar o barco.", next: "useBoat" }
        ]
    },
    rightPath: {
        text: "Você entra em uma clareira e vê uma caverna escura. Você ouve ruídos estranhos vindos de lá. O que você faz?",
        choices: [
            { text: "Entrar na caverna.", next: "enterCave" },
            { text: "Ignorar a caverna e procurar outro caminho.", next: "anotherPath" }
        ]
    },
    fixBridge: {
        text: "Você conseguiu consertar a ponte! Do outro lado, você encontra um tesouro escondido. Você venceu!",
        choices: [] // Fim da história
    },
    useBoat: {
        text: "O barco estava podre e afundou. Você não conseguiu atravessar o rio. Fim de jogo.",
        choices: [] // Fim da história
    },
    enterCave: {
        text: "Você encontra um urso dormindo! Você faz muito barulho e ele acorda. Fim de jogo.",
        choices: [] // Fim da história
    },
    anotherPath: {
        text: "Você encontra um caminho secreto que leva a um vilarejo pacífico. Você vive feliz para sempre. Você venceu!",
        choices: [] // Fim da história
    }
};

let currentScene = "start"; // Começa a aventura na cena inicial

const storyTextElement = document.getElementById("story-text");
const choicesElement = document.getElementById("choices");
const restartButton = document.getElementById("restart-button");

function startGame() {
    currentScene = "start";
    restartButton.classList.add("hidden");
    updateScene();
}

function updateScene() {
    const scene = story[currentScene];
    storyTextElement.textContent = scene.text;
    choicesElement.innerHTML = ""; // Limpa as escolhas anteriores

    if (scene.choices.length > 0) {
        scene.choices.forEach(choice => {
            const button = document.createElement("button");
            button.classList.add("choice-button");
            button.textContent = choice.text;
            button.addEventListener("click", () => choose(choice.next));
            choicesElement.appendChild(button);
        });
    } else {
        // Se não houver escolhas, é o fim da história
        restartButton.classList.remove("hidden");
    }
}

function choose(nextScene) {
    currentScene = nextScene;
    updateScene();
}

restartButton.addEventListener("click", startGame);

startGame(); // Inicia o jogo quando a página carrega
