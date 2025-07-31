# snake_game
snake_game by using functions
import random
width=10
height=10

def print_board(snake, food):
    for y in range(height):
        for x in range(width):
            if[x, y] == food:
                print("F", end=" ")
            elif[x, y] in snake:
                print("S", end=" ")
            else:
                print(".", end=" ")
        print()
    print() 
def move_snake(snake,directions):
    head= snake [-1]
    if directions =='up':
        new_head=[head[0],head[1] - 1]
    elif directions =='down':
        new_head=[head[0],head[1] + 1]
    elif directions =='left':
        new_head=[head[0] - 1, head[1]]
    elif directions =='right':
        new_head=[head[0] + 1, head[1]]
    else:
        print("Invalid directions,use left/right/down/up..")
        return snake,False
    
#wall collide conditions
    if new_head[0] < 0 or new_head[0] >= width or new_head[1] < 0 or new_head[1] >= height:
        return snake,'wall'
#self collide conditions
    if new_head in snake:
        return snake,'self'
    
    snake.append(new_head)
    return snake,new_head
def place_food(snake):
    while True:
        x = random.randint(0, width - 1)
        y = random.randint(0, height - 1)
        if[x, y] not in snake:
            return[x, y]
        
def snake_game():
    snake=[[5, 5]]
    food=place_food(snake)
    score = 0
    while True:
        print_board(snake, food)
        print("score:", score)
        directions=input("enter directions(up/doen/right/left): ")

        snake,result=move_snake(snake,directions)

        if result=='wall':
            print("you hit the wall!! Game over!!")
            break
        elif result=='self':
            print("you hit yourself..... Game over!!!")
            break
        elif result == food:
            score += 1
            food=place_food(snake)
        else:
            snake.pop(0)
    print("Final score: " , score)

snake_game()        
