# homework api
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
