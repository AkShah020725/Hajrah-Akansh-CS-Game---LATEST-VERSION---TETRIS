***Tetris Game By Hajrah & Akansh***

**How to write our program?**
1. We will have to import the pygame module so the computer can run the game properly and it will function properly.
```
import pygame
import random
```
2. Now we will have to import the background sound that will play while the game is running so that it will have a good vibe.
```
pygame.init()
my_sound = pygame.mixer.Sound('/Users/akanshshah/Downloads/Akansh Iphone Pictures/Epic Mix_ Top 25 Songs No Vocals #1 ♫ Best Gaming Music 2024 Mix ♫ Best No Vocal, NCS, EDM, House.mp3')
my_sound.play()
```
3. Moving on, we will have to add the sizings for the game screen or the window so that it would display properly.
```
W = 9
H = 17
TILE = 45
DISPLAY_WIDTH = 200
game_width = W * TILE + DISPLAY_WIDTH
game_height = H * TILE
```
4. Now, we will start to define the shapes based on their numbers.
```
shapes = [
    [[13, 9, 5, 1], [7, 6, 5, 4]], 
    [[10, 6, 2, 1], [9, 5, 6, 7], [11, 10, 6, 2], [3, 5, 6, 7]], 
    [[6, 5, 4, 1], [9, 5, 1, 4], [9, 6, 5, 4], [9, 5, 1, 6]], 
    [[1, 2, 4, 5], [1, 5, 6, 10]], 
    [[0, 1, 5, 6], [1, 4, 5, 8]], 
    [[2, 6, 10, 11], [7, 9, 10, 11], [1, 2, 6, 10], [9, 10, 11, 13]], 
    [[0, 1, 2, 3], [0, 4, 8, 12], [12, 13, 14, 15], [3, 7, 11, 15]]
]
```
5. Moving on, we will be adding the shape colors so that it would be a better appealing display.
```
shape_colors = [
    (128, 0, 128), #Purple
    (255, 0, 255), #Bright pink
    (0, 0, 255), #Blue
    (0, 0, 128), #Navy
    (102, 0, 102), #Dark purple
    (51, 51, 153), #Dark blue
]
```
6. Now, we will define the block in the game and display the shapes on the grid.
```
class Tile:
```
7. We will now initialize a new tile with a specific x & y positon.
```
def __init__(self, x, y, tile_type):
```
8. We will now set the x & y coordinate of the tile on the grid.
```
self.x = x
self.y = y
```
9. We will now set the type of the tile, which will detect the shapes.
```
self.type = tile_type
```
10. We will now set the color of the tile, detecting the shapes.
```
self.color = tile_type
```
11. We will now initialize the rotation of the tile to zero.
```
self.rotation = 0
```
12. We will now return the recent shape based on its type.
```
def recent_shape(self):
```
13. We will now get the current shape based on its designs.
```
return shapes[self.type][self.rotation]
```
14. We will now rotate the current rotation to the next rotation state.
```
def shape_rotation(self):
```
15. We will now increment the rotation state within the shape design.
```
self.rotation = (self.rotation + 1) % len(shapes[self.type])
```
16. We will now represent the components of the tetris game.
```
class Game:
```
17. We will now initialize the game as it sets up the display and game field.
```
def __init__(self):
```
18. We will now initialize all of the imported pygame modules.
```
pygame.init()
```
19. We will now set the width of the game screen.
```
self.screen_width = game_width
```
20. We will now set the height of the game screen.
```
self.screen_height = game_height
```
21. We will now create a window with a seperate width and height.
```
self.screen = pygame.display.set_mode((self.screen_width, self.screen_height))
```
22. We will now create a 2D list representing the game field with their dimensions.
```
self.field = [[0 for y in range(W)] for x in range(H)]
```
23. We will now initalize a clock object to control the frame rate.
```
self.clock = pygame.time.Clock()
```
24. We will now initalize the score to zero at the start of the game.
```
self.score = 0
```
25. We will now indicate whether the game is over or not.
```
self.gameover = False
```
26. We will now create the current tile for the game.
```
self.current_tile = self.create_tile()
```
27. We will now create the next tile for the game.
```
self.next_tile = self.create_tile()
```
28. We will now set the font for the text in the game.
```
self.font = pygame.font.SysFont('Calibri', 35)
```
29. We will now initialize the fall time to zero.
```
self.fall_time = 0
```
30. We will now initialize the falling speed.
```
self.fall_speed = 100
```
31. We will now track whether the game has started or not.
```
self.start_game = False
```
32. We will now reset the game state to its initial state.
```
def reset_game(self):
```
33. We will now create a 2D list representing the game field with their dimensions.
```
self.field = [[0 for y in range(W)] for x in range(H)]
```
34. We will now initalize the score to zero at the start of the game.
```
self.score = 0
```
35. We will now indicate whether the game is over or not.
```
self.gameover = False
```
36. We will now create the current tile for the game.
```
self.current_tile = self.create_tile()
```
37. We will now create the next tile for the game.
```
self.next_tile = self.create_tile()
```
38. We will now initialize the fall time to zero.
```
self.fall_time = 0
```
39. We will now track whether the game has started or not.
```
self.start_game = False
```
40. We will now create and return a new tile at the top of the board.
```
def create_tile(self):
```
41. We will now return a new tile with a random shape or object.
```
return Tile(5, 0, random.randint(0, len(shapes) - 1) % len(shape_colors))
```
42. We will now draw the grid lines of the game.
```
def draw_grid(self):
```
43. We will now iterate over the width and height of the grid.
```
for x in range(W):
  for y in range(H):
```
44. We will now create a rectangle for each tile in the grid.
```
rect = pygame.Rect(x * TILE, y * TILE, TILE, TILE)
```
45. We will now draw a rectangle on the screen with a boarder color.
```
pygame.draw.rect(self.screen, (40, 40, 40), rect, 1)
```
46. We will now check whether the current tile intersects with the boundries of the game field.
```
def intersect(self):
```
47. We will now initialize the intersection as false.
```
intersection = False
```
48. We will now loop through the rows of the current tile.
```
for y in range(4):
```
49. We will now loop through the colomns of the current tile.
```
for x in range(4):
```
50. We will now check whether the current shape intersects with the field.
```
if y * 4 + x in self.current_tile.recent_shape():
```
51. We will now check whether the tile has reached the bottom of the grid.
```
if y + self.current_tile.y > H - 1:
  return True
```
52. We will now set a condition where the tile has to reach the right edge of the grid.
```
if x + self.current_tile.x > W - 1:
  return True
```
53. We will now set a condition where the tile has to reach the left edge of the grid.
```
if x + self.current_tile.x < 0:
  return True
```
54. We will now set a condition where the tile has to intersect with a non empty cell in the field.
```
if self.field[y + self.current_tile.y][x + self.current_tile.x] > 0:
  return True
return False
```
55. We will now 

