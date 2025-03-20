Players receive quests like "Enter the Galactic Grove dungeon". Upon completing the task, the player receives [[Experience Points (XP)]].

QuestSystem.GiveQuest.ToPlayer(player).UseItem(Items.GoldenBow).Once();

QuestSystem.GiveQuest(player, quest, results)

List of types of achievements

* Loot x numbers of items of type y

* Kill x enemies of type y

* Enter x number of times the dungeon y

* Plant x seeds of any type

* Use x number of times the item y

* Die once

* Complete dungeon x without getting hit once

* Open a chest with rarity x

· Quests, events, rewards - most importantly, the game has a variety of quests and events that reward the player with gems and in-game money, as well as equipment upgrades and various magical items.

Player can receive quests like "Destroy two scarecrow". They gain XP on completion.

Player receives quest "Obtain 1 Green Leaf" and completes it by collecting 1 green leaf.

Quest

➝ UseItem

➝ Kill enemy

QuestResult

➝ ReceiveNewQuest

➝ ReceiveGold

➝ ReceiveItem

The player can see his completed quests by sorting by "Completed" in the "Quests" menu.