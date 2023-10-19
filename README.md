# Zerokwolf2.github.io
import pygame
import time

# Initialize Pygame
pygame.init()

# Set up window dimensions
screen_width = 800
screen_height = 600
screen = pygame.display.set_mode((screen_width, screen_height))
pygame.display.set_caption("Clicker Heroes Replica")

# Load images
hero_image = pygame.image.load("https://www.google.com/imgres?imgurl=https%3A%2F%2Fassets.stickpng.com%2Fimages%2F5b90edc3196573108b203a7d.png&tbnid=BNmsKhdKYsrccM&vet=10CBMQMyhxahcKEwi4o5j714KCAxUAAAAAHQAAAAAQAg..i&imgrefurl=https%3A%2F%2Fwww.stickpng.com%2Fimg%2Fgames%2Fclicker-heroes%2Fclicker-heroes-newbie&docid=dPKkPn5coJUPBM&w=1142&h=807&q=clicker%20heroes%20heroes%20images&safe=active&ved=0CBMQMyhxahcKEwi4o5j714KCAxUAAAAAHQAAAAAQAg")
enemy_image = pygame.image.load("https://www.google.com/imgres?imgurl=https%3A%2F%2Fstatic.wikia.nocookie.net%2Fclickerheroes%2Fimages%2Fe%2Fed%2FMushroom_Bloop.png%2Frevision%2Flatest%2Fscale-to-width-down%2F250%3Fcb%3D20150614034232&tbnid=k5vQhMix5c9vYM&vet=12ahUKEwiN9qHE14KCAxU0Lt4AHSvOC34QMygGegQIARBO..i&imgrefurl=https%3A%2F%2Fclickerheroes.fandom.com%2Fwiki%2FMonsters&docid=B9hwLMvn6ztWKM&w=250&h=346&q=clicker%20heroes%20monster%20images&safe=active&ved=2ahUKEwiN9qHE14KCAxU0Lt4AHSvOC34QMygGegQIARBO")

class Hero:
    def __init__(self, name, damage):
        self.name = name
        self.damage = damage
        self.level = 1
        self.prestige_level = 0

    def attack(self, enemy, clicker_damage):
        enemy.take_damage(self.damage + clicker_damage)

    def prestige(self):
        self.prestige_level += 1
        self.damage *= 2  # Increase damage after prestiging

class Enemy:
    def __init__(self, name, health):
        self.name = name
        self.health = health

    def take_damage(self, amount):
        self.health -= amount

def main():
    hero = Hero("Hero", 10)
    enemy = Enemy("Enemy", 100)
    clicker_damage = 1

    clock = pygame.time.Clock()

    while True:
        for event in pygame.event.get():
            if event.type == pygame.QUIT:
                pygame.quit()
                return

        hero.attack(enemy, clicker_damage)
        print(f"{hero.name} dealt {hero.damage + clicker_damage} damage to {enemy.name}")
        print(f"{enemy.name} has {enemy.health} health remaining")

        if enemy.health <= 0:
            print(f"{enemy.name} defeated!")

            if hero.level % 10 == 0:  # Every 10 levels, prestige
                hero.prestige()
                print(f"{hero.name} has prestiged to level {hero.prestige_level}")

            hero.level += 1
            enemy.health = 100  # Reset enemy health for the next level

        clicker_damage += 1  # Increase clicker damage over time

        # Draw the game objects
        screen.fill((0, 0, 0))  # Clear the screen
        screen.blit(hero_image, (100, 200))  # Draw hero image
        screen.blit(enemy_image, (500, 200))  # Draw enemy image
        pygame.display.flip()  # Update the display

        clock.tick(60)  # Limit the frame rate

if __name__ == "__main__":
    main()
