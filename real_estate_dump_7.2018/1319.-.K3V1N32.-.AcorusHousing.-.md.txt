AcorusHousing
=

Installation
-
Plugins you will need:

		* WorldGuard (link placeholder)
		* WorldEdit (link placeholder)
		* Permissions (link placeholder)
		* IConomy (link placeholder)

Just place the 'AcorusHousing.jar'  file in your 'plugins' folder along with the required plugins.

Download
-

http://dl.dropbox.com/u/22923847/BukkitPlugins/AcorusHousing/AcorusHousing.jar

Key
-

[] = options

<> = depends

() = required

Commands
-

		* /house [reg|buy|help|info|forsale|remove|update|givekey|takekey] <address|player|price>
		* /house reg (house address) _-=Registers a house with the address given=-_ //acorus.housing.admin
		* /house buy _-=Lets Users Buy a house=-_ //acorus.housing.buy
		* /hosue help _-=Shows a help page=-_ //anyone!
		* /house info (house address) _-=Shows the owners and price of a house=-_  //acorus.housing.info
		* /house forsale (house address) (price) _-=Sets the specified houses price=-_ //acorus.housing.admin
		* /house remove (house address) _-=Removes a house=-_ //acorus.housing.admin
		* /house update _-=Update a [forsale] sign=-_ //acorus.housing.admin
		* /house givekey (house address) (player) _-=Gives a key to the specified player for a house=-_ //owner or |acorus.housing.admin|
		* /house takekey (house address) (player) _-=Takes a key from specified player for a house=-_ //owner or |acorus.housing.admin|

About
-

Acorus Housing is a bukkit housing plugin that uses worldguard and permissions and iconomy to make it easier for players to buy apartments/houses and takes some stress of admins/staff for setting up houses for players

How to use
-

1. Server staff creates a(n) apartment/house and would like for players to be allowed to buy it, but does not want to have to be on at the same time as the player for the player to purchase the house.
* Server staff marks the 'editable' boundries of the house/apartment with worldedits wand (a wooden axe for acorus)
* Server staff types /region definr (house address)
* Server staff establishes an address for the house/apartment
* Server staff type: /house reg (house address)
* The default price is $1000 If the staff wishes the house to be a different price, type: /house forsale (address) (price)
* House (address) is registered and ready to be sold! all we need now is a way to sell it =)
* Server staff puts down a sign (most likely next to the apartment/house, or in a real estate office) and writes this on it:
	* Line 1:[houseinfo]
	* Line 2:(house address)
* Server staff presses done and then right clicks the sign to 'initialize it', the sign now reads:
	* Line 1:(house address)
	* Line 2:[forsale]
	* Line 3:(price)
	* Line 4:/house buy
* The house/apartment is now ready to be bought!
* Player finds a house that they want and found the sign that belongs to that house
* Player types: /house buy, and left clicks the sign, money is credited and the property is now owned by Player
* The sign should now read:
	* Line 1:(house address)
	* Line 2:Owner:
	* Line 3:(owner)
* Players friend comes onto server and wants to live in friends house with him(moocher!)
* Player types /house givekey (house address) (player name(moocher in this case))
* moocher can now edit blocks/open the door to Players house/apartment
* moocher breaks Players couch during a wild party while Player was away
* Player uses: /house takekey (house address) (player)
* moocher is kicked out!
* Player moves out
* Server staff use /house remove (address) and do steps 2 - 5 over again(sorry for now, the restore command will hopefully be implemented soon!)
* house/apartment is available again!
* ENJOY!!!!
