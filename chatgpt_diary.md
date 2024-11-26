# ChatGPT Coding Diary

## Project Name: _Piano Player_
### Date: _11/18/24_

---

## 1. **I want to create a game where you can play the piano**
I want to create a game where music is played when the user uses the keys to play the piano.
## 2. **ChatGPT**
I went to ChatGPT for a base code to build off of. I was thinking of writing out the varibles for aspects of the code.
## 3. **Interaction with ChatGPT**
Questions asked to ChatGPT:
 - "How can I create a piano player game in pygame?"
 - "How can I make it so that certain keys play certain piano sounds?"
 - "How can I make the pian tile highlighted when pressed?"
## 4. **ChatGPT's Suggestions/Code Changes**
```python
import pygame
import os

# Initialize Pygame and the mixer
pygame.init()
pygame.mixer.init()

# Set up the screen
WIDTH, HEIGHT = 800, 400
screen = pygame.display.set_mode((WIDTH, HEIGHT))
pygame.display.set_caption("Piano Game")

# Define colors
WHITE = (255, 255, 255)
BLACK = (0, 0, 0)
GRAY = (200, 200, 200)

# Define piano keys
WHITE_KEYS = ['A', 'S', 'D', 'F', 'G', 'H', 'J', 'K', 'L']
BLACK_KEYS = ['W', 'E', 'T', 'Y', 'U', 'O', 'P']
NOTE_SOUNDS = {
    'A': 'sounds/note_C.wav', 'S': 'sounds/note_D.wav', 'D': 'sounds/note_E.wav',
    'F': 'sounds/note_F.wav', 'G': 'sounds/note_G.wav', 'H': 'sounds/note_A.wav',
    'J': 'sounds/note_B.wav', 'K': 'sounds/note_C_high.wav', 'L': 'sounds/note_D_high.wav',
    'W': 'sounds/note_C_sharp.wav', 'E': 'sounds/note_D_sharp.wav', 'T': 'sounds/note_F_sharp.wav',
    'Y': 'sounds/note_G_sharp.wav', 'U': 'sounds/note_A_sharp.wav', 'O': 'sounds/note_C_high_sharp.wav',
    'P': 'sounds/note_D_high_sharp.wav'
}

# Load sounds
for key, sound_file in NOTE_SOUNDS.items():
    if os.path.exists(sound_file):
        NOTE_SOUNDS[key] = pygame.mixer.Sound(sound_file)
    else:
        NOTE_SOUNDS[key] = None  # Placeholder for non-existent sound files

# Define key dimensions
WHITE_KEY_WIDTH = WIDTH // len(WHITE_KEYS)
BLACK_KEY_WIDTH = WHITE_KEY_WIDTH // 2
BLACK_KEY_HEIGHT = HEIGHT // 2

# Draw the piano keys
def draw_piano():
    # Draw white keys
    for i, key in enumerate(WHITE_KEYS):
        pygame.draw.rect(screen, WHITE, (i * WHITE_KEY_WIDTH, 0, WHITE_KEY_WIDTH, HEIGHT))
        pygame.draw.rect(screen, BLACK, (i * WHITE_KEY_WIDTH, 0, WHITE_KEY_WIDTH, HEIGHT), 2)  # Outline

    # Draw black keys
    for i, key in enumerate(BLACK_KEYS):
        black_key_x = (i + 1) * WHITE_KEY_WIDTH - BLACK_KEY_WIDTH // 2
        pygame.draw.rect(screen, BLACK, (black_key_x, 0, BLACK_KEY_WIDTH, BLACK_KEY_HEIGHT))
        pygame.draw.rect(screen, WHITE, (black_key_x, 0, BLACK_KEY_WIDTH, BLACK_KEY_HEIGHT), 2)  # Outline

# Play a sound when a key is pressed
def play_sound(key):
    if NOTE_SOUNDS.get(key):
        NOTE_SOUNDS[key].play()

# Main game loop
running = True
while running:
    screen.fill(GRAY)  # Set background color
    draw_piano()  # Draw the piano keys

    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            running = False

        # Check if a key is pressed
        if event.type == pygame.KEYDOWN:
            key = pygame.key.name(event.key).upper()
            if key in NOTE_SOUNDS:
                play_sound(key)

    pygame.display.flip()  # Update the screen

pygame.quit()
```
ChatGPT told me to have random keys assigned to the keyboard, which differed from my original approach of using an organized keybind system.
## 5. **Reflection on Changes**
ChatGPT's suggestions were helpful as it layed the base code for the game. Most of the code made sense, especially the note sound key binding part.
ChatGPT also recommended that I make the piano tiles turn gray when clicked idicating what key was being pressed, which I then implemented into the code. I also made audio files so that the keys actually can correspond to a sound.
## 6. **Testing and Results**
After finalizing the changes, my code was working smoothly besides the color changing keys. The results had the piano playing sounds when pressed but didn't have the keys turning gray for a moment when pressed. So I went to ChatGPT looking for new code that made that work. After fixing my code to ChatGPT's new suggestion, it worked out.
## 7. **What Did I Learn?**
Using ChatGPT for this project taught me how to make a user interface in pygame. I was able to create the piano keys with this new information. On the other hand, I learned to create audio files and use it to correspond to keys in the original code. I also was struggling with using a function I previously defined, but now I know how to use the functions in later parts of the code.
