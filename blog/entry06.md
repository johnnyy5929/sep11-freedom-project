# Entry 6
##### 5/30/25

## Content 
This is my blog 6. Throughout this school year, we had a project called the Freedom Project. This is our year-long project, and we have reached the end. Where we had to pick a tool and learn how it use it. We are getting to our final parts of the project. We have coded an MVP up to this point, which is like a start to our project. So I finished my MVP during the break for this cooking game I was doing. I made some changes to the initial project. So the tool that I picked was Kaboom JS, and in some ways, I learned this was by using [kaboom website] (https://kaboomjs.com/). On this website, you are allowed to see the codes you can use, and you can go to the playground, which has games and codes for those games. Another thing I used was the [learning log](../tool/learning-log.md) where I put all the information I learned into. So wondering what I did for the freedom project. We had to make an elevator pitch and slides for our project. [Elevator pitch](https://docs.google.com/document/d/1-lgzP7K8CmKBgsjgY4cMFvLfvLTIZefJRRvoIbQveG4/edit?tab=t.0) and the [THE SLIDES](https://docs.google.com/presentation/d/1I7DhBuQJP0BuV2XR532SJXRRB0XofwneNnzXnazd_aU/edit?slide=id.p#slide=id.p). 


### My code
`````js
<!DOCTYPE html>
<html>
    <head>
        <meta charset="utf-8">
        <meta name="viewport" content="width=device-width, initial-scale=1">
        <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.2.1/dist/css/bootstrap.min.css" rel="stylesheet" />
        <title>Restaurant Adventure</title>
        <style>
            body {
                background-color: #333;
                overflow: hidden;
                margin: 0;
                padding: 0;
            }
            #menu-container {
                position: fixed;
                top: 0;
                left: 0;
                width: 100%;
                height: 100%;
                display: flex;
                flex-direction: column;
                justify-content: center;
                align-items: center;
                z-index: 1000;
                background-color: rgba(0, 0, 0, 0.7);
            }
            .menu {
                background-color: #f5e7d5;
                padding: 2rem;
                border-radius: 15px;
                text-align: center;
                box-shadow: 0 0 20px rgba(0, 0, 0, 0.5);
                max-width: 600px;
            }
            .game-title {
                font-size: 3.5rem;
                color: #8b4513;
                margin-bottom: 1.5rem;
                font-weight: bold;
                text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.3);
            }
            .role-selection {
                display: flex;
                justify-content: center;
                gap: 20px;
                margin-bottom: 1.5rem;
            }
            .btn-role {
                background-color: #8b4513;
                color: white;
                font-size: 1.2rem;
                padding: 0.8rem 1.5rem;
                border: none;
                border-radius: 10px;
                cursor: pointer;
                transition: all 0.3s;
                width: 180px;
            }
            .btn-role:hover {
                background-color: #a0522d;
                transform: scale(1.05);
            }
            .instructions {
                color: #333;
                font-size: 1.1rem;
                margin-top: 1rem;
                text-align: left;
            }
            .role-description {
                margin: 1rem 0;
                padding: 1rem;
                background-color: rgba(139, 69, 19, 0.1);
                border-radius: 8px;
            }
        </style>
    </head>
    <body>
        <!-- Main Menu -->
        <div id="menu-container">
            <div class="menu">
                <div class="game-title">Restaurant Adventure</div>
                <div class="role-selection">
                    <button id="chef-btn" class="btn-role">Be a Chef</button>
                    <button id="adventurer-btn" class="btn-role">Be an Adventurer</button>
                </div>
                <div id="chef-desc" class="role-description">
                    <h5>Chef Gameplay:</h5>
                    <ul>
                        <li>Manage the restaurant kitchen</li>
                        <li>Cook meals for customers</li>
                        <li>Keep customers happy to earn points</li>
                        <li>Upgrade your kitchen equipment</li>
                        <li>Press '1' to prepare a Burger</li>
                        <li>Press '2' to prepare a Pizza</li>
                        <li>Press '3' to prepare a Salad</li>
                        <li>Press 'S' to serve customers</li>
                        <li>Press 'E' to take customer orders</li>
                    </ul>
                </div>
                <div id="adventurer-desc" class="role-description" style="display:none;">
                    <h5>Adventurer Gameplay:</h5>
                    <ul>
                        <li>Explore a culinary fantasy world</li>
                        <li>Discover legendary recipes</li>
                        <li>Battle food monsters (Press 'F' to attack)</li>
                        <li>Complete epic cooking quests</li>
                        <li>Collect ingredients to upgrade your skills</li>
                    </ul>
                </div>
                <div class="instructions">
                    <h4>How to Play:</h4>
                    <ul>
                        <li>Use arrow keys to move your character</li>
                        <li>Press 'E' to interact with objects and people</li>
                        <li>Switch between areas using doors/portals</li>
                    </ul>
                </div>
            </div>
        </div>

        <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.2.1/dist/js/bootstrap.bundle.min.js"></script>
        <script src="https://unpkg.com/kaboom@3000.0.1/dist/kaboom.js"></script>
        <script>
            // Initialize Kaboom with larger canvas
            const k = kaboom({
                background: [245, 231, 213],
                width: 2500,
                height: 1000,
                global: false
            });

            // Make Kaboom functions available globally
            const {
                loadSprite,
                scene,
                addLevel,
                rect,
                color,
                area,
                body,
                sprite,
                scale,
                text,
                pos,
                vec2,
                z,
                fixed,
                anchor,
                LEFT,
                RIGHT,
                UP,
                DOWN,
                onKeyPress,
                onKeyDown,
                onKeyRelease,
                go,
                height,
                width,
                add,
                destroy,
                loop,
                get,
                onSceneLeave,
                wait,
                camPos,
                camShake,
                burp,
                play,
                loadSound,
                outline
            } = k;

            // Role selection
            document.getElementById("chef-btn").addEventListener("click", function() {
                document.getElementById("chef-desc").style.display = "block";
                document.getElementById("adventurer-desc").style.display = "none";
            });

            document.getElementById("adventurer-btn").addEventListener("click", function() {
                document.getElementById("adventurer-desc").style.display = "block";
                document.getElementById("chef-desc").style.display = "none";
            });

            // Start game with selected role
            document.getElementById("chef-btn").addEventListener("click", function() {
                setTimeout(() => {
                    const menuContainer = document.getElementById("menu-container");
                    menuContainer.parentNode.removeChild(menuContainer);
                    startGame("chef");
                }, 300);
            });

            document.getElementById("adventurer-btn").addEventListener("click", function() {
                setTimeout(() => {
                    const menuContainer = document.getElementById("menu-container");
                    menuContainer.parentNode.removeChild(menuContainer);
                    startGame("adventurer");
                }, 300);
            });

            function startGame(role) {
                // Load sprites
                loadSprite("chef", "sprites/../c.png");
                loadSprite("adventurer", "sprites/../c.png");
                loadSprite("customer1", "sprites/../c1.png");
                loadSprite("customer2", "sprites/../c3.png");
                loadSprite("table", "sprites/../table.png");
                loadSprite("door", "sprites/../door.png");
                loadSprite("stove", "sprites/../stove.png");
                loadSprite("counter", "sprites/../c4.png");
                loadSprite("fridge", "sprites/../fridge.png");
                loadSprite("plate", "sprites/../plate.png");
                loadSprite("food", "sprites/../food.png");
                loadSprite("burger", "sprites/../burger.png");
                loadSprite("pizza", "sprites/../pizza.png");
                loadSprite("salad", "sprites/../salad.png");

                // Adventurer-specific sprites
                loadSprite("quest-giver", "sprites/../c1.png");
                loadSprite("treasure", "sprites/../treasure.png");
                loadSprite("ingredient", "sprites/../ingredient.png");
                loadSprite("portal", "sprites/../door.png");
                loadSprite("monster", "sprites/../c3.png");
                loadSprite("forest-tree", "sprites/../tree.png");
                loadSprite("mountain", "sprites/../mountain.png");
                loadSprite("castle", "sprites/../castle.png");
                loadSprite("sword", "sprites/../sword.png");

                // Load sounds
                loadSound("sizzle", "sounds/sizzle.mp3");
                loadSound("coin", "sounds/coin.mp3");
                loadSound("attack", "sounds/attack.mp3");
                loadSound("hurt", "sounds/hurt.mp3");

                // Define characters and their dialog based on role
                const chefCharacters = {
                    "c": {
                        sprite: "customer1",
                        msg: "I'd like a burger, please!",
                        order: "burger",
                        patience: 100,
                        maxPatience: 100
                    },
                    "d": {
                        sprite: "customer2",
                        msg: "Can I get a pizza?",
                        order: "pizza",
                        patience: 100,
                        maxPatience: 100
                    },
                    "e": {
                        sprite: "customer1",
                        msg: "Just a salad for me, thanks!",
                        order: "salad",
                        patience: 100,
                        maxPatience: 100
                    }
                };

                const adventurerCharacters = {
                    "q": { sprite: "quest-giver", msg: "Find the 5 legendary ingredients!" },
                    "t": { sprite: "treasure", msg: "You found a treasure chest! +50 points" },
                    "i": { sprite: "ingredient", msg: "Rare ingredient found! +20 points" },
                    "m": {
                        sprite: "monster",
                        msg: "A wild Food Monster appears!",
                        health: 100,
                        maxHealth: 100,
                        damage: 15, // Increased damage
                        speed: 800, // Increased speed
                        attackCooldown: 1, // Reduced cooldown
                        chaseRange: 300 // How far they can detect player
                    }
                };

                // Define levels for each role
                const chefLevels = [
                    // Dining Area
                    [
                        "---------------------",
                        "-                   -",
                        "-  c      d       e -",
                        "-  T      T       T -",
                        "-                   -",
                        "-                   -",
                        "-         @         -",
                        "-                   -",
                        "-                   -",
                        "-  T     T        T -",
                        "-                   -",
                        "-                   -",
                        "---------------------",
                    ],
                    // Kitchen Area
                    [
                        "---------------------",
                        "-                   -",
                        "-  S   C   F        -",
                        "-                   -",
                        "-                   -",
                        "-                   -",
                        "-         @         -",
                        "-                   -",
                        "-                   -",
                        "-                   -",
                        "-                   -",
                        "-                   -",
                        "---------------------",
                    ]
                ];

                // Expanded Adventurer World with 4 unique areas
                const adventurerLevels = [
                    // 0 - Culinary Village (fewer monsters)
                    [
                        "-------------------------",
                        "-                       -",
                        "-  q     i     t       -",
                        "-  T     T     T       -",
                        "-                       -",
                        "-           P          -",
                        "-           @          -",
                        "-                       -",
                        "-  T     T     T       -",
                        "-  i     t     q       -",
                        "-                       -",
                        "-                       -",
                        "-------------------------",
                    ],
                    // 1 - Enchanted Forest (more monsters)
                    [
                        "-------------------------",
                        "-  ^^^^^^^^^^^^^^^^^^ ^ -",
                        "-  ^  i     t     m   ^ -",
                        "-  ^  m               ^ -",
                        "-  ^  ^  ^  ^     ^   ^ -",
                        "-  P        @         P -",
                        "-  ^                  ^ -",
                        "-  ^  m               ^ -",
                        "-  ^  q     i     m   ^ -",
                        "-  ^^^^^^^^^^^^^^^^^^^  -",
                        "-------------------------",
                    ],
                    // 2 - Spice Mountains (dangerous area)
                    [
                        "-------------------------",
                        "-  MMMMMMMMMMMMMMMMMMM -",
                        "-  M  t  M  i  M  m   M -",
                        "-  MM    m           M -",
                        "-  M        m        M -",
                        "-  P           @      P -",
                        "-  M              M   M -",
                        "-     m                -",
                        "-  M  m  M  i  M  m   M -",
                        "-  MMMMMMMMMMMMMMMMMM M -",
                        "-------------------------",
                    ],
                    // 3 - Royal Kitchen Castle (boss area)
                    [
                        "-------------------------",
                        "-  CCCCCCCCCCCCCCCCC    -",
                        "-  C  q  C  t  C  m  C  -",
                        "-     m                -",
                        "-           m           -",
                        "-  P  C  C  @  C  C   P -",
                        "-                       -",
                        "-     m         m       -",
                        "-  C  i  C  t  C  m  C  -",
                        "-  CCCCCCCCCCCCCCCCCCC  -",
                        "-------------------------",
                    ]
                ];

                // Game variables
                let score = 0;
                let currentLevel = 0;
                let playerRole = role;
                let ingredientsCollected = 0;
                const totalIngredientsNeeded = 5;

                // Chef-specific variables
                let preparedFood = null;
                let customerOrders = [];
                let kitchenUpgrades = {
                    stove: 1,
                    fridge: 1,
                    counter: 1
                };

                // Adventurer-specific variables
                let playerHealth = 100;
                let playerMaxHealth = 100;
                let playerDamage = 20;
                let playerAttackCooldown = 0;
                let monsters = [];
                let attackHitbox = null;

                // Main game scene
                scene("main", (levelIdx) => {
                    const SPEED = 240;
                    const levels = playerRole === "chef" ? chefLevels : adventurerLevels;
                    const characters = playerRole === "chef" ? chefCharacters : adventurerCharacters;

                    // Create the level
                    const level = addLevel(levels[levelIdx], {
                        tileWidth: 64,
                        tileHeight: 64,
                        pos: vec2(64, 64),
                        tiles: {
                            "-": () => [
                                rect(64, 64),
                                color(playerRole === "chef" ? [139, 69, 19] : [34, 139, 34]), // Different floor colors
                                area(),
                                body({ isStatic: true }),
                            ],
                            "T": () => [
                                sprite(playerRole === "chef" ? "table" : "forest-tree"),
                                area(),
                                body({ isStatic: true }),
                                "furniture",
                                scale(0.7)
                            ],
                            "@": () => [
                                sprite(playerRole === "chef" ? "chef" : "adventurer"),
                                area(),
                                body(),
                                "player",
                                scale(0.5),
                                {
                                    facing: "down",
                                    isAttacking: false,
                                    attackCooldown: 0
                                }
                            ],
                            // Chef-specific objects
                            "S": playerRole === "chef" ? () => [
                                sprite("stove"),
                                area(),
                                body({ isStatic: true }),
                                "kitchen-equipment",
                                scale(0.6),
                                "stove",
                                {
                                    upgradeLevel: kitchenUpgrades.stove
                                }
                            ] : undefined,
                            "C": playerRole === "chef" ? () => [
                                sprite("counter"),
                                area(),
                                body({ isStatic: true }),
                                "kitchen-equipment",
                                scale(0.6),
                                "counter",
                                {
                                    upgradeLevel: kitchenUpgrades.counter
                                }
                            ] : undefined,
                            "F": playerRole === "chef" ? () => [
                                sprite("fridge"),
                                area(),
                                body({ isStatic: true }),
                                "kitchen-equipment",
                                scale(0.6),
                                "fridge",
                                {
                                    upgradeLevel: kitchenUpgrades.fridge
                                }
                            ] : undefined,
                            // Adventurer-specific objects
                            "P": playerRole === "adventurer" ? () => [
                                sprite("portal"),
                                area(),
                                body({ isStatic: true }),
                                "portal",
                                scale(0.6),
                                {
                                    targetLevel: (levelIdx + 1) % adventurerLevels.length,
                                    isActive: true
                                }
                            ] : undefined,
                            "^": playerRole === "adventurer" ? () => [
                                sprite("forest-tree"),
                                area(),
                                body({ isStatic: true }),
                                "obstacle",
                                scale(0.8)
                            ] : undefined,
                            "M": playerRole === "adventurer" ? () => [
                                sprite("mountain"),
                                area(),
                                body({ isStatic: true }),
                                "obstacle",
                                scale(0.8)
                            ] : undefined,
                            "C": playerRole === "adventurer" ? () => [
                                sprite("castle"),
                                area(),
                                body({ isStatic: true }),
                                "obstacle",
                                scale(0.8)
                            ] : undefined
                        },
                        wildcardTile(ch) {
                            const char = characters[ch];
                            if (char) {
                                const components = [
                                    sprite(char.sprite),
                                    area(),
                                    body({ isStatic: true }),
                                    "character",
                                    {
                                        msg: char.msg,
                                        type: ch
                                    },
                                ];

                                // Add monster-specific components
                                if (char.health) {
                                    components.push({
                                        health: char.health,
                                        maxHealth: char.maxHealth,
                                        damage: char.damage,
                                        speed: char.speed,
                                        attackCooldown: char.attackCooldown,
                                        chaseRange: char.chaseRange,
                                        lastAttackTime: 0,
                                        isAggressive: true,
                                        isAlive: true
                                    });
                                }

                                // Add customer-specific components
                                if (char.patience) {
                                    components.push({
                                        order: char.order,
                                        patience: char.patience,
                                        maxPatience: char.maxPatience,
                                        isWaiting: false, // Changed to false initially
                                        isServed: false,
                                        hasOrder: false // New property to track if order was taken
                                    });
                                }

                                return components;
                            }
                        },
                    });

                    // Get the player object
                    const player = level.get("player")[0];

                    // Improved Dialog system with better visibility
                    function addDialog() {
                        const h = 150; // Taller dialog box
                        const pad = 30; // More padding
                        const bg = add([
                            pos(0, height() - h),
                            rect(width(), h),
                            color(0, 0, 0, 0.9), // More opaque background
                            z(100),
                            fixed()
                        ]);
                        const txt = add([
                            text("", {
                                width: width() - pad * 2,
                                size: 32, // Larger font size
                                font: "sans-serif",
                                align: "center", // Center aligned text
                            }),
                            pos(width()/2, height() - h + pad),
                            anchor("center"),
                            color(255, 255, 255), // White text
                            outline(4, color(0, 0, 0)), // Black outline for better contrast
                            z(100),
                            fixed()
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

                    // Score display
                    const scoreDisplay = add([
                        text(`${playerRole === "chef" ? "Restaurant" : "Adventure"} Score: ${score}`, { size: 24 }),
                        pos(20, 20),
                        color(0, 0, 0),
                        z(50),
                        fixed()
                    ]);

                    // Health display (for adventurer)
                    if (playerRole === "adventurer") {
                        const healthDisplay = add([
                            text(`Health: ${playerHealth}/${playerMaxHealth}`, { size: 24 }),
                            pos(20, 60),
                            color(0, 0, 0),
                            z(50),
                            fixed()
                        ]);
                    }

                    // Adventurer-specific displays
                    if (playerRole === "adventurer") {
                        const ingredientDisplay = add([
                            text(`Ingredients: ${ingredientsCollected}/${totalIngredientsNeeded}`, { size: 24 }),
                            pos(20, 100),
                            color(0, 0, 0),
                            z(50),
                            fixed()
                        ]);
                    }

                    // Chef-specific displays
                    if (playerRole === "chef") {
                        const ordersDisplay = add([
                            text(`Orders: ${customerOrders.length}`, { size: 24 }),
                            pos(20, 60),
                            color(0, 0, 0),
                            z(50),
                            fixed()
                        ]);

                        const upgradesDisplay = add([
                            text(`Stove: Lvl ${kitchenUpgrades.stove} | Fridge: Lvl ${kitchenUpgrades.fridge} | Counter: Lvl ${kitchenUpgrades.counter}`, { size: 20 }),
                            pos(20, 100),
                            color(0, 0, 0),
                            z(50),
                            fixed()
                        ]);
                    }

                    // Interact with characters and objects
                    player.onCollide("character", (character) => {
                        dialog.say(character.msg);

                        // Adventurer-specific interactions
                        if (playerRole === "adventurer") {
                            if (character.type === "t") { // Treasure
                                score += 50;
                                scoreDisplay.text = `Adventure Score: ${score}`;
                                play("coin");
                                destroy(character);
                            } else if (character.type === "i") { // Ingredient
                                score += 20;
                                ingredientsCollected++;
                                scoreDisplay.text = `Adventure Score: ${score}`;
                                play("coin");
                                destroy(character);

                                // Check if all ingredients collected
                                if (ingredientsCollected >= totalIngredientsNeeded) {
                                    dialog.say("Congratulations! You found all legendary ingredients!");
                                    playerMaxHealth += 50;
                                    playerDamage += 10;
                                }
                            } else if (character.type === "m") { // Monster
                                // Monster interaction handled in combat system
                            }
                        }
                    });

                    if (playerRole === "chef") {
                        player.onCollide("kitchen-equipment", (equipment) => {
                            if (equipment.sprite === "stove") {
                                dialog.say("Time to cook some food! Press '1' for Burger, '2' for Pizza, '3' for Salad");
                            } else if (equipment.sprite === "counter") {
                                dialog.say("Place prepared dishes here for serving");
                            } else if (equipment.sprite === "fridge") {
                                dialog.say("Get fresh ingredients from here. Press 'E' to upgrade (Cost: 200)");
                            }
                        });
                    }

                    // Portals for adventurer to switch between areas
                    if (playerRole === "adventurer") {
                        player.onCollide("portal", (portal) => {
                            if (portal.isActive) {
                                go("main", portal.targetLevel);
                            }
                        });
                    } else {
                        // Door for chef to switch between kitchen and dining
                        const door = add([
                            rect(64, 32),
                            pos(1000 - 100, height() / 2 + 325),
                            area(),
                            color(139, 69, 19),
                            "door",
                            {
                                targetLevel: levelIdx === 0 ? 1 : 0,
                                areaName: levelIdx === 0 ? "Kitchen" : "Dining Room"
                            }
                        ]);

                        // Door label
                        add([
                            text(levelIdx === 0 ? "Kitchen" : "Dining Room", { size: 16 }),
                            pos(1000 - 110, height() / 2 + 370),
                            color(0, 0, 0)
                        ]);

                        player.onCollide("door", (d) => {
                            go("main", d.targetLevel);
                        });
                    }

                    // Player movement
                    const dirs = {
                        "left": LEFT,
                        "right": RIGHT,
                        "up": UP,
                        "down": DOWN,
                    };

                    for (const dir in dirs) {
                        onKeyPress(dir, () => {
                            dialog.dismiss();
                            player.facing = dir;
                        });
                        onKeyDown(dir, () => player.move(dirs[dir].scale(SPEED)));
                    }

                    // Take customer orders with 'E' key (Chef only)
                    if (playerRole === "chef") {
                        onKeyPress("e", () => {
                            const customers = level.get("character").filter(c =>
                                c.type === "c" || c.type === "d" || c.type === "e"
                            );

                            // Find the nearest customer in range
                            let nearestCustomer = null;
                            let minDist = Infinity;

                            customers.forEach(customer => {
                                const dist = player.pos.dist(customer.pos);
                                if (dist < 100 && dist < minDist) {
                                    nearestCustomer = customer;
                                    minDist = dist;
                                }
                            });

                            if (nearestCustomer && !nearestCustomer.hasOrder && !nearestCustomer.isWaiting) {
                                // Take the order
                                nearestCustomer.isWaiting = true;
                                nearestCustomer.hasOrder = true;
                                customerOrders.push({
                                    type: nearestCustomer.order,
                                    customer: nearestCustomer
                                });
                                dialog.say(`Order taken: ${nearestCustomer.order}`);

                                // Start patience timer
                                loop(1, () => {
                                    if (nearestCustomer.isWaiting && !nearestCustomer.isServed) {
                                        nearestCustomer.patience -= 5;

                                        if (nearestCustomer.patience <= 0) {
                                            score -= 20;
                                            scoreDisplay.text = `Restaurant Score: ${score}`;
                                            dialog.say("Customer left unhappy! -20 points");
                                            destroy(nearestCustomer);
                                        }
                                    }
                                });
                            }
                        });

                        // Serve customers with 'S' key
                        onKeyPress("s", () => {
                            if (!preparedFood) {
                                dialog.say("You don't have any prepared food to serve!");
                                return;
                            }

                            const customers = level.get("character").filter(c =>
                                c.type === "c" || c.type === "d" || c.type === "e"
                            );

                            // Find the nearest waiting customer in range
                            let nearestCustomer = null;
                            let minDist = Infinity;

                            customers.forEach(customer => {
                                const dist = player.pos.dist(customer.pos);
                                if (customer.isWaiting && !customer.isServed && dist < 100 && dist < minDist) {
                                    nearestCustomer = customer;
                                    minDist = dist;
                                }
                            });

                            if (nearestCustomer && preparedFood.type === nearestCustomer.order) {
                                // Serve the customer
                                nearestCustomer.isServed = true;
                                nearestCustomer.isWaiting = false;
                                score += 50 * kitchenUpgrades.counter;
                                scoreDisplay.text = `Restaurant Score: ${score}`;
                                play("coin");
                                destroy(preparedFood);
                                preparedFood = null;
                                dialog.say(`Customer served! +${50 * kitchenUpgrades.counter} points`);

                                // Remove the order from the queue
                                customerOrders = customerOrders.filter(order =>
                                    order.customer !== nearestCustomer
                                );

                                // Customer leaves after being served
                                wait(2, () => {
                                    destroy(nearestCustomer);
                                });
                            } else if (nearestCustomer && preparedFood.type !== nearestCustomer.order) {
                                dialog.say(`Wrong order! This customer wants a ${nearestCustomer.order}`);
                            } else {
                                dialog.say("No waiting customers nearby to serve!");
                            }
                        });
                    }

                    // Combat system for adventurer
                    if (playerRole === "adventurer") {
                        // Attack with 'F' key
                        onKeyPress("f", () => {
                            if (player.isAttacking || player.attackCooldown > 0) return;

                            player.isAttacking = true;
                            play("attack");

                            // Create attack hitbox based on facing direction
                            const offset = {
                                left: vec2(-50, 0),
                                right: vec2(50, 0),
                                up: vec2(0, -50),
                                down: vec2(0, 50)
                            }[player.facing];

                            attackHitbox = add([
                                sprite("sword"),
                                pos(player.pos.add(offset)),
                                area(),
                                "attack",
                                {
                                    damage: playerDamage,
                                    lifespan: 0.2,
                                    timer: 0
                                },
                                scale(0.5),
                                z(10)
                            ]);

                            // Set cooldown
                            player.attackCooldown = 0.5;

                            // End attack after short time
                            wait(0.2, () => {
                                player.isAttacking = false;
                                if (attackHitbox) {
                                    destroy(attackHitbox);
                                    attackHitbox = null;
                                }
                            });
                        });

                        // Monster behavior
                        const monsters = level.get("character").filter(c => c.type === "m");
                        monsters.forEach(monster => {
                            // More aggressive monster movement towards player
                            loop(0.1, () => { // More frequent updates
                                if (!monster.isAlive) return;

                                // Only chase if player is within range
                                if (monster.pos.dist(player.pos) < monster.chaseRange) {
                                    const direction = player.pos.sub(monster.pos).unit();
                                    monster.move(direction.scale(monster.speed));
                                }
                            });

                            // Monster attacks more frequently
                            loop(0.1, () => {
                                if (!monster.isAlive || monster.attackCooldown > 0) return;

                                if (monster.pos.dist(player.pos) < 80) {
                                    playerHealth -= monster.damage;
                                    play("hurt");
                                    camShake(5);
                                    monster.attackCooldown = monster.attackCooldown;

                                    // Update health display
                                    get("health-display").forEach(h => {
                                        h.text = `Health: ${playerHealth}/${playerMaxHealth}`;
                                    });

                                    if (playerHealth <= 0) {
                                        dialog.say("Game Over! Refresh to try again.");
                                        // Disable player controls
                                        for (const dir in dirs) {
                                            onKeyRelease(dir, () => {});
                                            onKeyDown(dir, () => {});
                                        }
                                    }
                                }
                            });

                            // Monster takes damage
                            monster.onCollide("attack", () => {
                                if (!monster.isAlive) return;

                                monster.health -= playerDamage;
                                play("hurt");

                                if (monster.health <= 0) {
                                    monster.isAlive = false;
                                    score += 30;
                                    scoreDisplay.text = `Adventure Score: ${score}`;
                                    dialog.say("You defeated the Food Monster! +30 points");
                                    destroy(monster);
                                }
                            });
                        });
                    }

                    // Chef cooking system - Modified to use different keys for different recipes
                    if (playerRole === "chef") {
                        // Prepare food at stove with different keys for different recipes
                        onKeyPress("1", () => prepareFood("burger"));
                        onKeyPress("2", () => prepareFood("pizza"));
                        onKeyPress("3", () => prepareFood("salad"));

                        function prepareFood(foodType) {
                            const stove = level.get("stove")[0];
                            if (stove && player.pos.dist(stove.pos) < 100) {
                                if (preparedFood) {
                                    dialog.say("You already have prepared food!");
                                    return;
                                }

                                play("sizzle");
                                preparedFood = add([
                                    sprite(foodType),
                                    pos(player.pos.x, player.pos.y - 50),
                                    area(),
                                    "food",
                                    {
                                        type: foodType,
                                        isPrepared: true
                                    },
                                    scale(0.4)
                                ]);

                                dialog.say(`Prepared a ${foodType}! Take it to the counter`);
                            }
                        }

                        // Place food on counter
                        onKeyPress("s", () => {
                            const counter = level.get("counter")[0];
                            if (counter && preparedFood && player.pos.dist(counter.pos) < 100) {
                                preparedFood.pos = counter.pos.add(vec2(0, -30));
                                dialog.say(`Food placed on counter: ${preparedFood.type}`);
                            }
                        });

                        // Upgrade equipment
                        onKeyPress("e", () => {
                            const fridge = level.get("fridge")[0];
                            if (fridge && player.pos.dist(fridge.pos) < 100) {
                                if (score >= 200) {
                                    score -= 200;
                                    kitchenUpgrades.fridge++;
                                    scoreDisplay.text = `Restaurant Score: ${score}`;
                                    play("coin");
                                    dialog.say(`Fridge upgraded to level ${kitchenUpgrades.fridge}!`);

                                    // Update upgrades display
                                    get("upgrades-display").forEach(u => {
                                        u.text = `Stove: Lvl ${kitchenUpgrades.stove} | Fridge: Lvl ${kitchenUpgrades.fridge} | Counter: Lvl ${kitchenUpgrades.counter}`;
                                    });
                                } else {
                                    dialog.say("Not enough points to upgrade! (Need 200)");
                                }
                            }
                        });
                    }

                    // Cooldown system
                    loop(0.1, () => {
                        if (player.attackCooldown > 0) {
                            player.attackCooldown -= 0.1;
                        }

                        // Update attack hitbox position
                        if (attackHitbox) {
                            const offset = {
                                left: vec2(-50, 0),
                                right: vec2(50, 0),
                                up: vec2(0, -50),
                                down: vec2(0, 50)
                            }[player.facing];

                            attackHitbox.pos = player.pos.add(offset);
                            attackHitbox.timer += 0.1;

                            if (attackHitbox.timer >= attackHitbox.lifespan) {
                                destroy(attackHitbox);
                                attackHitbox = null;
                            }
                        }
                    });

                    // Display area name
                    const chefAreaNames = [" ", " "];
                    const adventurerAreaNames = [
                        " ",
                        " ",
                        " ",
                        " "
                    ];

                    add([
                        text(playerRole === "chef" ?
                            chefAreaNames[levelIdx] :
                            adventurerAreaNames[levelIdx], {
                            size: 32,
                            width: width(),
                        }),
                        pos(width() / 2, 30),
                        anchor("center"),
                        color(139, 69, 19),
                        z(50),
                        fixed()
                    ]);

                    // Camera follows player
                    camPos(player.pos);
                });

                // Start the game
                go("main", 0);
            }
        </script>
    </body>
</html>


`````


## Takeaways of the Expo elevator pitch

One takeaway is that I should make more eye contact. In my opinion, I feel like I didn't look around enough. I feel that when I was talking to the teachers, I was just looking at my computer, which isn't good because I don't know what people were thinking when I was presenting, and I wouldn't know if they could hear me. This is the first takeaway. 

The last takeaway was that you should be prepared before the pitch. If we weren't ready, we wouldn't know who is doing what and what part is whose. This is something I was making sure we do before we present. Which made it so that it went smoothly. These are the takeaways for the class pitch, and there were takeaways for the class presentation. We know who was doing which part of it, so when we were talking, it went well. 

## Takeaways of in-class presentation 
One takeaway from the class presentation  is that I should spend some time thinking of a hook. I lost points because my hook wasn't the best, so I should have spent more time on my hook and made it interesting. 

Another takeaway is that I should make more eye contact. In my opinion, I feel like I didn't look around enough. I feel that when I was talking, I was just looking at my computer, which isn't good because I don't know what people were thinking when I was presenting, and I wouldn't know if they could hear me.

The last takeaway was that you should be prepared before presenting in class. If we weren't ready, we wouldn't know who is doing what and what part is whose. This is something I was making sure we do before we present. Which made it so that it went smoothly. Therefore, we know what to do next time, and these are my takeaways. 


[Previous](entry05.md) | [Next](entry07.md)

[Home](../README.md)
