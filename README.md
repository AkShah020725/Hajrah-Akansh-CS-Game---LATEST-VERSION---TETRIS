***Tetris Game By Hajrah & Akansh***

***How to write our program?***

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
55. We will now check for complete lines and then remove them, increasing the score later.
```
def break_lines(self):
```
56. We will now initialize a variable to keep track of the number of lines that were removed.
```
lines = 0
```
57. We will now iterate over each row in the field.
```
for y in range(1, H):
```
58. We will now initialize a variable to count the empty cells in the row.
```
empty_cells = 0
```
59. We will now iterate through each column in the row.
```
for x in range(W):
```
60. We will now check if the cell in the current row is empty or not.
```
if self.field[y][x] == 0:
```
61. We will now increment the count of empty cells in the current row.
```
empty_cells += 1
```
62. We will now check if the current row has no empty cells.
```
if empty_cells == 0:
```
63. We will now increment the number of lines cleared.
```
lines += 1
```
64. We will now shift the lines above the cleared lines.
```
for y1 in range(y, 1, -1):
```
65. We will now continue to shift the lines.
```
for x in range(W):
```
66. We will now move the contents of the current row to the row above it.
```
self.field[y1][x] == self.field[y1 - 1][x]
```
67. We will now increase the score by the number of lines cleared by 100.
```
self.score += lines * 100
```
68. We will now draw the current falling tile on the screen.
```
def draw_tile(self, tile):
```
69. We will now iterate over the rows of the following tiles.
```
for y in range(4):
```
70. We will now iterate over the colomns of the following tiles.
```
for x in range(4):
```
71. We will now check if the x or y coordinate has a free tile or not.
```
if y * 4 + x in tile.recent_shape():
```
72. We will now calculate the current x coordinate on the grid.
```
current_x = tile.x + x
```
73. We will now calculate the current y coordinate on the grid.
```
current_y = tile.y + y
```
74. We will now check wheter the current y coordinate on the grid is visable on the grid.
```
if current_y >= 0:
```
75. We will now draw the tile on the screen if the y coordinate is visable on the screen.
```
pygame.draw.rect(self.screen, shape_colors[tile.color], (current_x * TILE, current_y * TILE, TILE, TILE))
```
76. We will now draw the preview of the "Next Shape" on the screen.
```
def draw_next_tile(self):
```
77. We will now render the label for the "Next Shape" preview.
```
label = self.font.render("Next Shape", True, (255, 255, 255))
```
78. We will now display the label for the "Next Shape" preview on the screen.
```
self.screen.blit(label, (game_width - DISPLAY_WIDTH + 20, 20))
```
79. We will now get the current shape format for the next tile.
```
format = self.next_tile.recent_shape()
```
80. We will now loop through each row.
```
for y in range(4):
```
81. We will now loop through each colomn.
```
for x in range(4):
```
82. We will now check if the current cell is part of the shape.
```
if y * 4 + x in format:
```
83. We will now calculate the x coordinate of the current cell in the "Next Shape".
```
current_x = W * TILE + 50 + x * TILE
```
84. We will now calculate the y coordinate of the current cell in the "Next Shape".
```
current_y = 80 + y * TILE
```
85. We will now draw a rectangle representing the "Next Shape".
```
pygame.draw.rect(self.screen, shape_colors[self.next_tile.color], (current_x, current_y, TILE, TILE))
```
86. We will now draw the tiles that already have been fallen.
```
def draw_field(self):
```
87. We will now iterate through each row in the field.
```
for y in range(H):
```
88. We will now iterate through each colomn in the field.
```
for x in range(W):
```
89. We will now if the cell is occupied or not.
```
if self.field[y][x]:
```
90. We will now draw the occupied with the shape color.
```
pygame.draw.rect(self.screen, shape_colors[self.field[y][x] - 1], (x * TILE, y * TILE, TILE, TILE))
```
91. We will now define the shapes that are going down.
```
def shape_going_down(self):
```
92. We will now move the current tile down by one.
```
self.current_tile.y += 1
```
93. We will now check if the current tile intersects with any other tile.
```
if self.intersect():
```
94. We will now move the current tile up by one.
```
self.current_tile.y -= 1
```
95. We will now lock the current tile in place.
```
self.freeze():
```
96. We will now define how the shapes get locked into their places on the gird.
```
def freeze(self):
```
97. We will now loop through each row and colomn.
```
for y in range(4):
    for x in range(4):
```
98. We will now check if the current position is part of the recent shape.
```
if y * 4 + x in self.current_tile.recent_shape():
```
99. We will now set the field's cell at the current tile's position.
```
self.field[y + self.current_tile.y][x + self.current_tile.x] = self.current_tile.color + 1
```
100. We will now call this method to check and break any completed lines in the grid.
```
self.break_lines()
```
101. We will now set the current tile to the next tile.
```
self.current_tile = self.next_tile
```
102. We will now generate a new tile to be used as the next tile in the game.
```
self.next_tile = self.create_tile()
```
103. We will now check if the current tile intersects with any other tile.
```
if self.intersect():
```
104. We will now set the gameover condition to true.
```
self.gameover = True
```
105. We will now define the method to move the current tile horizontally.
```
def go_horizontal(self, delta):
```
106. We will now store the current x coordinate of the current tile.
```
x = self.current_tile.x
```
107. We will now update the x coordinate of the current tile.
```
self.current_tile.x += delta
```
108. We will now check if the current tile intersects with any other tile.
```
if self.intersect():
```
109. We will now reset the x coordinate of the current tile to its previous value.
```
self.current_tile.x = x
```
110. We will now define the method to rotate the current tile.
```
def rotate(self):
```
111. We will now store the current rotation state of the current tile.
```
rotation = self.current_tile.rotation
```
112. We will now rotate the shape of the current tile.
```
self.current_tile.shape_rotation()
```
113. We will now check if the current tile intersects with any other tile.
```
if self.intersect():
```
114. We will now reset the rotation state of the current tile to its previous value.
```
self.current_tile.rotation = rotation
```
115. We will now define the possible events that a player could move or do.
```
def handle_events(self):
```
116. We will now iterate through all pygame events.
```
for event in pygame.event.get():
```
117. We will now check if the event type is a quit event.
```
if event.type == pygame.QUIT:
```
118. We will now quit the pygame module.
```
pygame.quit()
```
119. We will now exit the program.
```
quit()
```
120. We will now check if the event is a key press event.
```
if event.type == pygame.KEYDOWN:
```
121. We will now check if the event is a key press up arrow.
```
if event.key == pygame.K_UP:
```
122. We will now rotate the current tile clockwise.
```
self.rotate()
```
123. We will now check if the event is a key pressed down arrow.
```
if event.key == pygame.K_DOWN:
```
124. We will now make the current tile move downwards.
```
self.shape_going_down()
```
125. We will now check if the key pressed is a right arrow key.
```
if event.key == pygame.K_RIGHT:
```
126. We will now move the current tile one step to the right.
```
self.go_horizontal(1)
```
127. We will now check if the key pressed if the left arrow.
```
if event.key == pygame.K_LEFT:
```
128. We will now move the current tile one step to the left.
```
self.go_horizontal(-1)
```
129. We will now check if the key pressed is the space bar.
```
if event.key == pygame.K_SPACE:
```
130. We will now continue the looping until the current tile intersects with any other tile.
```
while not self.intersects():
```
131. We will now move the current tile one step downwards.
```
self.current_tile.y += 1
```
132. We will now move the current tile one step upwards.
```
self.current_tile.y -= 1
```
133. We will now lock the current tile in place.
```
self.freeze()
```
134. We will now define the display screen.
```
def display_screen(self):
```
135. We will now upload the background image.
```
background_image = pygame.image.load('/Users/akanshshah/Downloads/Random/PHOTO-2024-05-28-16-27-05 2.jpg').convert_alpha()
self.screen.blit(background_image, (0, 0))
```
136. We will now create a font object with Calibri.
```
font = pygame.font.SysFont('Calibri', 1)
```
137. We will now render the text using the font with white color.
```
title = font.render('Tetris Game!', True, (255, 255, 255))
```
138. We will now render the text using the font with white color.
```
start_button = font.render('Click to start!', True, (255, 255, 255))
```
139. We will now display the title text cenetered on the screen.
```
self.screen.blit(title, (self.screen.get_width() / 2 - title.get_width() / 2, self.screen.get_height() / 2 - title.get_height() / 2))
```
140. We will now display the start button text centered below the title.
```
self.screen.blit(start_button, (self.screen.get_width() / 2 - start_button.get_width() / 2, self.screen.get_height() / 2 + start_button.get_height() / 2))
```
141. We will now update the display to show any changes.
```
pygame.display.update()
```
142. We will now continue the loop until the game has started.
```
while not self.start_game:
```
143. We will now iterate through all pygame events.
```
for event in pygame.event.get():
```
144. We will now check if the event type is a quit event.
```
if event.type == pygame.QUIT:
```
145. We will now quit the pygame module.
```
pygame.quit()
```
146. We will now exit the program.
```
quit()
```
147. We will now check if the event is a mouse button down event.
```
elif event.type == pygame.MOUSEBUTTONDOWN:
```
148. We will now start the start_game function.
```
self.start_game = True
```
149. We will now define the score which will show on the screen or the display.
```
def show_score(self):
```
150. We will now render the text with the current score using the font with white color.
```
score_text = self.font.render('Score:' +str(self.score), True, (255, 255, 255))
```
151. We will now display the score text at a specific position on the screen.
```
self.screen.blit(score, (20, 10))
```
152. We will now define the game over screen.
```
def game_over_screen(self):
background_image = pygame.image.load('/Users/akanshshah/Downloads/Random/WhatsApp Image 2024-05-28 at 20.01.01.jpeg').convert_alpha()
self.screen.blit(background_image, (0, 0))
```
153. We will now create a font object with Calibri.
```
font = pygame.font.SysFont('Calibri', 1)
```
154. We will now render the text using the font with white color.
```
title = font.render('Game Over!', True, (255, 255, 255))
```
155. We will now render the text using the font with white color.
```
restart_button = font.render('R - Restart', True, (255, 255, 255))
```
156. We will now render the text using the font with white color.
```
quit_button = font.render('Q - Quit', True, (255, 255, 255))
```
157. We will now create a display of the title text which is centered above the middle screen.
```
self.screen.blit(title, (self.screen_width / 2 - title.get_width() / 2, self.screen_height / 2 - title.get_height() / 3))
```
158. We will now display the restart button which is centered below the game over message.
```
self.screen.blit(restart_button, (self.screen_width / 2 - restart_button.get_width() / 2, self.screen_height / 1.9 + restart_button.get_height()))
```
159. We will now display the quit button which is centered below the title text.
```
self.screen.blit(quit_button, (self.screen_width / 2 - quit_button.get_width() / 2, self.screen_height / 2 + quit_button.get_height() / 2))
```
160. We will now update the display to show any changes.
```
pygame.display.update()
```
161. We will now define the main loop of the game, we will continue the looping until the game is finished and we will call the method to display the game screen.
```
def main(self):
    while not self.start_game:
        self.display_screen()
```
162. We will now continue the loop until the game is over.
```
while not self.gameover:
```
163. We will now fill the screen with black color.
```
self.screen.fill((0, 0, 0))
```
164. We will now draw the grid on the screen.
```
self.draw_grid()
```
165. We will now draw the field on the screen.
```
self.draw.field()
```
166. We will now draw the current tile on the screen.
```
self.draw_tile(self.current_tile)
```
167. We will now draw the next tile on the screen.
```
self.draw.next.tile()
```
168. We will now draw the score on the screen.
```
self.show.score()
```
169. We will now update the entire display to show any changes.
```
pygame.display.flip()
```
170. We will now limit the frame rate to 60.
```
self.clock.tick(60)
```
171. We will now update the fall time by adding the passed time.
```
self.fall_time += self.clock.get_rawtime()
```
172. We will now tick the clock to control the frame rate.
```
self.clock.tick()
```
173. We will now check if the fall time has exceeded the fall speed.
```
if self.fall_time >= self.fall_speed:
```
174. We will now reset the fall time to zero.
```
self.fall_time = 0
```
175. We will now allow the method to move the current tile downwards.
```
self.shape_going_down()
```
176. We will now call the method to handle the events for the current objects.
```
self.handle_events()
```
177. We will now iterate through all events that pygame has detected.
```
for event in pygame.event.get():
```
178. We will now check if the event type is a quit.
```
if event.type == pygame.QUIT:
```
179. We will now quit the game window.
```
pygame.quit()
```
180. We will now exit the program.
```
quit()
```
181. We will now check if the event type is a key press event.
```
elif event.type == pygame.KEYDOWN:
```
182. We will now check if the pressed key is the r key.
```
if event.key == pygame.K_r:
```
183. We will now reset the game if the r is pressed by the player.
```
self.reset_game()
```
184. We will now end the main loop function and check if the pressed key is the q so that, the computer would know to quit the program.
```
self.main()
return
elif event.key == pygame.K_q:
    pygame.quit()
    quit()
```
185. We will now define the game state to its initial state.
```
def reset_game(self): #this resets the game state to its initial state
    self.field = [[0 for y in range(W)] for x in range(H)] #this creates a 2D list representing the game field with their dimensions
    self.score = 0 #this initalizes the score to zero at the start of the game
    self.gameover = False #this indicates whether the game is over or not
    self.current_tile = self.create_tile() #this creates the current tile for the game
    self.next_tile = self.create_tile() #this creates the next tile for the game
    self.fall_time = 0 #this initializes the fall time to zero
    self.start_game = False #this tracks whether the game has started or not
```
186. We will now define the create tile as it creates a new tile from the top of the board.
```
def create_tile(self): #this creates and returns a new tile at the top of the board
    return Tile(5, 0, random.randint(0, len(shapes) - 1) % len(shape_colors)) #this returns a new tile with a random shape or object
```
187. We will now define the draw grid as it will draw the grid.
```
def draw_grid(self): #this draws the grid lines of the game
    for x in range(W): #this iterates over the width of the grid
        for y in range(H): #this iterates over the height of the grid
            rect = pygame.Rect(x * TILE, y * TILE, TILE, TILE) #this creates a rectangle for each tile in the grid
            pygame.draw.rect(self.screen, (40, 40, 40), rect, 1) #this draws a rectangle on the screen with a boarder color
```
188. We will now define the intersection again.
```
def intersect(self): #this checks whether the current tile intersects with the boundries of the game field 
    intersection = False #this initializes the intersection as false 
        for y in range(4): #this loops through the rows of the current tile 
                for x in range(4): #this loops through the colomns of the current tile  
                    if y * 4 + x in self.current_tile.recent_shape(): #this checks whether the current shape intersects with the field 
                        if y + self.current_tile.y > H - 1: #this checks whether the tile has reached the bottom of the grid
                            return True 
                        if x + self.current_tile.x > W - 1: #this sets a condition where the tile has to reach the right edge of grid
                            return True
                        if x + self.current_tile.x < 0: #this sets a condition where the tile has to reach the left edge of the grid
                            return True
                        if self.field[y + self.current_tile.y][x + self.current_tile.x] > 0: #tile has to intersect with non empty cell
                            return True
        return False

```
189. We will now define the break lines again because this time we will be adding the speeds to the shapes going down faster.
```
def break_lines(self): #this checks for complete lines and then removes them, increasing the score later
    lines = 0 #this initializes a variable to keep track of the number of lines that were removed 
    for y in range(1, H): #this iterates over each row in the field 
        empty_cells = 0 #this initializes a variable to count the empty cells in the row 
        for x in range(W): #this iterates through each colomn in the row
            if self.field[y][x] == 0: #this checks if the cell in the current row is empty or not
                empty_cells += 1 #this increments the count of empty cells in the current row 
    if empty_cells == 0: #this checks if the current row has no empty cells
        lines += 1 #this increments the number of lines cleared 
        for y1 in range(y, 1, -1): #this shifts the lines above the cleared lines
            for x in range(W): #this continues to shift the lines 
                self.field[y1][x] = self.field[y1 - 1][x] #this moves the contents of the current row to the row above it 
    self.score += lines * 100 #this increases the score by the number of lines cleared by 100 
            
    if self.score >= 200 and self.fall_speed > 75: #this is increasing the falling speed if the score is greater then or equal to 200 
        self.fall_speed = 75 #Website from above - this is basically just setting the falling speed to 70 frames per seconds
    if self.score >= 400 and self.fall_speed > 50: #this is increasing the falling speed if the score is greater then or equal to 400 
        self.fall_speed = 50 #Website from above - this is setting the falling speed to 50 frames per seconds 
    if self.score >= 600 and self.fall_speed > 25: #this is increasing the falling speed if the score is greater than or equal to 600
        self.fall_speed = 25 #Website from above - this is setting the falling speed to 25 frames per seconds 
    if self.score >= 800 and self.fall_speed > 10: #this is increasing the falling speed if the score if greater than or equal to 800
        self.fall_speed = 10 #this is setting the falling speed to 10 frames per seconds
    if self.score >= 1000: #this is increasing the falling speed if the the score is greater then or equal to 1000 
        self.fall_speed = 1 #this is setting the falling speed to the lowest which is 1 frame per second

    self.next_tile = self.create_tile() #this generates a new tile object for the next tile
    if self.intersect(): #this checks if the current tile intersects with any other tile
        self.gameover = True #this sets the game condition to true, if it meets the condition
```
190. We will now add the updated code version of drawing the current tile.
```
def draw_tile(self, tile): #this draws the current falling tile on the screen 
    for y in range(4): #this iterates over the rows of the following tiles
        for x in range(4): #this iterates over the colomns of the following tiles 
            if y * 4 + x in tile.recent_shape(): #this checks if the x or y coordinate has a free tile or not
                current_x = tile.x + x #this calculates the current x coordinate on the grid
                current_y = tile.y + y #this calculates the current y coordinate on the grid 
                if current_y >= 0: #this checks whether the current y coordinate on the grid is visable in the grid
                    pygame.draw.rect(self.screen, shape_colors[tile.color], (current_x * TILE, current_y * TILE, TILE, TILE)) #this draws the tile on the screen if the y coordinate is visable in the grid
```
191. We will now add the updated code version of drawing the next tile.
```
def draw_next_tile(self): #this draws the preview of the next shape on the screen  
    label = self.font.render("Next Shape", True, (255, 255, 255)) #this renders the label for the next shape preview  
    self.screen.blit(label, (game_width - DISPLAY_WIDTH + 20, 20)) #this displays the label for the next shape preview on the screen
    format = self.next_tile.recent_shape() #Website from above - this gets the current shape format for the next tile
    for y in range(4): #this loops through each row 
        for x in range(4): #this loops through each coloumn 
            if y * 4 + x in format: #this checks if the current cell is part of the shape 
                current_x = W * TILE + 50 + x * TILE #this calculates the x coordinate of the current cell in the Next Shape 
                current_y = 80 + y * TILE #this calculates the y coordinate of the current cell in the Next Shape 
                pygame.draw.rect(self.screen, shape_colors[self.next_tile.color], (current_x, current_y, TILE, TILE)) #this draws a rectangle representing the Next Shape
```
192. We will now add the updated code version of drawing the field.
```
def draw_field(self): #this draws the tiles that have already been fallen 
    for y in range(H): #this iterates through each row in the field  
        for x in range(W): #this iterates through each column in the field  
            if self.field[y][x]: #this checks if the cell is occupied or not 
                pygame.draw.rect(self.screen, shape_colors[self.field[y][x] - 1], (x * TILE, y * TILE, TILE, TILE)) #this draws the occupied with the shape color
```
193. We will now add the updated code version of making the shapes go down.
```
def shape_going_down(self): #this defines the shapes that are going down
    self.current_tile.y += 5 #this moves the current tile down by one  
    if self.intersect(): #this checks if the current tile intersects with any other tile 
        self.current_tile.y -= 5 #this moves the current tile up by one  
        self.freeze() #this locks the current tile in place
```
194. We will now add the updated code version of defining the freeze function.
```
def freeze(self): #this defines how the shapes get locked into their places on their grid
    for y in range(4): #this loops through each row 
        for x in range(4): #this loops through each column 
            if y * 4 + x in self.current_tile.recent_shape(): #this checks if the current position is part of the recent shape 
                self.field[y + self.current_tile.y][x + self.current_tile.x] = self.current_tile.color + 1 #this sets the field's cell at the current tile's position
    self.break_lines() #this calls the method to check and break any completed lines in the grid
    self.current_tile = self.next_tile #this sets the current tile to the next tile  
    self.next_tile = self.create_tile() #this geneartes a new tile to be used as the next tile in the game 
    if self.intersect(): #this checks if the current tile intersects with any other tile  
        self.gameover = True #this sets the gameover to condition to true
```
195. We will now add the updated code version of making the shape go horizontally.
```
 def go_horizontal(self, delta): #this defines the method to move the current tile horizontally
    x = self.current_tile.x #this stores the current x coordinate of the current tile  
    self.current_tile.x += delta #this updates the x coordinate of the current tile  
    if self.intersect(): #this checks if the current tile intersects with any other tile
        self.current_tile.x = x #this resets the x coordinate of the current tile to its previous value
```
196. We will now add the updated code version of rotating the shapes.
```
def rotate(self): #this defines the method to rotate the current tile 
    rotation = self.current_tile.rotation #this stores the current rottion state of the current tile
    self.current_tile.shape_rotation() #this rotates the shape of the current tile 
    if self.intersect(): #this checks if the current tile intersects with any other tile 
        self.current_tile.rotation = rotation #this resets the rotation state of the current tile to its previous value 
```
197. We will now add the updated code version of handling the events.
```
def handle_events(self): #this defines the possible events that a player could move or do 
    for event in pygame.event.get(): #this itertes thorugh all pygame events  
        if event.type == pygame.QUIT: #this checks if the event type is a quit event 
            pygame.quit() #this quits the pygame module
            quit() #this exits the program 
        if event.type == pygame.KEYDOWN: #this checks if the event is a key press event  
            if event.key == pygame.K_UP: #this checks if the event is a key pressed up arrow
                self.rotate() #this rotates the current tile clockwise 
            if event.key == pygame.K_DOWN: #this checks if the event is a key pressed down arrow 
                self.shape_going_down() #this makes the current tile move downwards  
            if event.key == pygame.K_RIGHT: #this checks if the key pressed if the right arrow key  
                self.go_horizontal(1) #this moves the current tile on step to the right 
            if event.key == pygame.K_LEFT: #this checks if the key pressed is the left arrow key 
                self.go_horizontal(-1) #this moves the current tile one step to the left
            if event.key == pygame.K_SPACE: #this checks if the key pressed if the spacebar key 
                while not self.intersect(): #this continues the looping until the current tile intersects with any other tile 
                    self.current_tile.y += 1 #this moves the current tile one step downwards  
                self.current_tile.y -= 1 #this  moves the current tile one step upwards 
                self.freeze() #this locks the current tile in place
```
198. We will now add the updated code version displaying the screen.
```
def display_screen(self): #this defines the display screen 
            
    background_image = pygame.image.load('/Users/akanshshah/Downloads/Random/PHOTO-2024-05-28-16-27-05 2.jpg').convert_alpha()
    self.screen.blit(background_image, (0, 0)) 
            
    font = pygame.font.SysFont('Calibri', 1) #this creates a font object with Calibri 
    title = font.render('Tetris Game!', True, (255, 255, 255)) #this renders the text using the font with white color
    start_button = font.render('Click to start!', True, (255, 255, 255)) #this renders the text using the font with white color 
    self.screen.blit(title, (self.screen.get_width() / 2 - title.get_width() / 2, self.screen.get_height() / 2 - title.get_height() /  2)) #this displays the title text centered on the screen 
    self.screen.blit(start_button, (self.screen.get_width() / 2 - start_button.get_width() / 2, self.screen.get_height() / 2 + start_button.get_height() / 2)) #this displays the start button text cenetered below the title 
    pygame.display.update() #Website from above - this updates the display to show any changes 

    while not self.start_game: #this continues to loop until the game is started  
        for event in pygame.event.get(): #this iterates through all pygame events
            if event.type == pygame.QUIT: #this checks if the event type is a quit event  
                pygame.quit() #this quits the pygame module  
                quit() #this exits the program
            elif event.type == pygame.MOUSEBUTTONDOWN: #this checks if the event is a mouse button down event 
                self.start_game = True #this starts the start_game function
```
199. We will now add the updated code for showing the score on the screen.
```
def show_score(self): #this defines the score showing on the screen or display 
    score_text = self.font.render('Score: ' + str(self.score), True, (255, 255, 255)) #this renders the text with the current score
    self.screen.blit(score_text, (20, 10)) #this displays the score text at a specific postion on the screen
```
200. We will now add the updated code for the game over screen or the end screen.
```
def game_over_screen(self): #this defines the game over screen 
            
    background_image = pygame.image.load('/Users/akanshshah/Downloads/Random/WhatsApp Image 2024-05-28 at 20.01.01.jpeg').convert_alpha()
    self.screen.blit(background_image, (0, 0))
    font = pygame.font.SysFont('Calibri', 1) #this creates a font object with Calibri  
    title = font.render('Game Over!', True, (255, 255, 255)) #this renders the text using the font with white color 
    restart_button = font.render('R - Restart', True, (255, 255, 255)) #this renders the text using the font with white color 
    quit_button = font.render('Q - Quit', True, (255, 255, 255)) #this renders the text using the font with white color

    self.screen.blit(title, (self.screen_width / 2 - title.get_width() / 2, self.screen_height / 2 - title.get_height() / 3)) #this creates a display of the title text which is centered above the middle of the screen

    self.screen.blit(restart_button, (self.screen_width / 2 - restart_button.get_width() / 2, self.screen_height / 1.9 +               restart_button.get_height())) #this displays the restart button which is centered below the game over message
 
    self.screen.blit(quit_button, (self.screen_width / 2 - quit_button.get_width() / 2, self.screen_height / 2 +                    quit_button.get_height() / 2)) #this displays the quit button which is centered below the title text

    pygame.display.update() #this updates the display to show any changes
```
201. We will now add the updated code version for main loop of the game.
```
def main(self): #this is defining the main loop of the game  
    while not self.start_game: #this continues the looping until the game is started 
    self.display_screen() #this calls the method to display the game screen

    while not self.gameover: #this continues the looping until the game is over 
        self.screen.fill((0, 0, 0)) #this fills the screen with black color 
        self.draw_grid() #this draws the grid on the screen
        self.draw_field() #this draws the field on the screen
        self.draw_tile(self.current_tile) #this draws the current tile on the screen
        self.draw_next_tile() #this draws the next tile on the screen
        self.show_score() #this draws the score on the screen
        pygame.display.flip() #this updates the entire display to show any changes  
        self.clock.tick(60) #this limits the frame rate to 60  

        self.fall_time += self.clock.get_rawtime() #this updates the fall time by adding the passed time 
        self.clock.tick() #this ticks the clock to control the frame rate 
        if self.fall_time >= self.fall_speed: #this checks if the fall time has exceeded the fall speed 
            self.fall_time = 0 #this resets the fall time to zero
            self.shape_going_down() #this allows the method to moe the current tile downwards 

        self.handle_events() #this calls the method to handle the events for the current objects 

    self.game_over_screen() #this displays the game over screen 
    while True:
        for event in pygame.event.get(): #this iterates through all events that pygame has detected  
            if event.type == pygame.QUIT: #this checks if the event type is a quit event
                pygame.quit() #this quits the game window   
                quit() #this exits the program   
            elif event.type == pygame.KEYDOWN: #this checks if the event type is a key press event
                if event.key == pygame.K_r: #the checks if the pressed key is the r key 
                    self.reset_game() #this resets the game if the r is pressed by the player 
                    self.main() #this ends the main loop function    
                    return  
                elif event.key == pygame.K_q: #this checks if the pressed key is the q key 
                    pygame.quit() #this quits the game if the q is pressed by the player   
                    quit() #this exits the program
```
202. We will now end the loop of the whole game so that it will function or run properly.
```
if __name__ == "__main__": #this checks if the program is being ran by python 
    game = Game() #this creates an instance of the Game class to start the game  
    game.main() #this calls the main method of the game
```

***How can the user run this program effectively?***

1. Import all of the pygames needed to run this game.
2. Make a class called the "Class Game" where you could define all of the functions.
3. Call the "main" method of the game becuase this starts the loop of the game.
4. Then we will have to understand the handle events in this case they are the controls so that we know how to play the game properly and also enjoy it and have a good experince while playing it.
Up Arrow - Rotates Shapes
Down Arrow - Move Tiles Down Faster
Right Arrow - Moves Tile to Right Side
Left Arrow - Moves Tile to Left Side
SpaceBar - Drops Tile Instantly to the Ground
5. Then as the tile hits or crashes with the top of the grid or board, then the game shows the game over screen, where you have two options, one to quit the game pressing Q and the other option to restrart the game pressing R.

***References***

https://www.techwithtim.net/tutorials/game-development-with-python/tetris-pygame/tutorial-1
https://www.activestate.com/blog/how-to-use-pygame-for-game-development/
https://www.makeuseof.com/start-menu-and-game-over-screen-with-pygame/
https://stackoverflow.com/questions/23982907/how-to-center-text-in-pygame
https://www.geeksforgeeks.org/creating-start-menu-in-pygame/
https://www.youtube.com/watch?v=7kGNs5R-AM8
https://data-flair.training/blogs/python-tetris-game-pygame/
https://stackoverflow.com/questions/33963361/how-to-make-a-grid-in-pygame
https://www.mygreatlearning.com/blog/python-main/
https://www.geeksforgeeks.org/python-drawing-different-shapes-on-pygame-window/ 
https://data-flair.training/blogs/python-tetris-game-pygame/#google_vignette
https://stackoverflow.com/questions/32959705/player-does-not-move 
https://excelatfinance.com/xlf/xlf-colors-1.php
https://www.techwithtim.net/tutorials/game-development-with-python/tetris-pygame/tutorial-1 
https://stackoverflow.com/questions/32736498/initialize-class-attribute-with-a-method
https://stackoverflow.com/questions/52104513/python-pygame-class-init-question-not-drawing 
https://www.programiz.com/article/python-self-why
https://docs.python.org/3/tutorial/datastructures.html#list-comprehensions 
https://www.pygame.org/docs/
https://www.geeksforgeeks.org/pygame-drawing-objects-and-shapes/
https://stackoverflow.com/questions/66526297/python-how-to-type-anotate-a-method-that-returns-self
https://www.makeuseof.com/design-and-create-levels-in-pygame/
https://stackoverflow.com/questions/60468211/how-do-i-draw-text-onto-the-screen-in-pygame
https://stackoverflow.com/questions/33061063/how-to-make-another-level-in-python-platform-game 
https://gist.github.com/timurbakibayev/1f683d34487362b0f36280989c80960c
https://medium.com/wiki-flood/python-tetris-game-build-drop-repeat-ddaf0ed6804c 
https://stackoverflow.com/questions/19498987/how-to-make-a-sprites-speed-increase-after-a-certain-score-is-achieved-in-pygame
https://thecodingfun.com/2021/11/09/use-pygame-to-create-tetris-game-an-updated-version-part-2/ 

            


 






