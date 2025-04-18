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

I started to play around the Ai in kaboom. You are able to make an enemy shoot you. 
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
This allows the enemy to shoot at people and gives the shape of the bullet. 
These are the codes I learned and I used them to make a fun game where you run around trying not to get hit.
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
As you can see the blue thing is the bullet and the ghost is shooting it. So this is what I did for LL2 and a game where you run around until he kills you. I will probably make this better and more fun for the future. Where you have to fight a boss to shoot at you. This is something I will do later for LL3.


### LL3
### 11/10/24

I learned a little bit of code for LL3. The first code I learned  for LL3 is.
`````
player.onGround(() => {
	debug.log("ouch")
})
`````
What this does is allow a text to pop up when you touch the ground. Another code I learned is
`````
onKeyPress("space", () => {
	if (player.isGrounded()) {
		player.jump(JUMP_FORCE)
		player.play("jump")
	}
})
`````
When you jump on the top left it will show you jump. Another code is
`````
	anims: {
		"idle": {
			// Starts from frame 0, ends at frame 3
			from: 0,
			to: 3,
			// Frame per second
			speed: 5,
			loop: true,
		},
		"run": {
			from: 4,
			to: 7,
			speed: 10,
			loop: true,
		},
		// This animation only has 1 frame
		"jump": 8,
	},
})
`````
What this code does is that when there is idle the frame will be an amount, if it is jump it will be 8 and if you are running it between 4-7.

![hi](Screenshot_3-11-2024_193255_kaboomjs.com.jpeg)
As you can see it shows that the frame is 8 and that the character is jumping.

![j](Screenshot_3-11-2024_193246_kaboomjs.com.jpeg)
As you can see in this, it shows that it is idle and the frame is 0-4 and that it says ouch after they touch the ground. These were the codes I learned for LL3 and I will be learning more for LL4.

# LL4
## 11/24/24

For LL4 I was able to make levels. The code for this is.
`````js
	const characters = {
		"a": {
			sprite: "bag",
			msg: "Hi Bean! You should get that key!",
		},
		"b": {
			sprite: "ghosty",
			msg: "Who are you? You can see me??",
		},
	}
`````
So This code makes it so you can talk to people in the levels and what they say.


`````js
	// level layouts
	const levels = [
		[
			"===|====",
			"=      =",
			"= $    =",
			"=    a =",
			"=      =",
			"=   @  =",
			"========",
		],
		[
			"--------",
			"-      -",
			"-   $  -",
			"|      -",
			"-    b -",
			"-  @   -",
			"--------",
		],
		[		
			"========",
		    "=      =",
			"= $    =",
			"=    a =",
			"|      =",
			"=   @  =",
			"========",
		],
	]

	const level = addLevel(levels[levelIdx], {
		tileWidth: 64,
		tileHeight: 64,
		pos: vec2(64, 64),
		tiles: {
			"=": () => [
				sprite("grass"),
				area(),
				body({ isStatic: true }),
				anchor("center"),
			],
			"-": () => [
				sprite("steel"),
				area(),
				body({ isStatic: true }),
				anchor("center"),
			],
			"$": () => [
				sprite("key"),
				area(),
				anchor("center"),
				"key",
			],
			"@": () => [
				sprite("bean"),
				area(),
				body(),
				anchor("center"),
				"player",
			],
			"|": () => [
				sprite("door"),
				area(),
				body({ isStatic: true }),
				anchor("center"),
				"door",
			],
		},
  `````
this code makes it so we give something a variable and make it connect back to the levels. We can give them width and height. We make an outline for everything and use the symbols to give it a value. like - is steel and other stuff is different sprite.

The whole code is:
```````js
// simple rpg style walk and talk

kaboom({
	background: [74, 48, 82],
})

loadSprite("bag", "/sprites/bag.png")
loadSprite("ghosty", "/sprites/ghosty.png")
loadSprite("grass", "/sprites/grass.png")
loadSprite("steel", "/sprites/steel.png")
loadSprite("door", "/sprites/door.png")
loadSprite("key", "/sprites/key.png")
loadSprite("bean", "/sprites/bean.png")

scene("main", (levelIdx) => {

	const SPEED = 320

	// character dialog data
	const characters = {
		"a": {
			sprite: "bag",
			msg: "Hi Bean! You should get that key!",
		},
		"b": {
			sprite: "ghosty",
			msg: "Who are you? You can see me??",
		},
	}

	// level layouts
	const levels = [
		[
			"===|====",
			"=      =",
			"= $    =",
			"=    a =",
			"=      =",
			"=   @  =",
			"========",
		],
		[
			"--------",
			"-      -",
			"-   $  -",
			"|      -",
			"-    b -",
			"-  @   -",
			"--------",
		],
		[		
			"========",
		    "=      =",
			"= $    =",
			"=    a =",
			"|      =",
			"=   @  =",
			"========",
		],
	]

	const level = addLevel(levels[levelIdx], {
		tileWidth: 64,
		tileHeight: 64,
		pos: vec2(64, 64),
		tiles: {
			"=": () => [
				sprite("grass"),
				area(),
				body({ isStatic: true }),
				anchor("center"),
			],
			"-": () => [
				sprite("steel"),
				area(),
				body({ isStatic: true }),
				anchor("center"),
			],
			"$": () => [
				sprite("key"),
				area(),
				anchor("center"),
				"key",
			],
			"@": () => [
				sprite("bean"),
				area(),
				body(),
				anchor("center"),
				"player",
			],
			"|": () => [
				sprite("door"),
				area(),
				body({ isStatic: true }),
				anchor("center"),
				"door",
			],
		},
		// any() is a special function that gets called everytime there's a
		// symbol not defined above and is supposed to return what that symbol
		// means
		wildcardTile(ch) {
			const char = characters[ch]
			if (char) {
				return [
					sprite(char.sprite),
					area(),
					body({ isStatic: true }),
					anchor("center"),
					"character",
					{ msg: char.msg },
				]
			}
		},
	})

	// get the player game obj by tag
	const player = level.get("player")[0]

	function addDialog() {
		const h = 160
		const pad = 16
		const bg = add([
			pos(0, height() - h),
			rect(width(), h),
			color(0, 0, 0),
			z(100),
		])
		const txt = add([
			text("", {
				width: width(),
			}),
			pos(0 + pad, height() - h + pad),
			z(100),
		])
		bg.hidden = true
		txt.hidden = true
		return {
			say(t) {
				txt.text = t
				bg.hidden = false
				txt.hidden = false
			},
			dismiss() {
				if (!this.active()) {
					return
				}
				txt.text = ""
				bg.hidden = true
				txt.hidden = true
			},
			active() {
				return !bg.hidden
			},
			destroy() {
				bg.destroy()
				txt.destroy()
			},
		}
	}

	let hasKey = false
	const dialog = addDialog()

	player.onCollide("key", (key) => {
		destroy(key)
		hasKey = true
	})

	player.onCollide("door", () => {
		if (hasKey) {
			if (levelIdx + 1 < levels.length) {
				go("main", levelIdx + 1)
			} else {
				go("win")
			}
		} else {
			dialog.say("you got no key!")
		}
	})

	// talk on touch
	player.onCollide("character", (ch) => {
		dialog.say(ch.msg)
	})

	const dirs = {
		"left": LEFT,
		"right": RIGHT,
		"up": UP,
		"down": DOWN,
	}

	for (const dir in dirs) {
		onKeyPress(dir, () => {
			dialog.dismiss()
		})
		onKeyDown(dir, () => {
			player.move(dirs[dir].scale(SPEED))
		})
	}

})

scene("win", () => {
	add([
		text("You Win!"),
		pos(width() / 2, height() / 2),
		anchor("center"),
	])
})

go("main", 0)
```````






![](Screenshot_24-11-2024_192014_kaboomjs.com.jpeg)
![](Screenshot_24-11-2024_192024_kaboomjs.com.jpeg)
![](Screenshot_24-11-2024_192034_kaboomjs.com.jpeg)

This is what I did for LL4. We made a RPG game where you can explore and talk to the npc and roam.


## LL5
## 12/8/24

Just like css where you have things like hover, in java and in kaboom there is a code where you hover. There are many ways of using this. Where when you hover it will go forever or when you hover it will run once. These are cool things we can do. The code for this is:

`````js

// Only runs once when bean is hovered, and when bean is unhovered
redBean.onHover(() => {
	debug.log("red bean hovered")

	redBean.color = GREEN
})
redBean.onHoverEnd(() => {
	debug.log("red bean unhovered")

	redBean.color = BLUE
})

// Runs every frame when blue bean is hovered
blueBean.onHoverUpdate(() => {
	const t = time() * 10
	blueBean.color = rgb(
		wave(0, 255, t),
		wave(0, 255, t + 2),
		wave(0, 255, t + 4),
	)
`````
These are the two codes we can use.

We can use this with a sprite to make a color changing thing when you put your mouse over it.

The whole code is:
`````js
// Differences between onHover and onHoverUpdate

kaboom({
	// Use logMax to see more messages on debug.log()
	logMax: 5,
})

loadSprite("bean", "/sprites/bean.png")

add([
	text("onHover()\nonHoverEnd()"),
	pos(80, 80),
])

add([
	text("onHoverUpdate()"),
	pos(340, 80),
])

const redBean = add([
	sprite("bean"),
	color(RED),
	pos(130, 180),
	anchor("center"),
	area(),
])

const blueBean = add([
	sprite("bean"),
	color(BLUE),
	pos(380, 180),
	anchor("center"),
	area(),
])

// Only runs once when bean is hovered, and when bean is unhovered
redBean.onHover(() => {
	debug.log("red bean hovered")

	redBean.color = GREEN
})
redBean.onHoverEnd(() => {
	debug.log("red bean unhovered")

	redBean.color = BLUE
})

// Runs every frame when blue bean is hovered
blueBean.onHoverUpdate(() => {
	const t = time() * 10
	blueBean.color = rgb(
		wave(0, 255, t),
		wave(0, 255, t + 2),
		wave(0, 255, t + 4),
	)

	debug.log("blue bean on hover")
})
`````
![j](Screenshot_8-12-2024_163429_kaboomjs.com.jpeg)
![k](Screenshot_8-12-2024_163440_kaboomjs.com.jpeg)
These are the two different hovers used. It is really cool. This is what my LL5 was about. Thank you




// LL6
// 12/30/24

So for LL6 I was working with my partner Katherine where I made an outline and she coded the outline to the best of her ability. So the plan I made is below. 

![i](tool/Screenshot_30-12-2024_13517_docs.google.com.jpeg)

As you can see this is the plan I made where it is a prototype of our game. It isn't fully done yet but there will be different levels where you can do different things you can go back or keep going. 

The other thing I did was learn how to make npc and be able to talk to them. So I wrote a code on my ide since before I was just using the website now. I am going to do everything on my ide.
So what I did which you can see below is a code that allows you to talk to people and you can press space and it keeps talking.

`````js

kaboom({
	background: [ 255, 209, 253 ],
})

loadSprite("bean", "/sprites/../person.png")
loadSprite("mark", "/sprites/../women.png")

// Define the dialogue data
const dialogs = [
	[ "bean", "hi my butterfly" ],
	[ "bean", "i love u" ],
	[ "bean", "you love me? pretty baby" ],
	[ "bean", "he did not know how to take care of you..." ],
	[ "mark", "you don't know me ..." ],
	[ "bean", "what! baby???" ],
	[ "mark", "oh...hi " ],
]

let curDialog = 0

// Text bubble
const textbox = add([
	rect(width() - 200, 120, { radius: 32 }),
	anchor("center"),
	pos(center().x, height() - 100),
	outline(4),
])

// Text
const txt = add([
	text("", { size: 32, width: width() - 230, align: "center" }),
	pos(textbox.pos),
	anchor("center"),
	color(0, 0, 0),
])

// Character avatar
const avatar = add([
	sprite("bean"),
	scale(3),
	anchor("center"),
	pos(center().sub(0, 50)),
])

onKeyPress("space", () => {
	// Cycle through the dialogs
	curDialog = (curDialog + 1) % dialogs.length
	updateDialog()
})

// Update the on screen sprite & text
function updateDialog() {

	const [ char, dialog ] = dialogs[curDialog]

	// Use a new sprite component to replace the old one
	avatar.use(sprite(char))
	// Update the dialog text
	txt.text = dialog

}

updateDialog()


`````


![](women.png)
![](hi.png)

As you can see here the people can talk to each other and when you press space it keeps going. What I want to do next is make it so that I get to pick between options and the computer will respond depending on what you pick. This is my plan for LL7 and I will make it so computers come and go. This would be really cool. Also I will need to add a way to have different people join. These are the plans for the future and for my other LL. Thank you


LL9
3/8/25

So for this LL we learned how to move with a mouse. So what I mean by this is when you click your character will move to the place you click to. This is cool for those who don't like arrow keys. I was going to add this as a way of moving. So the code I learned is this:

```` js
// Tweeeeeening!

kaboom({
	background: [141, 183, 255],
})

loadSprite("bean", "/sprites/bean.png")

const duration = 1
const easeTypes = Object.keys(easings)
let curEaseType = 0

const bean = add([
	sprite("bean"),
	pos(center()),
	rotate(0),
	anchor("center"),
])

const label = add([
	text(easeTypes[curEaseType], { size: 64 }),
	pos(24, 24),
])

add([
	text("Click anywhere & use arrow keys", { width: width() }),
	anchor("botleft"),
	pos(24, height() - 24),
])

onKeyPress("left", () => {
	curEaseType = curEaseType === 0 ? easeTypes.length - 1 : curEaseType - 1
	label.text = easeTypes[curEaseType]
})

onKeyPress("right", () => {
	curEaseType = (curEaseType + 1) % easeTypes.length
	label.text = easeTypes[curEaseType]
})

let curTween = null

onMousePress(() => {
	const easeType = easeTypes[curEaseType]
	// stop previous lerp, or there will be jittering
	if (curTween) curTween.cancel()
	// start the tween
	curTween = tween(
		// start value (accepts number, Vec2 and Color)
		bean.pos,
		// destination value
		mousePos(),
		// duration (in seconds)
		duration,
		// how value should be updated
		(val) => bean.pos = val,
		// interpolation function (defaults to easings.linear)
		easings[easeType],
	)
})
`````
As you can see in this code there is a thing called Onpress which makes it so when you press down it will move. So when I press down it will move the character.
![](Screenshot_8-3-2025_191636_kaboomjs.com.jpeg)
![](Screenshot_8-3-2025_191659_kaboomjs.com.jpeg)
As you can see you can move and use arrows or press to move. We are going to use this for the project so it was good to know. This is what I have done for LL9 and going to do more.

LL10
3/23/25

So LL10 I made a code where you fight against people it is like a RPG game where you explore and you kill monsters for stuff and you can cook with the stuff was idea. So I made a game where you can start fighting aginst people and you get stuff for it. 

```` js
kaboom({
	scale: 4,
	background: [0, 0, 0],
})

// Load sprite atlas
loadSpriteAtlas("/examples/sprites/dungeon.png", {
	"hero": {
		"x": 128,
		"y": 196,
		"width": 144,
		"height": 28,
		"sliceX": 9,
		"anims": {
			"idle": {
				"from": 0,
				"to": 3,
				"speed": 3,
				"loop": true,
			},
			"run": {
				"from": 4,
				"to": 7,
				"speed": 10,
				"loop": true,
			},
			"hit": 8,
		},
	},
	"ogre": {
		"x": 16,
		"y": 320,
		"width": 256,
		"height": 32,
		"sliceX": 8,
		"anims": {
			"idle": {
				"from": 0,
				"to": 3,
				"speed": 3,
				"loop": true,
			},
			"run": {
				"from": 4,
				"to": 7,
				"speed": 10,
				"loop": true,
			},
		},
	},
	"floor": {
		"x": 16,
		"y": 64,
		"width": 48,
		"height": 48,
		"sliceX": 3,
		"sliceY": 3,
	},
	"chest": {
		"x": 304,
		"y": 304,
		"width": 48,
		"height": 16,
		"sliceX": 3,
		"anims": {
			"open": {
				"from": 0,
				"to": 2,
				"speed": 20,
				"loop": false,
			},
			"close": {
				"from": 2,
				"to": 0,
				"speed": 20,
				"loop": false,
			},
		},
	},
	"sword": {
		"x": 322,
		"y": 81,
		"width": 12,
		"height": 30,
	},
	"wall": {
		"x": 16,
		"y": 16,
		"width": 16,
		"height": 16,
	},
	"wall_top": {
		"x": 16,
		"y": 0,
		"width": 16,
		"height": 16,
	},
	"wall_left": {
		"x": 16,
		"y": 128,
		"width": 16,
		"height": 16,
	},
	"wall_right": {
		"x": 0,
		"y": 128,
		"width": 16,
		"height": 16,
	},
	"wall_topleft": {
		"x": 32,
		"y": 128,
		"width": 16,
		"height": 16,
	},
	"wall_topright": {
		"x": 48,
		"y": 128,
		"width": 16,
		"height": 16,
	},
	"wall_botleft": {
		"x": 32,
		"y": 144,
		"width": 16,
		"height": 16,
	},
	"wall_botright": {
		"x": 48,
		"y": 144,
		"width": 16,
		"height": 16,
	},
})

// Floor
addLevel([
	"xxxxxxxxxx",
	"          ",
	"          ",
	"          ",
	"          ",
	"          ",
	"          ",
	"          ",
	"          ",
	"          ",
], {
	tileWidth: 16,
	tileHeight: 16,
	tiles: {
		" ": () => [
			sprite("floor", { frame: ~~rand(0, 8) }),
		],
	},
})

// Objects
const map = addLevel([
	"tttttttttt",
	"cwwwwwwwwd",
	"l        r",
	"l        r",
	"l        r",
	"l      $ r",
	"l        r",
	"l $      r",
	"attttttttb",
	"wwwwwwwwww",
], {
	tileWidth: 16,
	tileHeight: 16,
	tiles: {
		"$": () => [
			sprite("chest"),
			area(),
			body({ isStatic: true }),
			tile({ isObstacle: true }),
			{ opened: false },
			"chest",
		],
		"a": () => [
			sprite("wall_botleft"),
			area({ shape: new Rect(vec2(0), 4, 16) }),
			body({ isStatic: true }),
			tile({ isObstacle: true }),
		],
		"b": () => [
			sprite("wall_botright"),
			area({ shape: new Rect(vec2(12, 0), 4, 16) }),
			body({ isStatic: true }),
			tile({ isObstacle: true }),
		],
		"c": () => [
			sprite("wall_topleft"),
			area(),
			body({ isStatic: true }),
			tile({ isObstacle: true }),
		],
		"d": () => [
			sprite("wall_topright"),
			area(),
			body({ isStatic: true }),
			tile({ isObstacle: true }),
		],
		"w": () => [
			sprite("wall"),
			area(),
			body({ isStatic: true }),
			tile({ isObstacle: true }),
		],
		"t": () => [
			sprite("wall_top"),
			area({ shape: new Rect(vec2(0, 12), 16, 4) }),
			body({ isStatic: true }),
			tile({ isObstacle: true }),
		],
		"l": () => [
			sprite("wall_left"),
			area({ shape: new Rect(vec2(0), 4, 16) }),
			body({ isStatic: true }),
			tile({ isObstacle: true }),
		],
		"r": () => [
			sprite("wall_right"),
			area({ shape: new Rect(vec2(12, 0), 4, 16) }),
			body({ isStatic: true }),
			tile({ isObstacle: true }),
		],
	},
})

// Player
const player = map.spawn([
	sprite("hero", { anim: "idle" }),
	area({ shape: new Rect(vec2(0, 6), 12, 12) }),
	body(),
	anchor("center"),
	tile(),
	health(3), // Player health
], 2, 2)

// Sword
const sword = player.add([
	pos(-4, 9),
	sprite("sword"),
	anchor("bot"),
	rotate(0),
	area({ scale: 0.8 }),
	"weapon",
])

// Enemy
function spawnEnemy(x, y) {
	const enemy = map.spawn([
		sprite("ogre", { anim: "idle" }),
		area({ scale: 0.8 }),
		body(),
		anchor("center"),
		health(2), // Enemy health
		"enemy",
		state("idle", ["idle", "chase", "attack"]),
	], x, y)

	// Enemy AI
	enemy.onStateEnter("idle", () => {
		enemy.play("idle")
	})

	enemy.onStateEnter("chase", () => {
		enemy.play("run")
	})

	enemy.onStateUpdate("chase", () => {
		const dir = player.pos.sub(enemy.pos).unit()
		enemy.move(dir.scale(50))
	})

	enemy.onStateEnter("attack", () => {
		enemy.play("idle")
		player.hurt(1) // Damage player
		wait(1, () => enemy.enterState("chase"))
	})

	enemy.onUpdate(() => {
		if (enemy.state !== "attack" && player.pos.dist(enemy.pos) < 64) {
			enemy.enterState("chase")
		}
		if (enemy.state === "chase" && player.pos.dist(enemy.pos) < 16) {
			enemy.enterState("attack")
		}
	})

	enemy.onCollide("weapon", () => {
		enemy.hurt(1) // Damage enemy
		if (enemy.hp() <= 0) {
			destroy(enemy)
		}
	})
}

// Spawn enemies
spawnEnemy(5, 4)
spawnEnemy(7, 6)

// Combat
onKeyPress("space", () => {
	sword.spin()
	for (const enemy of get("enemy")) {
		if (sword.isColliding(enemy)) {
			enemy.hurt(1) // Damage enemy
			if (enemy.hp() <= 0) {
				destroy(enemy)
			}
		}
	}
})

// Player movement
const SPEED = 120

onKeyDown("right", () => {
	player.flipX = false
	sword.flipX = false
	player.move(SPEED, 0)
	sword.pos = vec2(-4, 9)
})

onKeyDown("left", () => {
	player.flipX = true
	sword.flipX = true
	player.move(-SPEED, 0)
	sword.pos = vec2(4, 9)
})

onKeyDown("up", () => {
	player.move(0, -SPEED)
})

onKeyDown("down", () => {
	player.move(0, SPEED)
})

// Camera follows player
player.onUpdate(() => {
	camPos(player.pos)
})
````
This is the code as you can see where you have us and them and we are fighting them.
![](Screenshot_22-3-2025_192212_kaboomjs.com.jpeg)
As you can see the monster can attack us and we can attack them. This is something I learned and will be using in the future. This is my LL10 and what I did.

LL11
3/30/25

For this LL I made a kitchen for our project, so our project is like a cooking gam,e so I made the kitchen for it.
`````js
<!DOCTYPE html>
<html>
    <head>
        <meta charset="utf-8">
        <meta name="viewport" content="width=device-width, initial-scale=1">
        <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.2.1/dist/css/bootstrap.min.css" rel="stylesheet" />
        <title>Kitchen Chaos</title>
        <style>
            body {
                background-color: #333;
                overflow: hidden;
            }
        </style>
    </head>
    <body>
        <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.2.1/dist/js/bootstrap.bundle.min.js"></script>
        <script src="https://unpkg.com/kaboom@3000.0.1/dist/kaboom.js"></script>
        <script>
            kaboom({
                               background: [173, 216, 230], // Light blue kitchen walls
                width: 1000,  // Smaller canvas width
                height: 800  // Smaller canvas height
            });

            // Load kitchen-themed sprites
            loadSprite("chef", "sprites/../c.png");
            loadSprite("stove", "sprites/../sink.png");
            loadSprite("counter", "sprites/../counter.png");
            loadSprite("fridge", "sprites/../I.png");
            loadSprite("sink", "sprites/../s.png");

            // Define kitchen stations and staff
            const kitchenElements = {
                "s": { // Stove
                    sprite: "stove",
                    msg: "Cook here!",
                },
                "f": { // Fridge
                    sprite: "fridge",
                    msg: "Get ingredients!",
                },
                "k": { // Sink
                    sprite: "sink",
                    msg: "Wash dishes!",
                },
                "m": { // Manager
                    sprite: "stove",
                    msg: "Hurry up!",
                }
            };

            const levels = [
                // Smaller kitchen layout
                [
                    "------------",
                    "-          -",
                    "- s  f   k -",
                    "- C  C   C -",
                    "-          -",
                    "-     @    -",
                    "-          -",
                    "- C     m  -",
                    "-          -",
                    "------------",
                ]
            ];

            let score = 0;

            scene("main", (levelIdx) => {
                const SPEED = 240;

                const level = addLevel(levels[levelIdx], {
                    tileWidth: 64,
                    tileHeight: 64,
                    pos: vec2(64, 64),
                    tiles: {
                        "-": () => [
                            rect(64, 64),
                            color(105, 105, 105), // Steel counter floor
                            area(),
                            body({ isStatic: true }),
                        ],
                        "C": () => [
                            sprite("counter"),
                            area(),
                            body({ isStatic: true }),
                            "counter",
                            scale(0.7)
                        ],
                        "@": () => [
                            sprite("chef"),
                            area(),
                            body(),
                            "chef",
                            scale(0.5)
                        ]
                    },
                    wildcardTile(ch) {
                        const element = kitchenElements[ch];
                        if (element) {
                            return [
                                sprite(element.sprite),
                                area(),
                                body({ isStatic: true }),
                                "station",
                                {
                                    msg: element.msg
                                },
                            ];
                        }
                    },
                });

                const chef = level.get("chef")[0];

                function addDialog() {
                    const h = 100;  // Smaller dialog box
                    const pad = 12;
                    const bg = add([
                        pos(0, height() - h),
                        rect(width(), h),
                        color(0, 0, 0, 200),
                        z(100),
                    ]);
                    const txt = add([
                        text("", {
                            width: width() - pad * 2,
                            size: 16  // Smaller text
                        }),
                        pos(pad, height() - h + pad),
                        z(100),
                        color(255, 255, 255),
                    ]);
                    bg.hidden = true;
                    txt.hidden = true;
                    return {
                        say(t) {
                            txt.text = t;
                            bg.hidden = false;
                            txt.hidden = false;
                        },
                        dismiss() {
                            if (!this.active()) return;
                            txt.text = "";
                            bg.hidden = true;
                            txt.hidden = true;
                        },
                        active() {
                            return !bg.hidden;
                        },
                    };
                }

                const dialog = addDialog();

                const scoreDisplay = add([
                    text(`Orders: ${score}`, { size: 20 }),  // Smaller score display
                    pos(20, 20),
                    color(0, 0, 0),
                    z(50),
                    fixed()
                ]);

                chef.onCollide("station", (station) => {
                    dialog.say(station.msg);
                    // Simple scoring - press space to complete action
                    onKeyPress("space", () => {
                        score++;
                        scoreDisplay.text = `Orders: ${score}`;
                        dialog.dismiss();
                    });
                });

                const dirs = {
                    "left": LEFT,
                    "right": RIGHT,
                    "up": UP,
                    "down": DOWN,
                };
                for (const dir in dirs) {
                    onKeyPress(dir, () => dialog.dismiss());
                    onKeyDown(dir, () => chef.move(dirs[dir].scale(SPEED)));
                }

                add([
                    text("Kitchen", {  // Smaller title
                        size: 28,
                        width: width(),
                    }),
                    pos(width() / 2, 20),  // Moved up
                    anchor("center"),
                    color(70, 130, 180),
                    z(50),
                    fixed()
                ]);
            });

            go("main", 0);
        </script>
    </body>
</html>
`````
This is the code to the project. our project, as I said, needs a kitchen, so that is what I did this time.



![](k.png)


This is what I did for LL11, and I will be adding this to our work
<!-- 
* Links you used today (websites, videos, etc)
* Things you tried, progress you made, etc
* Challenges, a-ha moments, etc
* Questions you still have
* What you're going to try next
-->








