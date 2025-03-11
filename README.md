import random

class FishingGame:
    def __init__(self):
        self.fish_count = 0
        self.coins = 0
        self.fishing_level = 1
        self.fish_types = ['🐟', '🐠', '🐡', '🦈', '🐋', '🐠', '🐡', '🐟', '🐠', '🐟', '🐋', '🐡', '🐟', '🐠', '🐟', '🐠', '🐡', '🐠', '🐟', '🐋', 
                          '🐡', '🐠', '🐟', '🐟', '🐠', '🐋', '🐠', '🐟', '🐋', '🐠', '🐠', '🐡', '🐟', '🐋', '🐠', '🐠', '🐡', '🐟', '🐋', '🐟']
        self.species = ['Salmon', 'Trout', 'Bass', 'Pike', 'Shark', 'Whale', 'Cod', 'Mackerel', 'Carp', 'Tuna', 'Swordfish', 'Anglerfish', 'Catfish',
                        'Marlin', 'Barracuda', 'Swordfish', 'Bluegill', 'Snapper', 'Flounder', 'Grouper', 'Largemouth Bass', 'Goldfish', 'Perch', 'Bream', 
                        'Sturgeon', 'Eel', 'Kingfish', 'Tilapia', 'Gudgeon', 'Lobster', 'Jellyfish', 'Piranha', 'Lionfish', 'Tetra', 'Clownfish', 'Sardine',
                        'Piranha', 'Angelfish']
        self.fish_log = []
        self.aquarium = []
        self.store_items = {"Fishing Rod Upgrade": 20, "Bait": 10, "Boat Upgrade": 50}

    def display_inventory(self):
        print("\nInventory:")
        print(f"Fish caught: {self.fish_count}")
        print(f"Coins: {self.coins}")
        print(f"Fishing Level: {self.fishing_level}")
        print("-" * 30)

    def log_catch(self, fish, weight, length, rarity, price, description, nickname):
        self.fish_log.append({
            "Fish": fish,
            "Weight": weight,
            "Length": length,
            "Rarity": rarity,
            "Price": price,
            "Description": description,
            "Nickname": nickname
        })
        print(f"{fish} caught! Added to log.")

    def store(self):
        print("\nWelcome to the store!")
        print("Items available for purchase:")
        for item, price in self.store_items.items():
            print(f"{item}: {price} coins")
        item_choice = input("\nWhat would you like to buy? (Type the item name or 'exit' to leave): ").strip().lower()

        if item_choice == "exit":
            print("Exiting store...")
            return

        if item_choice in self.store_items:
            if self.coins >= self.store_items[item_choice]:
                self.coins -= self.store_items[item_choice]
                print(f"You bought {item_choice}!")
                if item_choice == "Fishing Rod Upgrade":
                    self.fishing_level += 1
                    print(f"Fishing level increased to {self.fishing_level}")
                elif item_choice == "Bait":
                    print("Bait purchased! You'll catch more fish!")
                elif item_choice == "Boat Upgrade":
                    print("Boat upgraded! You can travel to more fishing spots!")
            else:
                print("Not enough coins to buy this item.")
        else:
            print("Invalid item choice.")

    def aquarium_view(self):
        print("\n--- Aquarium ---")
        if not self.aquarium:
            print("Your aquarium is empty! Catch some fish to fill it.")
        else:
            for fish in self.aquarium:
                print(f"Nickname: {fish['Nickname']}, Species: {fish['Species']}, Weight: {fish['Weight']}kg, Length: {fish['Length']}cm, Rarity: {fish['Rarity']}")
        print("-" * 30)

    def catch_fish(self):
        fish = random.choice(self.fish_types)
        species = random.choice(self.species)
        weight = round(random.uniform(1, 50), 2)
        length = round(random.uniform(10, 200), 2)
        rarity = random.choice(['Common', 'Uncommon', 'Rare', 'Legendary'])
        price = round(random.uniform(10, 100), 2)
        description = f"A wild {species} fish."
        nickname = f"{fish}_{random.randint(1, 100)}"
        
        self.fish_count += 1
        self.coins += price
        self.log_catch(fish, weight, length, rarity, price, description, nickname)
        
        if rarity != 'Common':
            self.aquarium.append({"Nickname": nickname, "Species": species, "Weight": weight, "Length": length, "Rarity": rarity})
            print(f"Added {fish} to aquarium!")
        
    def sell_fish(self):
        if self.fish_count > 0:
            print(f"You sold your fish for {self.coins} coins!")
            self.fish_count = 0
        else:
            print("You don't have any fish to sell.")

    def buy_upgrade(self):
        if self.coins >= 20:
            self.coins -= 20
            self.fishing_level += 1
            print(f"Fishing level increased to {self.fishing_level}!")
        else:
            print("Not enough coins for an upgrade!")

    def display_game_log(self):
        print("\n--- Fishing Log ---")
        for log in self.fish_log:
            print(log)
        print("-" * 30)

    def start(self):
        while True:
            self.display_inventory()
            action = input("\nWhat would you like to do? (Fish, Sell, Buy Upgrade, Log, Store, Aquarium, Quit): ").strip().lower()

            if action == "fish":
                self.catch_fish()
            elif action == "sell":
                self.sell_fish()
            elif action == "buy upgrade":
                self.buy_upgrade()
            elif action == "log":
                self.display_game_log()
            elif action == "store":
                self.store()
            elif action == "aquarium":
                self.aquarium_view()
            elif action == "quit":
                print("Thanks for playing!")
                break
            else:
                print("Invalid action. Please try again.")

if __name__ == "__main__":
    game = FishingGame()
    game.start()
