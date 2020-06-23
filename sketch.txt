var helicopterIMG, helicopterSprite, packageSprite,packageIMG;
var packageBody,ground,boxB,boxL,boxR;
var boxLeft,boxRight,boxBottom;
const Engine = Matter.Engine;
const World = Matter.World;
const Bodies = Matter.Bodies;
const Body = Matter.Body;

function preload()
{
	helicopterIMG=loadImage("helicopter.png")
	packageIMG=loadImage("package.png")
}

function setup() {
	createCanvas(800, 700);
	rectMode(CENTER);
	

	packageSprite=createSprite(width/2, 80, 10,10);
	packageSprite.addImage(packageIMG)
	packageSprite.scale=0.2
  
	helicopterSprite=createSprite(width/2, 200, 10,10);
	helicopterSprite.addImage(helicopterIMG)
	helicopterSprite.scale=0.6

	groundSprite=createSprite(width/2, height-35, width,10);
	groundSprite.shapeColor=color(255)

	boxBottom=createSprite(350,710,200,20);
	boxRight=createSprite(650,100,20,100);
	boxLeft=createSprite(650,100,20,100);
	
	engine = Engine.create();
	world = engine.world;

	packageBody = Bodies.circle(width/2 , 200 , 5 , {restitution:1.5, isStatic:true});
	World.add(world, packageBody);
	
	boxB = Bodies.rectangle(400,650,200,20,{isStatic:true});
	World.add(world, boxB)
	boxL  = Bodies.rectangle(500,600,20,100,{isStatic:true});
	World.add(world, boxL)
	boxR  = Bodies.rectangle(300,600,20,100,{isStatic:true});
	World.add(world, boxR)
	//Create a Ground
	ground = Bodies.rectangle(width/2, 650, width, 10 , {isStatic:true} );
 	World.add(world, ground);


	Engine.run(engine);
  
}


function draw() {
  rectMode(CENTER);
  background(0);
  packageSprite.x= packageBody.position.x 
  packageSprite.y= packageBody.position.y
  packageBody.restitution = 0.5 
  boxBottom.x = boxB.position.x 
  boxBottom.y = boxB.position.y
  boxLeft.x = boxL.position.x 
  boxLeft.y = boxL.position.y
  boxRight.x = boxR.position.x 
  boxRight.y = boxR.position.y
  boxBottom.shapeColor="red";
  boxLeft.shapeColor="red";
  boxRight.shapeColor="red";
  boxB.isStatic = true
  boxL.isStatic = true
  boxR.isStatic = true
  drawSprites();
  keyPressed();
}

function keyPressed() {
 if (keyCode === DOWN_ARROW) {
    Matter.Body.setStatic(packageBody,false);
    
  }
}