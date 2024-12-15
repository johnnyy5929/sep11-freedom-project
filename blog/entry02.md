# Entry 2
##### 12/15/24

## Content 
So we have a year-long project called the freedom project. In this project I have to choose a couple of tools. However I decided to go with kaboom. kaboom is a website where you can make games and learn about different codes for these games. Some of which I have been learning from LL's. Last time we only did LL1 and LL2. Now we did 3 more. The way I've been coding is using [kaboom website](https://kaboomjs.com/) in this website you are allowed to see the codes you can use and you can go to the playground which has games and codes for those games. Another thing I used was the [learning log](../tool/learning-log.md) Here you can see all the processes I have done. As some of the codes I learned are. 


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
The Engineering Design process is the part of the project you are on. So I am currently on the fourth Engineering Design process which is planning, I define the problem, research the problem and Brainstorm the problem. Now I need to find a way to make the product, so I am planning on making a game with Kaboom. I learned a lot from my learning log. I made a design of the game in my mind and an outline using kaboom. I know what codes I need to use and the next step is the prototype part. so this is the part of the Engineering Design part I am on.

## Skills 

### Researching
Researching is a really important skill that I learned when doing this blog and my LL. I need to research how to do some of these codes. How they work and how I can use them together. so learning how to research was a really important part that will help me later on in the year. Also when I am doing my work and I don't understand something, researching is helpful, in getting the right information. So researching is good and will help me later in the years.

### Communication 
This is one of the most important things ever. You always need good communication no matter what you are doing. Since I have a partner we need to talk and decide if we both are fine with doing what we want. Also communication is really helpful when you need help with something. For example, when I don't understand something you can ask people for help and they can help you. It is really an important skill that we should all use in our daily lives. this is a thing I will never forget how to do and will use it later on in the year for this freedom project this year. 


### Plans for the break
The plan for this break is to finish all my homework for sep and do all my LL. Afterwards, I will talk to my partner and work with them through the break. We will start coding the game. make levels and make sure everything works. We will learn about more codes and think of more ideas we want to add to the game. Also we will watch videos of people coding with Kaboom to get an idea of where we should start and how we should start. These are the plans for the break. We will finish some parts of the game and pray it works. 

[Previous](entry01.md) | [Next](entry03.md)

[Home](../README.md)



