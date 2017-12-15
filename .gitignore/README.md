# triliza
import random

def print3x3 (board, trailing = True):
    print("",board[0],"|",board[1],"|",board[2])
    print("----------+----------+---------")
    print("",board[3],"|",board[4],"|",board[5])
    print("----------+----------+---------")
    print("",board[6],"|",board[7],"|",board[8])
    if trailing:
        print()

def ReadPosition(player, board):
    print3x3(board)
    print3x3(range(9))
    while True:
        print (player, "Choose square:",end="")
        position=int(input())
        if position < 0 or position > 8:
            print("Pick a value from 0 to 8")
        elif board[position] !="":
            print("The square is not empty")
        else:
            break
    return position

def play(player, position, board):
    print("The player", player, "plays in", position)
    board[position] = player

def check(player, board):
    if board[0]==board[1]==board[2]==player:
        return True
    elif board[3]==board[4]==board[5]==player:
        return True
    elif board[6]==board[7]==board[8]==player:
        return True
    elif board[0]==board[3]==board[6]==player:
        return True
    elif board[1]==board[4]==board[7]==player:
        return True
    elif board[2]==board[5]==board[8]==player:
        return True
    elif board[0]==board[4]==board[8]==player:
        return True
    elif board[2]==board[4]==board[6]==player:
        return True
    else:
        return False

def next(player):
    if player== "x":
      return "O"
    else:
      return "x"
    
def available(board):
    return [s for s in range(9) if board[s]== ""]

def randomPosition(board):
    nbMoves= board.count("x")
    if nbMoves >=2:
           position = checkPartial("x",board)
           if position is not None:
              return position
           position = checkPartial("O",board)
           if position is not None:
              return position
    else:
           return random.choice(available(board))

def checkPartial(board, player):
    if (board[0]==board[1]==player and board[2]==""):
        return board[2]
    elif (board[2]==board==[1]==player and board[0]==""):
        return board[0]
    elif (board[3]==board[4]==player and board[5]==""):
        return board[5]
    elif (board[5]==board[4]==player and board[3]==""):
        return board[3]
    elif (board[6]==board[7]==player and board[8]==""):
        return board[8]
    elif (board[8]==board[7]==player and board[6]==""):
        return board[6]
    elif (board[0]==board[4]==player and board[8]==""):
        return board[8]
    elif (board[8]==board[4]==player and board[0]==""):
        return board[0]
    elif (board[2]==board[4]==player and board[6]==""):
        return board[6]
    elif (board[6]==board[4]==player and board[2]==""):
        return board[2]
    elif (board[0]==board[3]==player and board[6]==""):
        return board[6]
    elif (board[6]==board[3]==player and board[0]==""):
        return board[0]
    elif (board[1]==board[4]==player and board[7]==""):
        return board[7]
    elif (board[7]==board[4]==player and board[1]==""):
        return board[1]
    elif (board[2]==board[5]==player and board[8]==""):
        return board[8]
    elif (board[8]==board[5]==player and board[2]==""):
        return board[2]
    elif (board[0]==board[2]==player and board[1]==""):
        return board[1]
    elif (board[3]==board[5]==player and board[4]==""):
        return board[4]
    elif (board[6]==board[8]==player and board[7]==""):
        return board[7]
    elif (board[0]==board[8]==player and board[4]==""):
        return board[4]
    elif (board[2]==board[6]==player and board[4]==""):
        return board[4]
    elif (board[0]==board[6]==player and board[3]==""):
        return board[3]
    elif (board[1]==board[7]==player and board[4]==""):
        return board[4]
    elif (board[2]==board[8]==player and board[5]==""):
        return board[5]
    else:
        return None

computer="x"
player= "x"
board= 9*[""]
blank= 9
inarow = False

while blank>0 and not inarow:
    if player == computer:
        position=randomPosition(board)
    else:
        position = ReadPosition(player,board)
    play(player,position,board)
    blank -=1
    inarow=check(player,board)
    player=next(player)
    
if inarow:
    print("Triliza!", next(player),"won")
else:
    print("Deuce")
