import pygame
import random
import time

# Initialize Pygame
pygame.init()

# Game Constants
SCREEN_WIDTH = 800
SCREEN_HEIGHT = 600
WHITE = (255, 255, 255)
GREEN = (0, 255, 0)
BROWN = (139, 69, 19)
RED = (255, 0, 0)
BLUE = (0, 0, 255)
YELLOW = (255, 255, 0)
LIGHT_GREEN = (144, 238, 144)
PURPLE = (128, 0, 128)

# Setup the display
screen = pygame.display.set_mode((SCREEN_WIDTH, SCREEN_HEIGHT))
pygame.display.set_caption("Ultimate Plant Grower 🌱")

# Fonts
font = pygame.font.Font(None, 36)
big_font = pygame.font.Font(None, 48)

# Plant Growth Stages
STAGES = ["🌱 Seed", "🌿 Sprout", "🌳 Vegetative", "🌸 Flowering", "🍇 Harvest"]

# Emojis for Plant Stats
HEALTH_EMOJI = {
    "good": "😄",
    "average": "😐",
    "poor": "😞"
}
WATER_EMOJI = {
    "high": "💧💧💧",
    "low": "💦",
    "empty": "🚫"
}

# Plant Class
class Plant:
    def __init__(self):
        self.stage = 0  # Start as "Seed"
        self.health = 100
        self.growth_time = 0
        self.water_level = 50  # Range 0-100
        self.pest_level = 0  # Range 0-100
        self.name = "My Plant"  # Default name
        self.color = GREEN  # Default plant color

    def grow(self):
        if self.stage < 4:
            self.growth_time += 1
            if self.growth_time >= 100:
                self.growth_time = 0
                self.stage += 1

    def water(self):
        if self.water_level < 100:
            self.water_level += 10
        self.health = min(self.health + 5, 100)

    def check_health(self):
        # Random event: pests
        if random.random() < 0.1:
            self.pest_level += 10
            self.health -= 5
        
        # Check for watering
        if self.water_level <= 20:
            self.health -= 2
        
        if self.health <= 0:
            self.stage = 0  # If the plant dies, it goes back to "Seed" stage
            self.health = 100  # Reset health

    def get_image(self):
        if self.stage == 0:
            return pygame.Surface((50, 50))
        elif self.stage == 1:
            return pygame.Surface((70, 70))
        elif self.stage == 2:
            return pygame.Surface((100, 100))
        elif self.stage == 3:
            return pygame.Surface((130, 130))
        elif self.stage == 4:
            return pygame.Surface((160, 160))

    def display_info(self):
        health_status = self.get_health_status()
        water_status = self.get_water_status()
        
        text = f"{self.name} | Stage: {STAGES[self.stage]} | {health_status} | {water_status}"
        return font.render(text, True, WHITE)

    def get_health_status(self):
        if self.health > 75:
            return HEALTH_EMOJI["good"]
        elif self.health > 40:
            return HEALTH_EMOJI["average"]
        else:
            return HEALTH_EMOJI["poor"]

    def get_water_status(self):
        if self.water_level > 75:
            return WATER_EMOJI["high"]
        elif self.water_level > 20:
            return WATER_EMOJI["low"]
        else:
            return WATER_EMOJI["empty"]

# Main Game Loop
def main():
    running = True
    clock = pygame.time.Clock()

    # Plant Initialization
    plant = Plant()
    plant_rect = pygame.Rect(300, 200, 50, 50)
    background_color = WHITE

    # Store System
    store_open = False
    store_items = ["Watering Can", "Fertilizer", "Pest Spray"]
    
    # Mini-Game System: Random Events
    mini_game_active = False
    random_events = ["Pest Attack", "Watering Boost", "Growth Burst"]

    # Main Game Loop
    while running:
        screen.fill(background_color)
        
        # Event Handling
        for event in pygame.event.get():
            if event.type == pygame.QUIT:
                running = False
            elif event.type == pygame.KEYDOWN:
                if event.key == pygame.K_SPACE:  # Water the plant with Space key
                    plant.water()
                elif event.key == pygame.K_g:  # Simulate plant growth on pressing 'G'
                    plant.grow()

        # Grow the plant over time
        plant.grow()
        plant.check_health()

        # Display the plant
        plant_surface = plant.get_image()
        screen.blit(plant_surface, plant_rect)

        # Display Plant Information
        info_text = plant.display_info()
        screen.blit(info_text, (10, 10))

        # Random Events: Check for water level, pests, etc.
        if plant.water_level <= 20:
            background_color = BLUE  # Simulate drought/low water
            mini_game_active = True  # Trigger random mini-game

        # Display Random Event Notification
        if mini_game_active:
            event_message = random.choice(random_events)
            event_text = big_font.render(f"Event: {event_message}", True, Y
