imimport time

class FishingGame:
    def __init__(self):
        # Initialize basic attributes
        self.fish_count = 0
        self.coins = 0
        self.fishing_level = 1

        # Define available fish types and species
        self.fish_types = [
            '🐟', '🐠', '🐡', '🦈', '🐋', '🐠', '🐡', '🐟', '🐠', '🐟',
            '🐋', '🐡', '🐟', '🐠', '🐟', '🐠', '🐡', '🐠', '🐟', '🐋',
            '🐡', '🐠', '🐟', '🐟', '🐠', '🐋', '🐠', '🐟', '🐋', '🐠',
            '🐠', '🐡', '🐟', '🐋', '🐠', '🐠', '🐡', '🐟', '🐋', '🐟'
        ]

        self.species = [
            'Salmon', 'Trout', 'Bass', 'Pike', 'Shark', 'Whale', 'Cod',
            'Mackerel', 'Carp', 'Tuna', 'Swordfish', 'Anglerfish', 'Catfish',
            'Marlin', 'Barracuda', 'Swordfish', 'Bluegill', 'Snapper', 'Flounder',
            'Grouper', 'Largemouth Bass', 'Goldfish', 'Perch', 'Bream', 'Sturgeon',
            'Eel', 'Kingfish', 'Tilapia', 'Gudgeon', 'Lobster', 'Jellyfish',
            'Piranha', 'Lionfish', 'Tetra', 'Clownfish', 'Sardine', 'Piranha',
            'Angelfish'
        ]

        # Fish log to track catches
        self.fish_log = []

        # Aquarium to store fish
        self.aquarium = []

        # Store items for upgrading or purchasing
        self.store_items = {
            "Fishing Rod Upgrade": 20,
            "Bait": 10,
            "Boat Upgrade": 50
        }

    def custom_random(self, limit):
        """ Generate a pseudo-random number using current time for simplicity. """
        current_time = int(time.time() * 1000)  # Current time in milliseconds
        return current_time % limit

    def catch_fish(self):
        """ Catch a random fish and store the information. """
        fish_index = self.custom_random(len(self.fish_types))  # Random index for fish
        fish = self.fish_types[fish_index]
        species = self.species[fish_index]

        # Randomly generate weight, length, rarity, and price for the fish
        weight = self.custom_random(100) + 1  # Weight between 1-100 pounds
        length = self.custom_random(72) + 12  # Length between 12-72 inches
        rarity = ["Common", "Uncommon", "Rare", "Legendary"][self.custom_random(4)]  # Random rarity
        price = self.custom_random(100) + 10  # Price between 10-100 coins

        fish_info = {
            'Fish': fish,
            'Species': species,
            'Weight': weight,
            'Length': length,
            'Rarity': rarity,
            'Price': price
        }

        # Add fish to log and aquarium
        self.fish_log.append(fish_info)
        self.aquarium.append(fish_info)

        # Update fish count and coins
        self.fish_count += 1
        self.coins += price

        # Return the fish details
        return fish_info

    def view_fish_log(self):
        """ View all the catches made. """
        return self.fish_log

    def view_aquarium(self):
        """ View all fish currently in the aquarium. """
        return self.aquarium

    def purchase_item(self, item):
        """ Attempt to purchase an item from the store. """
        if item in self.store_items:
            if self.coins >= self.store_items[item]:
                self.coins -= self.store_items[item]
                return f"You have purchased {item}!"
            else:
                return "Not enough coins to make this purchase!"
        else:
            return f"{item} is not available in the store."

    def upgrade_fishing_rod(self):
        """ Upgrade the fishing rod if enough coins are available. """
        if self.coins >= 20:
            self.coins -= 20
            self.fishing_level += 1
            return "Fishing rod upgraded!"
        else:
            return "Not enough coins for an upgrade!"

# Example usage
if __name__ == "__main__":
    # Create an instance of the game
    game = FishingGame()

    # Catch some fish
    fish1 = game.catch_fish()
    fish2 = game.catch_fish()

    # View the log of catches
    print("Fish Log:")
    for entry in game.view_fish_log():
        print(entry)

    # View aquarium contents
    print("\nAquarium:")
    for fish in game.view_aquarium():
        print(fish)

    # Purchase an item from the store
    print(game.purchase_item("Fishing Rod Upgrade"))

    # Upgrade the fishing rod
    print(game.upgrade_fishing_rod())
