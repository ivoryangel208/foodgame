import random

class FishingGame:
    def __init__(self):  # Use double underscores for __init__
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

    def catch_fish(self):
        # Randomly select fish type and species
        fish_index = random.randint(0, len(self.fish_types) - 1)
        fish = self.fish_types[fish_index]
        species = self.species[fish_index]

        # Randomly generate weight, length, rarity, and price for the fish
        weight = random.randint(1, 100)  # in pounds
        length = random.randint(12, 72)  # in inches
        rarity = random.choice(["Common", "Uncommon", "Rare", "Legendary"])
        price = random.randint(10, 100)  # in coins

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
        # Show details of all catches
        return self.fish_log

    def view_aquarium(self):
        # Show all fish in aquarium
        return self.aquarium

    def purchase_item(self, item):
        # Check if the player has enough coins to purchase
        if item in self.store_items:
            if self.coins >= self.store_items[item]:
                self.coins -= self.store_items[item]
                return f"You have purchased {item}!"
            else:
                return "Not enough coins to make this purchase!"
        else:
            return f"{item} is not available in the store."

    def upgrade_fishing_rod(self):
        # Upgrade the fishing rod if coins are available
        if self.coins >= 20:
            self.coins -= 20
            self.fishing_level += 1
            return "Fishing rod upgraded!"
        else:
            return "Not enough coins for an upgrade!"

# Example usage:
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

    def catch_fish(self):
        # Randomly select fish type and species
        fish_index = random.randint(0, len(self.fish_types) - 1)
        fish = self.fish_types[fish_index]
        species = self.species[fish_index]

        # Randomly generate weight, length, rarity, and price for the fish
        weight = random.randint(1, 100)  # in pounds
        length = random.randint(12, 72)  # in inches
        rarity = random.choice(["Common", "Uncommon", "Rare", "Legendary"])
        price = random.randint(10, 100)  # in coins

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
        # Show details of all catches
        return self.fish_log

    def view_aquarium(self):
        # Show all fish in aquarium
        return self.aquarium

    def purchase_item(self, item):
        # Check if the player has enough coins to purchase
        if item in self.store_items:
            if self.coins >= self.store_items[item]:
                self.coins -= self.store_items[item]
                return f"You have purchased {item}!"
            else:
                return "Not enough coins to make this purchase!"
        else:
            return f"{item} is not available in the store."

    def upgrade_fishing_rod(self):
        # Upgrade the fishing rod if coins are available
        if self.coins >= 20:
            self.coins -= 20
            self.fishing_level += 1
            return "Fishing rod upgraded!"
        else:
            return "Not enough coins for an upgrade!"

# Example usage:
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
