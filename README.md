# SoloProject
# Code Geass: Console Battle

## How to play
1. Press the Play button in the Unity Editor to start the game.
2. Click inside the Game view window to ensure keypresses are focused.
3. Press number keys (1-4) to choose Lelouch's moves from the printed menu.
4. Read the battle log and health statuses printed in the Unity Console.
5. Defeat all rival beasts (C.C. and Suzaku) in order without letting Lelouch faint!

## My classes
- **Beast**: A plain C# class representing a creature with protected stats (HP, Attack, Defense), move storage, and data-clamping methods.
- **Move**: The parent base class containing the move's Name property and a virtual Apply method.
- **DamageMove**: A derived child class of Move that calculates and inflicts damage on a target beast.
- **HealMove**: A derived child class of Move that restores HP to the user up to its MaxHp limit.
- **DebuffMove**: A derived child class of Move (my custom move) that permanently lowers the target's Defense stat.
- **Battle**: A MonoBehaviour attached to the Game object that manages keyboard input, opponent queueing, and turn execution.

## Inheritance
The `Apply(Beast user, Beast target)` method is declared virtual in the base `Move` class and is overridden in `DamageMove`, `HealMove`, and `DebuffMove` using the override keyword. Inheritance is used because a DamageMove *is a* Move, a HealMove *is a* Move, and a DebuffMove *is a* Move. Storing all moves inside a `List<Move>` allows `Battle.cs` to trigger `Apply()` polymorphically without needing if/else checks for specific move types.

## My move
My custom move is `DebuffMove` ("GEASS COMMAND"). It lowers the target beast's Defense stat by a fixed amount (e.g., 3). This move adds strategy because reducing the opponent's defense makes all future physical attacks (DamageMove) hit significantly harder. To enforce proper encapsulation, a `LowerDefense(int amount)` method was added to `Beast.cs` as a door to modify the private set Defense property safely.

## AI help
I asked the AI to help me understand if 3 moves were enough for the player beast based on the assignment instructions. I also asked for help rebalancing the MaxHP and Attack stats of my beasts so that the heal move would be effective and there would be a fair chance to win or lose. Finally, I used the AI to help me find and fix a "divide by zero" bug in my `DebuffMove` by adding a clamp in `Beast.cs` to prevent the defense stat from dropping below 1.
