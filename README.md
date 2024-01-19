# The Anatomy of a Cutscene

# The Cutscene Node 
* Also known as CheckConditionAction, this node is used to establish what requirements are needed to allow the rest of its child nodes to execute. This means everything below a Cutscene node is what actions will be taken when the cutscene is triggered. They execute in order from top to bottom.

![image](https://github.com/ninaforce13/CustsceneGuide/assets/68625676/a8c8ed87-4757-4468-810a-7b1ba387e84b)
![image](https://github.com/ninaforce13/CustsceneGuide/assets/68625676/616e7ad0-d1b9-4c6d-a568-b6b27c7154db)

* Let's go over some of the more commonly used requirements, **Flags** and **Counters**. Flags will be saved to the player's save file and can be managed through the Cutscene/CheckConditionAction nodes (also through certain action nodes). You can name a flag whatever you like (just try to make it unique to your mod to avoid messing with an existing one).
* You can have the cutscene set a new flag by entering the flag's name in "Set Flag". If you would like to prevent this cutscene from occurring again after that, then use "One Time Flag". 
* Clear Flags will unset a previously set Flag.
* Require Flags will only allow this cutscene to play if a specific flag has been set prior to this cutscene.
* Deny Flags prevents the cutscene from playing if a specific flag has been set prior to this cutscene.
* Counters are similar to flags except the can increase in value as needed. You can use this to then allow or prevent specific cutscenes from playing after an action has been performed a specific number of times.

## Interaction Behavior
This is still just a cutscene node, however the name of this node is important if you want the NPC to be interactable with the player (e.g starting an interaction with a shopkeeper). It is still a completely normal cutscene node otherwise. 

# Action Nodes
* As the name suggests, these are individual actions taken during the cutscene. They can do just about anything you're willing to write code for, though there are a few premade ones you can take advantage of that will suit your needs most of the time so you don't need to make your own unless the action is very specific to your needs.
* Let's start with the most common action in the game, MessageDialogAction. This is how all the dialog in the game gets delivered, pretty simple right? Let's break it down by attributes:
## MessageDialogAction
* Portrait - This is the character image displayed when this message is delivered, it's not mandatory but for existing characters that have portraits you should try to use it anyway. 
* Portrait Position - As it sounds, you decide if the image is on the left side of the text box or the right side.
* Audio - The sound clip that plays with this message (usually a small phrase from that character's available audio tracks), also optional.
* Messages - The actual point of this action. Here you can add however many lines of dialog you like, just increase the size and add the dialog text to the empty box made available. The text can either be a Translation ID from your imported CSV file (we'll cover this later) or plain text. Using either option will have no impact on how your mod performs unless you're trying to make the text available in other languages, in which case you'll need to use Translations.
* Wait for Confirm - If selected, the message box will wait for player input before performing the next Action. This is useful if you're planning to present the player with Menu Options and want to keep this text on screen while they choose.
* Close After - Setting this will close the message box after it has finished delivering messages. Leave this checked off as well if you're presenting Menu Options after.
* Substitute Blackboard Values - This replaces the use of certain keys in your text with their respective blackboard values (we'll cover this further down)
* Use Pronouns - Replaces pronouns used with the specified target's pronoun options. 
* Style - Changes the appearance of the message, this is typically used for scenes related to Archangels. Normal works fine 9/10.
* Text Variant Seed - I haven't explored this yet.
	
## MenuDialogAction
* This action is how we present dialog options to the player. The size of Menu Options is how many options will display and the text IDs listed here work the same as with MessageDialogAction. If you add child nodes under the MenuDialogAction, they will be the action taken corresponding to the menu option in order from top to bottom (e.g. Option 1 triggers Child Action 1).
* Default Option is the  number of the option chosen whenever the player presses their respective Back button. A -1 value here means there is no default option and the player must deliberately choose an option. 

# Grouping Actions (Decorators)
* Sometimes you want multiple actions taken for a single menu option selected or branched behavior. In this case you can place a Decorator node and add all your actions as children for this node. The decorator node won't 


# Always Succeed
* This property comes up a lot in Cutscene related nodes. Action nodes inside a cutscene will always return a boolean value (True or False) to indicate they have completed successfully or not. The cutscene will play until it either runs out of nodes or something interrupts the scene with a False value. This is useful for interrupting dialog because the player has decided to cancel it or simply because you decided the rest of the nodes weren't necessary if an action before them fails. 
* What Always Succeed does is allow you to move forward with the rest of the actions even if something returned a False value. This might be useful for branching options or optional dialogue nodes that may not have triggered due to the player not setting off the right flag, but you don't want the entire cutscene to stop because of it. 

# Let's put it all together
For this example we will not use translation IDs for the text, to make it easier to follow which node was responsible for what dialog box.

