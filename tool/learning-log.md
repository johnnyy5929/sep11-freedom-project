# Tool Learning Log

## Tool: **Kaboom**

## Project: **Cooking game**

---

### 10/6/24:
Using kaboom for the first time,
So to start off I had to learn how to instead it first;
The code to instead kaboom is

`````js
<script type="module">

// import kaboom.js
import kaboom from "https://unpkg.com/kaboom@3000.0.1/dist/kaboom.mjs";

// initialize kaboom context
kaboom();

// add a piece of text at position (120, 80)
add([
    text("hello"),
    pos(120, 80),
]);

</script>
`````
This is one way of insteading, if you instead this way there will be text and you can change the sides of the background. 
![hi](Screenshot_6-10-2024_15712_jsbin.com.jpeg)

The other way of insteading it is the same but there aren't any words. 
````js
<script src="https://unpkg.com/kaboom@3000.0.1/dist/kaboom.js"></script>

<script>
    kaboom();
</script>
````
![hi](Screenshot_6-10-2024_15134_jsbin.com.jpeg)

So after doing my research on Kaboom I learned many things and combined them. So somethings that I added to this is sprite which is the character of this game. Another thing I added was const which makes everything the same. another example of this is 
`````js 
const Speed =320
`````

Another thing I learned was onKeyDown, which makes it so when one key is down something will happen. For example:

`````js
onKeyDown("left", () => {
	player.move(-SPEED, 0)
})

onKeyDown("right", () => {
	player.move(SPEED, 0)
})

onKeyDown("up", () => {
	player.move(0, -SPEED)
})

onKeyDown("down", () => {
	player.move(0, SPEED)
})

onKeyDown("q", () => {
	player.angle -= SPEED * dt()
})

onKeyDown("e", () => {
	player.angle += SPEED * dt()
})
`````
Another thing I added was add a sprite with a mass that you can move:
`````js
add([
	sprite("steel"),
	pos(100, 200),
	area(),
	// This will not be static, but have a big mass that's hard to push over
	body({ mass: 10 }),
])
`````
Last code I have for my tinkering is:
`````js
player.onCollide("enemy", (enemy) => {
	destroy(enemy)
})

// .onCollideUpdate() runs every frame when an object collides with another object
player.onCollideUpdate("enemy", () => {
})
`````

So combining all these codes I came up with a test paceman game:

`````Js 
// Collision handling

// Start kaboom
kaboom({
	scale: 2,
})

// Load assets
loadSprite("bean", "/sprites/bean.png")
loadSprite("ghosty", "/sprites/ghosty.png")
loadSprite("grass", "/sprites/grass.png")
loadSprite("steel", "/sprites/steel.png")

// Define player movement speed
const SPEED = 320

// Add player game object
const player = add([
	sprite("bean"),
	pos(80, 120),
	color(),
	rotate(0),

	area(),

	body(),
])


onKeyDown("left", () => {
	player.move(-SPEED, 0)
})

onKeyDown("right", () => {
	player.move(SPEED, 0)
})

onKeyDown("up", () => {
	player.move(0, -SPEED)
})

onKeyDown("down", () => {
	player.move(0, SPEED)
})

onKeyDown("q", () => {
	player.angle -= SPEED * dt()
})

onKeyDown("e", () => {
	player.angle += SPEED * dt()
})


for (let i = 0; i < 3; i++) {

	const x = rand(0, width())
	const y = rand(0, height())

	add([
		sprite("ghosty"),
		pos(x, y),
		area(),
		"enemy",
	])

}


add([
	sprite("steel"),
	pos(100, 200),
	area(),
	body({ mass: 10 }),
])

add([
	sprite("steel"),
	pos(100, 200),
	area(),
	body({ mass: 10 }),
])

add([
	sprite("steel"),
	pos(100, 200),
	area(),
	body({ mass: 10 }),
])
add([
	sprite("steel"),
	pos(250, 320),
	area(),
	body({ mass: 10 }),
])
add([
	sprite("steel"),
	pos(200, 300),
	area(),
	body({ mass: 10 }),
])
add([
	sprite("steel"),
	pos(300, 100),
	area(),
	body({ mass: 10 }),
])

add([
	sprite("steel"),
	pos(10, 200),
	area(),
	body({ mass: 10 }),
])
add([
	sprite("steel"),
	pos(150, 200),
	area(),
	body({ mass: 10 }),
])

add([
	sprite("steel"),
	pos(300, 50),
	area(),
	body({ mass: 10 }),
])


	destroy(enemy)
})

player.onCollideUpdate("enemy", () => {
})

player.onCollideEnd("grass", (a) => {
	debug.log("leave grass")
})

player.onClick(() => {
	debug.log("what up")
})

player.onUpdate(() => {
	hovered on
	if (player.isHovering()) {
		player.color = rgb(0, 0, 255)
	} else {
		player.color = rgb()
	}
})


debug.inspect = true

`````
![js](Screenshot_20-10-2024_192348_kaboomjs.com.jpeg)
So as you can see here I used all the code I needed for a fake pacman game. You can move and eat the ghost. This is what I did for LL1.



## 10/27/24
## LL2

I started to play around we the Ai in kaboom. You are able to make an enemy shot you. 
The code I had for this is 
`````js
const enemy = add([
	sprite("ghosty"),
	pos(width() - 80, height() - 80),
	anchor("center"),
	// This enemy cycle between 3 states, and start from "idle" state
	state("move", [ "idle", "attack", "move" ]),
	area(),
	body(),
])
`````
This adds an enemy into your game.
The next code I did was:
`````js
enemy.onStateEnter("idle", async () => {
	await wait(0.5)
	enemy.enterState("attack")
})

// When we enter "attack" state, we fire a bullet, and enter "move" state after 1 sec
enemy.onStateEnter("attack", async () => {

	// Don't do anything if player doesn't exist anymore
	if (player.exists()) {

		const dir = player.pos.sub(enemy.pos).unit()

		add([
			pos(enemy.pos),
			move(dir, BULLET_SPEED),
			rect(12, 12),
			area(),
			offscreen({ destroy: true }),
			anchor("center"),
			color(BLUE),
			"bullet",
		])

	}

	await wait(1)
	enemy.enterState("move")

})

enemy.onStateEnter("move", async () => {
	await wait(2)
	enemy.enterState("idle")
})
`````
This allows the enemy to shot at people and gave the shape of the bullet. 
These are the code I learned and I used them to make a fun game where you run around trying not to get hit.
The code for that is:

`````js
kaboom()

loadSprite("bean", "/sprites/bean.png")
loadSprite("ghosty", "/sprites/ghosty.png")
loadSprite("grass", "/sprites/grass.png")
const SPEED = 320
const ENEMY_SPEED = 160
const BULLET_SPEED = 800

const player = add([
	sprite("bean"),
	pos(80, 80),
	area(),
	anchor("center"),
	body(),
])

const enemy = add([
	sprite("ghosty"),
	pos(width() - 80, height() - 80),
	anchor("center"),
	state("move", [ "idle", "attack", "move" ]),
	area(),
	body(),
])

add([
	sprite("grass"),
	pos(100, 200),
	area(),
	body({ isStatic: true }),
	"grass",
	
])
add([
	sprite("grass"),
	pos(163, 200),
	area(),
	body({ isStatic: true }),
	"grass",
	
])

add([
	sprite("grass"),
	pos(163, 500),
	area(),
	body({ isStatic: true }),
	"grass",
	
])

add([
	sprite("grass"),
	pos(503, 500),
	area(),
	body({ isStatic: true }),
	"grass",
	
])

add([
	sprite("grass"),
	pos(703, 450),
	area(),
	body({ isStatic: true }),
	"grass",
	
])

add([
	sprite("grass"),
	pos(303, 450),
	area(),
	body({ isStatic: true }),
	"grass",
	
])

add([
	sprite("grass"),
	pos(230, 700),
	area(),
	body({ isStatic: true }),
	"grass",
	
])

add([
	sprite("grass"),
	pos(700, 100),
	area(),
	body({ isStatic: true }),
	"grass",
	
])

add([
	sprite("grass"),
	pos(500, 300),
	area(),
	body({ isStatic: true }),
	"grass",
	
])
add([
	sprite("grass"),
	pos(505, 300),
	area(),
	body({ isStatic: true }),
	"grass",
	
])

add([
	sprite("grass"),
	pos(545, 555),
	area(),
	body({ isStatic: true }),
	"grass",
	
])

add([
	sprite("grass"),
	pos(545, 705),
	area(),
	body({ isStatic: true }),
	"grass",
	
])
enemy.onStateEnter("idle", async () => {
	await wait(0.5)
	enemy.enterState("attack")
})


enemy.onStateEnter("attack", async () => {


	if (player.exists()) {

		const dir = player.pos.sub(enemy.pos).unit()

		add([
			pos(enemy.pos),
			move(dir, BULLET_SPEED),
			rect(12, 12),
			area(),
			offscreen({ destroy: true }),
			anchor("center"),
			color(BLUE),
			"bullet",
		])

	}

	await wait(1)
	enemy.enterState("move")

})

enemy.onStateEnter("move", async () => {
	await wait(2)
	enemy.enterState("idle")
})


enemy.onStateUpdate("move", () => {
	if (!player.exists()) return
	const dir = player.pos.sub(enemy.pos).unit()
	enemy.move(dir.scale(ENEMY_SPEED))
})


player.onCollide("bullet", (bullet) => {
	destroy(bullet)
	destroy(player)
	addKaboom(bullet.pos)
})


onKeyDown("left", () => {
	player.move(-SPEED, 0)
})

onKeyDown("right", () => {
	player.move(SPEED, 0)
})

onKeyDown("up", () => {
	player.move(0, -SPEED)
})

onKeyDown("down", () => {
	player.move(0, SPEED)
})
`````
![hi](Screenshot_27-10-2024_201135_kaboomjs.com.jpeg)


<!-- 
* Links you used today (websites, videos, etc)
* Things you tried, progress you made, etc
* Challenges, a-ha moments, etc
* Questions you still have
* What you're going to try next
-->


