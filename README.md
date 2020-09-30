var scene = createSprite(0,0,400,400);
scene.setAnimation( "sunshine_showers_1");
scene.x = scene.width/2;
scene.scale = 2.2;

var motu = createSprite(65,330,1,1);
motu.setAnimation("motu");
motu.visible=false;
motu.scale=0.4;
motu.setCollider("circle", 0,0,150);
//motu.debug = true; 

var patlu = createSprite(355,350,1,1);
patlu.setAnimation("patlu");
patlu.visible=false;
patlu.scale=0.4;   
patlu.setCollider("circle", 0,0,150);
//patlu.debug = true;

var chingum = createSprite(200,320,1,1);
chingum.setAnimation("chingum");
chingum.visible=false;
chingum.scale=1;   
chingum.setCollider("circle", 0,0,65);
//chingum.debug = true;
    
var ground=createSprite(400,400,800,10);
ground.visible=false;
var invisibleground=createSprite(100,100,800,10);
invisibleground.visible=false;

var play = createSprite(200,50,100,10);
play.setAnimation("play");

var settings = createSprite(200,380,10,10);
settings.setAnimation("settings"); 
settings.scale = 3;

var back1 = createSprite(200,225,10,10);
back1.setAnimation("motu patlu"); 

var back2 = createSprite(100,200,10,10);
back2.setAnimation("motu patlu");

var back = createSprite(390,30,10,10);
back.setAnimation("back"); 
back.scale = 0.5;

var back3 = createSprite(380,30,10,10);
back3.setAnimation("back"); 
back3.scale = 0.5;

var mountain = createSprite(50,200,20,20);
mountain.setAnimation( "rainbow_1");

var buildings = createSprite(190,200,20,20);
buildings.setAnimation("farm_land_1");

var meadows = createSprite(330,200,20,20);
meadows.setAnimation("santa_1");

var r = createSprite(400,60,10,10);
r.setAnimation("r");

var s= createSprite(280,70,10,10);
s.setAnimation("s");

var h = createSprite(120,40,10,10);
h.setAnimation("h");

var play1 = createSprite(220,90,100,10);
play1.setAnimation("play3");

var gameOver = createSprite(200,230,10,10);
gameOver.setAnimation("gameover");
gameOver.scale = 0.5;
gameOver.visible = false;

var start = createSprite(300,200,10,10);
start.setAnimation("start");
start.scale=0.2;

var restart = createSprite(200,150,10,10);
restart.setAnimation("restart");
restart.scale=0.3;
restart.visible = false;

var gameState = "menu";
var n = 0;
var s1=0;
var score=0 ;
var count=0;

var samosaGroup=createGroup();
var ideaGroup=createGroup();
var coconutGroup=createGroup();
var stoneGroup=createGroup();

var PLAY = 1;
var END = 0;
var gameSTATE = PLAY;

function draw() {
 if(n > 2449){ 
  gameState = "menu";
}

if (gameSTATE === PLAY) {
  
if(stoneGroup.isTouching(motu)){
gameSTATE = END;
}
if(stoneGroup.isTouching(patlu)){
gameSTATE = END;
}
if(stoneGroup.isTouching(chingum)){
gameSTATE = END;
}
}
 
else if(gameSTATE ===END){
stoneGroup.destroyEach();
samosaGroup.destroyEach();
ideaGroup.destroyEach();
coconutGroup.destroyEach();
    
stoneGroup.setVelocityXEach(0);
samosaGroup.setVelocityXEach(0);
ideaGroup.setVelocityXEach(0);
coconutGroup.setVelocityXEach(0);
scene.x = scene.width/0;



patlu.velocityY=-0.0;
chingum.velocityY=-0.0;
motu.velocityY=-0.0;

gameOver.visible = true;

restart.visible = true;
restart.scale=0.5;

if(keyWentDown("space")&&gameSTATE ==="END"){
gameState = "play"; 
}

  
  if(mousePressedOver(restart)) {
    reset();
  }

 
}
  
if(samosaGroup.isTouching(motu)){
score=score+1; 
}
if(ideaGroup.isTouching(patlu)){
count=count+1; 
}
if(coconutGroup.isTouching(chingum)){
s1=s1+1; 
}

motu.bounceOff(invisibleground); 
motu.collide(ground);
patlu.bounceOff(invisibleground); 
patlu.collide(ground);
chingum.bounceOff(invisibleground); 
chingum.collide(ground);
  
if(gameState == "menu"){
  
background("green");
start.display();
   
back2.display();
back2.scale = 0.8;
 
if(mouseIsOver(start)){
start.scale = 0.5;
}else{
start.scale = 0.5;
}

if(mousePressedOver(start)){
gameState ="start";
}
}

if(gameState == "start"){
  
background("green");
play.display();
play.scale=0.8;

play1.display();
play1.scale=2;

settings.display();

back1.display();
 
if(mouseIsOver(play1)){
play1.scale = 1.2;
}else{
play1.scale = 1;
}

if(mousePressedOver(play1)){
gameState = "play1";
}
 
if(mouseIsOver(play)){
play.scale = 0.8;
}else{
play.scale = 0.8;
}
   
if(mousePressedOver(play)){
gameState = "game";
}
if(mousePressedOver(r)){
gameState = "play";
}
    
if(mousePressedOver(back)){
gameState = "start";
}
    
if(mousePressedOver(settings)){
gameState = "settings";
}
}

if(mouseIsOver(settings)){
settings.scale = 1;
}else{
settings.scale = 0.8;
}

if(gameState == "play1"){
  
background("green");

fill(230,mouseX,mouseY);
stroke(0);
strokeWeight(0);
textSize(30);
textFont("Comic Sans Sherif");   

text("how to play game :-",80,30);
text("1) click play you see 3 animations",5,60);
text("2)click h button motu will jump",5,90);
text("click s button motu and ",5,125);
text("chingum will jump",5,155);
text("3)click r button patlu and ",5,190);
text("chingum will jump",5,220);
text("3)when chingum is touching to ",5,250);
text("coconut score will increase",5,270);
text("4)when motu is touching to",5,300);
text("samosa score will increase",5,325);
text("4)when patlu is touching to",5,350);
text("idea score will increase",5,375);
 
back.display();
back.x = 50;
    
if(mousePressedOver(back)){
gameState = "start";
}
}
  
if(gameState == "settings"){

background("green");

mountain.display();
mountain.scale = 0.2;
mountain.visible = true;

buildings.display();
buildings.scale  = 0.25;
buildings.visible = true;
meadows.display();
meadows.scale = 0.25;
meadows.visible = true;

fill(230,mouseX,mouseY);
stroke(0);
strokeWeight(0);
textSize(30);
textFont("Comic Sans Sherif");   

text("CHANGE THE GAME",100,40);
text("BACKGROUND IMAGE TO - ",10,80);
text("Click over the image to continue*",5,350);
    
back.display();
back.x = 50;
   
if(mousePressedOver(back)){
gameState == "start";
}

if(mousePressedOver(mountain)){
scene.setAnimation("rainbow_1");
}

if(mousePressedOver(buildings)){
scene.setAnimation("farm_land_1");
}

if(mousePressedOver(meadows)){
scene.setAnimation("santa_1");
}
  
  }
  
if(gameState === "game"){
chingum.visible=true;
motu.visible=true;
patlu.visible=true;
start.visible=false;

if(mousePressedOver(r)){
patlu.velocityY=-20;

}

if(mousePressedOver(s)){
chingum.velocityY=-20;
}

if(mousePressedOver(h)){
motu.velocityY=-20;
}
 
background("green");
   
back1.visible=false;
back2.visible=false;

scene.visible = true;

play.visible = false;
play1.visible = false;

settings.visible = false;

mountain.visible = false;
buildings.visible = false;
meadows.visible = false;

back3.visible=false;

back.x = 25;


spawnstone();
spawnsamosa();
spawnidea();
drawSprites();
spawncoconut();


fill(230,mouseX,mouseY);
textFont("Comic Sans Sherif");
textSize(20);

text("Samosa :"+score,50,80); 
scene.velocityX = -9;  

fill(230,mouseX,mouseY);
textFont("Comic Sans Sherif");
textSize(20);

text("idea :"+count,330,80); 
scene.velocityX = -9;

fill(230,mouseX,mouseY);
textSize(20);
textFont("Comic Sans Sherif");
text("coconut  :"+s1,180,80); 

scene.velocityX = -9;

if(scene.x < 0){
scene.x = scene.width/2;
}
  

}            
 
if(mousePressedOver(back))  {
gameState = "start";
back1.visible=true;
start.visible=true;
play.visible = true;
play1.visible = true;
settings.visible = true;
}

if(mousePressedOver(play))  {
gameState = "game";
}

console.log(n);

 }
function reset(){
  
  gameSTATE = PLAY;
  gameOver.visible = false;
  restart.visible = false;
  
  motu.velocityY=-50;
  patlu.velocityY=-50;
  chingum.velocityY=-50;
  stoneGroup.destroyEach();
samosaGroup.destroyEach();
ideaGroup.destroyEach();
coconutGroup.destroyEach();
    
stoneGroup.setVelocityXEach(0);
samosaGroup.setVelocityXEach(0);
ideaGroup.setVelocityXEach(0);
coconutGroup.setVelocityXEach(0);
  
  motu.setAnimation("motu");
   patlu.setAnimation("patlu");
   n = 0;
   s1=0;
   score=0 ;
 count=0;
}

function spawnsamosa(){
  
if (World.frameCount % 150 === 0) {
var samosa = createSprite(400,320,40,10);
samosa.y = randomNumber(150,150);
samosa.setAnimation("samosa");
samosa.velocityX = -6;
samosa.lifetime = 134;
samosa.scale = 0.5;
samosaGroup.add(samosa);
  
}
}
    
function spawnidea(){
  
if (World.frameCount % 200 === 0) {
var idea = createSprite(400,320,40,10);
idea.y = randomNumber(150,150);
idea.setAnimation("idea");
idea.velocityX = -6;
idea.lifetime = 134;
idea.scale = 1;
ideaGroup.add(idea);

}
}
    
function spawncoconut(){
  
if (World.frameCount % 250 === 0) {
var coconut = createSprite(400,320,40,10);
coconut.y = randomNumber(150,150);
coconut.setAnimation("coconut");
coconut.velocityX = -10;
coconut.lifetime = 134;
coconut.scale = 1;
coconutGroup.add(coconut);

}
}
function spawnstone(){
  
if (World.frameCount % 300 === 0) {
var stone = createSprite(400,320,40,10);
stone.y = randomNumber(380,380);
stone.setAnimation("stone");
stone.velocityX = -10;
stone.lifetime = 134;
stone.scale = 0.5;
stoneGroup.add(stone);

}
}
