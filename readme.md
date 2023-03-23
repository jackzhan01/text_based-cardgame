# Legends of the Three Kindoms 

## Team Members

Name: Liu Meitong

UID: 3035845887


Name: Zhan Wangjia

UID: 3035844560
<br/>

## Brief Introduction 

Legends of Three Kindoms is a popular multiplayer turn-based strategy card games combined with historical background of China's Three Kingdoms period. Players need to develop strategies and make actions with their cards in hand to beat all opponents and then achieve the final victory. Our game is a simplified version of it, with only two players being the human and the computer. 
<br/>

# Rules
## Items
1. Card piles: There are two piles of cards. One is the Drawing Pile, covered up for players to draw; the other is the Discarded Pile made of used cards. If the first pile runs out during the game, the second pile will be shuffled immediately and inserted into the first pile.
2. For each player:
	1) Hand Card: cards in hand. Players can play them anytime needed.
	2) Equipment Area: containing displayed Equipment Cards representing the player's equipments. Specifically in the text-based game, 0: Weapon; 1: Armor; 2: Attacking Mount; 3: Defending Mount. Only one piece of equipment of each type can be equipped simultaneously.
	3) Judgement Area: containing Scroll Cards (explained later) to be judged during the player's Judgement Phase.
	4) Distance: the distance between two players **in the player's view**. This means the Distance **in the opponent's view** may be different. The initial distance          is both 1 and can vary due to player's [Mounts] (explained later). Only when one's [Weapon] has a range equal to or greater than his/her Distance can he/she            seek to play a [Srike] on the opponent.
	5) HP: Each player has a initial and maximum HP of 5. Once one player's HP reduces to or below 0, the opponent wins the game.

## Game Flow

1.  At the beginning of the game, all game cards are shuffled and  each player can get 4 cards at random as their initial hand cards. 

2.	Then, players take turns to go through the following four phases:
    1)	Judgment Phase: performing judgments for the Scroll Cards in the player's Judgement Area.
    2)	Draw Phase: drawing 2 cards from the top of the pile.
    3)	Play Phase: playing cards. By deault, a player can only play [Strike] once per turn.
    4)	Fold Phase: discarding cards until the number of hand cards is equal to or less than the player's HP.

3.	Play until one player's HP reduces to or below 0, and then the opponent wins.

## Introdution of Cards

There are in total 156 cards (3 52-poker-cards) , each assigned with a function. They can be divided into three types: Basic Cards, Stroll Cards, and Equipment Cards. Among them, Equipment Cards can be further divided into Weapons, Armors, Attacking Mounts, and Defending Mounts.

### Basic Cards

**Strike:** Cause 1 damage to the target if he/she doesn’t respond with a Dodge. Only one Strike can be played per round. Only when one's [Weapon] has a range equal to or greater than his/her Distance can he/she seek to play a Srike on the opponent.

**Dodge:** Avoid the damage caused by Strike.

**Peach:** Recover 1 point of HP.

**Mead:** Play Mead before 1 Strike to cast a Mead-Strike and cause 1 extra damage. Or recover 1 point of HP under the near-death condition.

<br/>

### Scroll Cards

**Peach Garden:** All players recover 1 point of HP.

**Barbarian Invasion:** Cause 1 damage to the target if he/she doesn’t respond with a Strike.

**Ward:** Negate the effect of 1 Scroll Card. Can be further negated by another Ward.

**Snatch:** Take 1 card from the target either from his/her Hand Cards or Equipment Area.

**Duel:** Target player and the owner play 1 Strike in turn. Cause 1 damage to the one who cannot play Strike anymore.

**Iron Chain:** Play this card to discard another card and draw 1 new card.

**Fire Attack:** Target player shows 1 Hand Card. Cause 1 damage if the owner discard 1 hand card of the same suit, otherwise cause no damage and the target player can take back his/her card.

**Dismantle:** Discard 1 card from the target either from his/her Hand Cards or Equipment Area.

**Something from Nothing:** Draw 2 new cards.

**Bountiful Harvest:** Reveal the top 2 cards of the Drawing Pile. The owner first chooses a card, the other player takes the other one.

**Arrow Barrage:** Cause 1 damage to the target if he/she doesn’t respond with a Dodge.

**Lightning:** Judgement Card. Play this card to put it into **your** Judgement Area. During the current owner's Judgment Phase, reveal the top card of the Drawing Pile. If it’s between Spade 2 to 9, cause 3 points of damage to the current owner. If not, the card will be put to the other player’s Judgment Area.

**Starvation:** Judgement Card. Play this card to put it into the target's Judgement Area. During the target’s Judgment Phase, reveal the top card of the Drawing Pile. If it’s not Club, the target skips his/her Draw Phase. Discarded after the first judgement.

**Contentment:** Judgement Card. Play this card to put it into the target's Judgement Area. During the target’s Judgement Phase, reveal the top card of the Drawing Pile. If it’s not Heart, the target skips his/her Play Phase. Discarded after the first judgement.

<br/>


### Equipment Cards

**-Weapons-**

**Chu Ko Nu:** Range-1. The owner can play any number of Strike(s) during his/her Play Phase.

**Black Pommel:** Range-1. The owner’s Strike ignores the target’s Armors.

**Ancient Sword:** Range-2. The owner’s Strike causes two damages to the target if he/she doesn’t have any Hand Card.

**Green Dragon Crescent Blade:** Range-1. The owner can play another Strike if the first Strike is negated by the target’s Dodge.

**Eighteen-Span Viper Spear:** Range-2. The owner can use 2 hand cards as 1 Strike.

**Stone Piercing Axe:** Range-1. If the owner’s Strike is negated by the target’s Dodge, the owner can discard 2 hand cards to cause 1 damage to the target.

**Qilin Bow:** Range-2. Discard 1 equipped Mount card of the target if the owner causes damage to him/her with a Strike.


**-Armors-**

**Eight-Trigrams Formation:** Whenever the owner is attacked by a Strike, reveal the top card of the Drawing Pile. If it is Heart or Diamond, the Dodge is no longer needed.

**Silver Lion Helmet:** The owner can only take a maximum of 1 damage at one time. To be specific, the damages caused by Lightning and Mead-Strike will be reduced to 1.

**Rattan Armor:** Ignore damage from Barbarian Invasion and Arrow Barrage.


**-Mount-**

**Ferghana House, Violet Stallion, Red hare:** Attaking Mounts (-1 Mounts). Distance between two players in the owner’s view decreases 1 (so that the owner can attack more easily).

**Shadow Runner, Hex Mark, Yellow Flash, Crimson Steed:** Defending Mounts (+1 Mounts). Distance between two players in the opponent’s view increases 1 (so that it would be harder for the opponent to attack the owner).





## How did we implement the compulsory features? 

### Feature 1: Generation of random game sets or events

There are multiple occasions where new cards are needed. For expmple, each player's Draw Phase and the Judgements for Judgement Cards. They are all from the randomly shaffled Drawing Pile. Here is one example, more details available in shaffle.cpp:

```cpp
srand((unsigned)((time(NULL))+114514));
for(int i=0;i<=155;i++)
    while(true)
    {
        tmp=rand()%156;
        if(a[tmp]==-1)
        {
            a[tmp]=i;
            break;
        }
    }
// randomly shuffle the pile
```
### Feature 2: Data structures for storing game status

We designed two struct types "card" and "player" to store the corresponding information. More details available in structs.h.

```cpp
struct card
{
	int suit;
	int num;
	int type;
	int changdu;  //range
	void kanpai() {...}  //print out the card
};
struct player
{
	char name;
	int tili,tilishangxian; //hp and maximum hp
	int juese; //1 represents the player, 0 represents the computer
	vector <card> shoupai;  //hand cards
	card zhuangbei[4];  //equipments
	int zhuangbeishu;  //number of equipments
	vector <card> pandingpai;  //cards in the judging area
	int juli;  //the distance between two players in this player's view
	int mopai,chupai;  //0 represents the process can be done, 1 represents the precess is banned
	void initialize() {...}
	void Kanshoupai()  {...}  //print out the hand cards
	void Kanzhuangbei()  {...}  //print out the equipment cards
	void Kanpandingpai()  {...}  //print out the cards in the judging area
};
```

We also used a three-dimensional array to store the information of each card, with the first dimension being the number of complete-poker-cards (i.e. 2 represents this card is in the second 52-poker-card), the second dimension being the suit, the third dimension being the number, and type representing the function. More details available in main.cpp.

![image](https://user-images.githubusercontent.com/102410200/167257084-a0ed7a46-3915-40a3-b74a-c410dffa0897.png)

### Feature 3: Dynamic memory management

We used the STL container vector to store each player's Hand Cards, Judgement Area, the Drawing Pile, and the Discarded Pile. As player is able to add cards in the **Draw Phase** and pop cards in the **Play Phase** or **Fold Phase**,  dynamic memory management is the best way to store the information of hand cards. Below is a rough example:

```
struct player
{
    vector <card> handcards;
}
playerA.handcards.push_back(cardA); // add a handcard
playerA.handcards.erase(playerA.handcards.begin()+x);//pop no.x handcard 
```

### Feature 4: File input/output 

Although we believe the best choice is to play our game in person, we have prepared a partial input/output file for reference :)

### Feature 5: Program codes in multiple files

We divided our codes into the following parts according to their functionalityies. Dependencies between each file can be found in the Makefile.
structs.h: definition and declaration of struct type "card" and "player".
shuffle.cpp: shuffling the Drawing Pile at the beginning and during the game.
draw.cpp: draw 1 or 2 card(s) during the game.
judge.cpp: draw 1 card from the Drawing Pile for Judgement Cards.
weapons.cpp: functionalities of some weapons (not all) for the player's usage.
basic.cpp: functionalities of Basic Cards (Strike, Peach, Mead, Dotch included in Strike).
scroll.cpp: functionalities of Scroll Cards.
main.cpp: the frame of the whole game.

### Feature 6: Proper indentation and naming styles

Due to the so-long length of our game, we named some of the variables by Chinese pinin for better understanding during coding. Sorry for the inconvenience, and comments are added to explain their meanings.

### Feature 7: In-code documentation

Certain comments can be found to assist understanding. Moreover, the hint sentences as part of the program also serve to help reading.

## What unique features do we have?

### Recuision for implementation of certain cards
During a [Duel], the two players take turns to play [Strike] and damage will be caused to the one who cannot strike anymore. The Ward card also has a similar feature for its possibility to be negated by another Ward. These two cards requires the program to repeatedly asking alternative users for input until someone quits, which caters to the characteristic of a recursion. More details available in scroll.cpp. For example, for the Ward:

```cpp
bool Ward(card cur,player &A,player &B,vector<card> &used){  //ask A if he/she wants to play a ward on the card cur, return 1 for successfully negated
  if (A.juese){  //ask the player
     ...
     return (!Ward(used.back(),B,A,used));  //ask the opponent if he/she wants to play another ward
  }
  else{  //ask the computer
    ...
    return (!Ward(used.back(),B,A,used)); //ask the opponent if he/she wants to play another ward
  }
}
```

### Multiple types of cards and their counterbalancing functions
The game of Legends of Three Kindoms is famous for its diverse functionalities of cards, their counterbalancing functions, and the derived strategy. We also kept this important feature in our game. For example, if one wants to cause 1 damage to the opponent by Strike, he/she can first cast a Arrow Barrage, which must be responded with a Dodge in order to prevent attack, to  1 Dodge from the opponent so that he/she will have a smaller chance to defend from the next Strike, and vice versa. And if one plays a Snatch to grab the target's equipments which is Black Pommel and Eight-Trigrams Formation, he/she would want to choose the Black Pommel instead of Eight-Trigrams Formation, because the former has the power to neglect the latter. Such scenarios make the game greatly interesting to think about and play with.

### Automatically responsing computer
We have implemented a automatically responsing computer whose strategy is conbined with precedence choosing and random process. It has been set to a proper level for the player to enjoy winning and taste excitement at the same time.
