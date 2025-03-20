**The Point of Interest System** allows a designer to easily select a world entity and mark it as important and requiring action.

### Examples of POI

- **A plant is too dry and needs to be watered:** _red_
- **A rare item is to be looted:** _color corresponds to the rarity_
- **A chest is ready to be opened:** _color corresponds to the rarity_
- **A player needs health:** _blinking red_

### POI Display and Behavior

- There are different types of interests with various sizes.
- The size of a POI dictates if it is rendered on top or below other elements.
- If the POI goes off screen, a round UI popup appears near the edge.
- The popup may disappear if:
    - The player gets close enough.
    - The player interacts (e.g., shoots) with the POI.
    - The entity disappears.

---

## POI Details

### POI Information Table

|**Icon**|**Action**|**Color**|
|---|---|---|
|Text "HP"|Player needs health|Red|
|Water Droplet Icon|A plant needs to be watered|Red|
|Chest Icon|A chest needs to be opened|Rarity-based|
|Outline of the Item|A rare item can be looted|Rarity-based|

---

## Interest Type (ScriptableObject)

### Interest Type Table

|**Interest Type**|**Size (%)**|**Color**|**Icon**|
|---|---|---|---|
|Chest|50|Blue|POI_ChestIcon|
|EnemyBoss|80|Red|POI_Outline of Alien|
|RareItem|50|Gold|POI_Rare Loot Bag Icon|
|EpicItem|60|–|POI_Epic Loot Bag Icon|
|LegendaryItem|70|–|POI_Lengendary Loot Bag Icon|
|DivineItem|80|–|–|
|Enemy|50|Red|–|

---

## Additional Elements

- **POI_Frame:**  
    A sprite containing the frame of the notification (white by default so that its color can be changed).
    
- **Visual Aid:**  
    Please enjoy this 2-minute drawing (top-down view).
    

---

## Integration with the Stat Effect System

**Question:** How does the Stat Effect system tie in with the Point of Interest?

- **Example:**  
    A dry plant is a point of interest. In this case, "dry" is a stat effect.
    
- **Object Status Examples:**
    
    - **Dry Plant:**
        - _Status:_ Is a dry plant, **is** a POI.
    - **Damaged Player:**
        - _Status:_ Is a damaged player, **is not** a POI.