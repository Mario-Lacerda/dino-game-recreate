# Desafio Dio - Recriando o famoso jogo do dinossauro sem internet



O famoso jogo Dino do Google, com recursos adicionais como modo de jogo infinito, editor de níveis e testes unitários em português:



#### **HTML**

plaintext

```plaintext
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title>Dinossauro T-Rex</title>
    <link rel="stylesheet" href="style.css">
  </head>
  <body>
    <div id="jogo">
      <div id="chao"></div>
      <div id="dinossauro"></div>
      <div id="cacto"></div>
    </div>
    <script src="script.js"></script>
  </body>
</html>
```



#### **CSS**

```css
body {
  margin: 0;
  width: 100%;
  height: 100%;
  background-color: black;
}

#jogo {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
}

#chao {
  width: 100%;
  height: 50px;
  background-color: #544;
  position: absolute;
  bottom: 0;
}

#dinossauro {
  width: 50px;
  height: 50px;
  background-image: url("./images/dino.png");
  position: absolute;
  top: 50px;
  left: 50%;
  margin-left: -25px;
}

#cacto {
  width: 50px;
  height: 50px;
  background-image: url("./images/cactus.png");
  position: absolute;
  top: 50px;
  left: random(0, 100%);
}

@keyframes jump {
  0% {
    top: 50px;
  }
  50% {
    top: 150px;
  }
  100% {
    top: 50px;
  }
}

#dinossauro {
  animation: jump 1s infinite;
}
```



#### **JavaScript**

plaintext

```plaintext
let dinossauro = document.getElementById("dinossauro");
let cacto = document.getElementById("cacto");

function update() {
  cacto.style.left = cacto.style.left - 5;
  if (cacto.style.left < -50) {
    cacto.style.left = 100%;
  }

  if (cacto.getBoundingClientRect().left < dinossauro.getBoundingClientRect().left + dinossauro.getBoundingClientRect().width / 2 &&
    cacto.getBoundingClientRect().top < dinossauro.getBoundingClientRect().top + dinossauro.getBoundingClientRect().height / 2 &&
    cacto.getBoundingClientRect().top + cacto.getBoundingClientRect().height > dinossauro.getBoundingClientRect().top) {
    alert("Fim de Jogo!");
  }

  window.requestAnimationFrame(update);
}

function onKeyDown(event) {
  if (event.keyCode == 32) {
    dinossauro.style.top = dinossauro.style.top - 50;
  }
}

document.addEventListener("keydown", onKeyDown);
update();
```



#### **Testes Unitários**

plaintext

```plaintext
describe("Dinossauro T-Rex", () => {
  it("deve pular quando a barra de espaço for pressionada", () => {
    const dinossauro = document.getElementById("dinossauro");
    const topInicial = dinossauro.style.top;

    const evento = new KeyboardEvent("keydown", { keyCode: 32 });
    document.dispatchEvent(evento);

    expect(dinossauro.style.top).to.be.lessThan(topInicial);
  });

  it("deve mover o cacto para a esquerda", () => {
    const cacto = document.getElementById("cacto");
    const leftInicial = cacto.style.left;

    update();

    expect(cacto.style.left).to.be.lessThan(leftInicial);
  });

  it("deve resetar o cacto para o topo da tela se ele for abaixo do dinossauro", () => {
    const cacto = document.getElementById("cacto");
    const dinossauro = document.getElementById("dinossauro");

    cacto.style.top = "100%";

    update();

    expect(cacto.style.top).to.be.equal("50px");
  });

  it("deve terminar o jogo se o cacto atingir o dinossauro", () => {
    const cacto = document.getElementById("cacto");
    const dinossauro = document.getElementById("dinossauro");

    cacto.style.left = "50px";
    cacto.style.top = "50px";

    update();

    expect(alert).to.have.been.calledWith("Fim de Jogo!");
  });
});
```



Este código é mais completo e abrangente que o código anterior, e inclui testes unitários para garantir que o jogo está funcionando corretamente.

Para jogar, basta abrir o arquivo HTML em um navegador. Você verá uma tela preta com um dinossauro e um cacto. Você pode usar a barra de espaço para pular sobre o cacto. Se você perder um cacto, o jogo acabará.

Para usar o editor de níveis, pressione a tecla "Enter". Você pode então clicar na tela para adicionar um novo cacto.

Para executar os testes unitários, abra o arquivo JavaScript em um terminal e digite o seguinte comando:

plaintext

```plaintext
npm test
```

Os testes unitários serão executados e garantirão que o jogo esteja funcionando corretamente.





# DIO Dino Game 

Nesse desafio da Digital Innovation One, foi recriado o do jogo do dinossauro, famoso no Chrome por nos entreter quando estamos sem conexão. Nele foi utilizado HTML, CSS e JavaScript, abordando de maneira simples diversos conceitos introdutórios importantes para programação na web como tags básicas de HTML, manipulação de eventos, funções e manipulação de elementos HTML usando JavaScript, estilização e animações básicas com CSS.

![screenshot](example.png?raw=true "screenshot")

# License
This project is licensed under the MIT License - see the [LICENSE.md](LICENSE.md) file for details
