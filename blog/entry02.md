# Entry 2
##### 12/15/24

## Content 
So we have a year long project called the freedom project. In this project I have to choose a couple of tools. However I decided to go with kaboom. kaboom is a website where you can make games and learn about different codes for these games. Some of which I been learning from LL's. Last time we only did LL1 and LL2. Now we did 3 more, the way I been coding is using [kaboom website](https://kaboomjs.com/) in this website you are allow to see the codes you can used and you can go to the playground which as games and codes for those games. Another thing I used was the [learning log](../tool/learning-log.md) In here you can see all the process I have done. As some of the codes I learned are. 


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
These are the two codes we can use allow you to hover over something. 
Other codes I have learned are
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
`````
These are most of the codes I have learned.

## Engineering Design Process
Engineering Design process is the part of the project you are on. So I am currently on the forth Engineering Design process which is planning, I define the problem, research the problem and Brainstorm the problem. Now I need to find a way to make the product, so I am planning on making a game with Kaboom. I learned a lot from my learning log. I made a design of the game in my mind and a outline using kaboom. I know what codes I need to use and the next step is the prototype part. so this is the part of the Engineering Design part I am on.

## Skills 

### Researching


### Communcation 


### Plans for the break


[Previous](entry01.md) | [Next](entry03.md)

[Home](../README.md)
