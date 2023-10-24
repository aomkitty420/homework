# homework 
#api
import requests

url = "https://rickandmortyapi.com/api/character/1"
rick_and_morty = requests.get(url)

rick_and_morty.json()

character = []
for x in range(50):
  url = f"https://rickandmortyapi.com/api/character/1{x+1}"
  response = requests.get(url)
  if response.status_code == 200:
    json_ram =response.json()
    character.append(
        (json_ram["name"],
        json_ram["species"],
        json_ram["origin"])
    )

    import pandas as pd
df = pd.DataFrame(character)

df.columns = ["name","species","origin"]
df.reset_index()

df.to_csv("rick_and_morty")

#ATM
class Customer:
    def __init__(self, name, pin, balance):
        self.name = name
        self.pin = pin
        self.balance = balance

customer_1 = Customer("Mr.A", "1234", 50000)

def atm():
    print("Please type your PIN:")
    while True:
        pin_input = input()
        if pin_input == customer_1.pin:
            print("Correct")
            break
        else:
            print("Incorrect PIN. Please try again.")

    print("Welcome to our ATM. We are a financial institute, not a Korean band.")
    print(f"Nice to see you, {customer_1.name}.")
    
    print("Please select the option you want to perform today:")
    print("1. Withdraw - press 1")
    print("2. Deposit - press 2")
    print("3. Check money in account - press 3")
    print("4. Cancel - press 4")
    print("5. Donate for our bank - press 5")

    while True:
        option = input("Enter your choice: ")

        if option == '1':
            print("Type the amount of money you want to withdraw, but don't empty your account; we don't want a bank run.")
            amount = int(input())
            if amount <= customer_1.balance:
                print("Have a nice day!")
                break
            else:
                print("You don't have enough balance.")
        elif option == '2':
            print("Thank you for trusting us to take care of your money.")
            print("Even if we will use your money for someone else to loan and mock up the number for your account.")
            num_deposit = float(input("Enter the amount you want to deposit: "))
            customer_1.balance += num_deposit
            print(f"Thank you! (devil smile) your current balance {customer_1.balance}")
            break
        elif option == '3':
            print(f"Your current balance is: ${customer_1.balance}\nnow let choose your option or if you want to quit press 4")
        elif option == '4':
            print("Goodbye!")
            break
        elif option == '5':
            print("Thank you for your kindness. How much would you like to donate?")
            donate = float(input())
            if donate <= 900:
                print("Thank you, Mr. Stingy!")
                break
            else:
                print("What a generous person! We appreciate your kindness, and we will treat you like the king of this land.")
                break
        else:
            print("Invalid choice. Please select a valid option.")

atm()

#Rock paper scissor
import random as rd

com_option = ["rock", "paper", "scissor"]
result = {"win": 0, "tie": 0, "lose": 0}

def game_rps():
    print("Welcome to Rock-Paper-Scissors game.")
    print("Let's choose your option: 'rock', 'paper', 'scissor'.")
    print("If you want to quit, type 'quit': ")
    
    while True:
        com = rd.choice(com_option)
        greeting = input()
        
        if greeting == com:
            print("It's a tie!,\nif you want to continue playing let' fill your option: ")
            print("...............................")
            result["tie"] += 1
        elif (greeting == "rock" and com == "scissor") or (greeting == "paper" and com == "rock") or (greeting == "scissor" and com == "paper"):
            print("You win!\nPlay again or type 'quit' to exit.")
            print("...............................")
            result["win"] += 1
        elif greeting == "quit":
            print("Goodbye!")
            break
        elif greeting not in ['rock', 'paper', 'scissor']:
            print("Wrong answer!\nPlease type only 'rock', 'paper', 'scissor', or 'quit'.")
            print("...............................")
        else:
            print("You lose!")
            print("...............................")
            result["lose"] += 1

    print(f"Game Summary:\n Wins > {result['win']},\n Ties > {result['tie']},\n Losses > {result['lose']}")

game_rps()

#scraping
!pip list
!pip install gazpacho
from gazpacho import Soup
import requests

url = "https://www.imdb.com/search/title/?groups=top_100"
headers = {"Accept-Language": "en-US,en;q=0.5"}
html = requests.get(url,headers = headers)

imdb = Soup(html.text)
titles = imdb.find("h3",{"class":"lister-item-header"})
cleansing_titles=[]
for i in titles:
  cleansing_titles.append(i.strip())
print(cleansing_titles)
from gazpacho import Soup
import requests

url_2 = "https://www.imdb.com/search/title/?groups=top_100"
html_2 = requests.get(url_2)

imdb_rating = Soup(html_2.text)
ratings = imdb_rating.find("div",{"class":"inline-block ratings-imdb-rating"})
cleansing_rating=[]
for r in ratings:
  cleansing_rating.append(r.strip())
print(cleansing_rating)

import pandas as pd
imdb_2023=pd.DataFrame(data = {
    "movie_titles": cleansing_titles,
    "movie_rating": cleansing_rating
})
print(imdb_2023)
imdb_2023.reset_index()

imdb_2023.to_csv("imdb_2023")


