# Pong-P5js

//Boleta
let xBoleta = 300;
let yBoleta = 200;
let diametro = 20;
let raio = diametro /2;

let velocidadeXboleta = 7;
let velocidadeYboleta = 7;

//Raqueta
let xRaqueta = 10
let yRaqueta = 150
let raquetaComprimento = 10
let raquetaAltura = 90

//A parte
let colider = false;

//Raqueta oponente
let xRaquetaO = 585;
let yRaquetaO = 150;
let velocidadeYOponente;

//Placar do jogo
let mP = 0;
let oP = 0;

//Sons(os)
let raquetadam;
let punto;
let musicly;

function preload(){
  musicly = loadSound("trilha.mp3")
  punto = loadSound("ponto.mp3")
  raquetadam = loadSound("raquetada.mp3")
}

function setup() {
  createCanvas(600, 400);
  musicly.loop();
}

function draw() {
    background(0);
    mostraBoleta();
    movimentaBoleta();
    verificaBoleta(); 
    mostraRaqueta(xRaqueta, yRaqueta);
    movimentoRaqueta();
    verificaRaqueta();
    verifycolisaoRaqueta(xRaqueta, yRaqueta);
    mostraRaqueta(xRaquetaO, yRaquetaO);
    movimentoRaquetaO();
    verifycolisaoRaqueta(xRaquetaO, yRaquetaO);
    placar();
    marcaPonto()
   
}

    function mostraBoleta(){
circle(xBoleta, yBoleta, diametro);
    }

    function movimentaBoleta(){
    xBoleta += velocidadeXboleta;
    yBoleta += velocidadeYboleta;
    }

    function verificaBoleta(){
      
     if (xBoleta + raio > width || xBoleta - raio < 0) {
    velocidadeXboleta *= -1;
}
    if (yBoleta + raio > height || yBoleta - raio < 0) {
    velocidadeYboleta *= -1;
}
    }

function mostraRaqueta(x,y){
   rect(x,y, raquetaComprimento, raquetaAltura);
}

   function movimentoRaqueta() {
    if (keyIsDown(87)) {
        yRaqueta -= 10;
    }
    if (keyIsDown(83)) {
        yRaqueta += 10;
    }
}

function verificaRaqueta(){
  if (xBoleta - raio < xRaqueta + raquetaComprimento && yBoleta - raio < yRaqueta + raquetaAltura && yBoleta + raio > yRaqueta){
    velocidadeXboleta *= -1;
    raquetadam.play();
  }
}

function verifycolisaoRaqueta(x, y){
  colider = collideRectCircle(x, y, raquetaComprimento, raquetaAltura, xBoleta, yBoleta, raio);
  if (colider){
    velocidadeXboleta *= -1;
    raquetadam.play();
  }
}
 
function movimentoRaquetaO(){
   if (keyIsDown(UP_ARROW)) {
        yRaquetaO -= 10;
    }
    if (keyIsDown(DOWN_ARROW)) {
        yRaquetaO += 10;
    }
}


function placar(){
  stroke(color(238,130,238))
  textAlign(CENTER);
  textSize(20);
  fill(color(148,0,211));
  rect(150, 10, 40, 20);
  fill(255);
  text(mP, 170, 26);
  fill(color(148,0,211));
  rect(450, 10, 40, 20);
  fill(255);
  text(oP,470,26);
}

function marcaPonto() {
    if (xBoleta > 590) {
        mP += 1;
        punto.play();
    }
    if (xBoleta < 10) {
        oP += 1;
        punto.play();
    }
}
