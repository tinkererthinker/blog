---
title: "Created a python program to export games played from chess.com and open analysis board for them in lichess"
source: "https://www.reddit.com/r/chess/comments/11kebcn/created_a_python_program_to_export_games_played/"
author:
  - "[[Reasonable-Review-22]]"
published: 2023-03-06
created: 2025-01-25
description: "Hey everyone, I created a python program to export your games played from chess.com and open analysis board for them in lichess as I found"
tags:
  - "clippings"
---
Hey everyone, I created a python program to export your games played from [chess.com](https://chess.com/) and open analysis board for them in lichess as I found it very rigorous to copy pgn from [chess.com](https://chess.com/), open analysis board on lichess and them import the pgn.

## Here is the code:

```md
import threading
import webbrowser
import chessdotcom
import requests

USERNAME = 'username_here'
API_KEY = 'lichess_API_key_here'

NO_OF_GAMES = int(
    input("Enter the no of games you want to analyse from the last game: "))

# Get the pgn of recent game of chess.com
def get_game_pgn(game_from_last):
    data = chessdotcom.get_player_game_archives(USERNAME)
    url = data.json['archives'][-1]  # pylint: disable=E1101
    export_response = requests.get(url, timeout=10)
    export_response.raise_for_status()
    pgn = export_response.json()['games'][-game_from_last]['pgn']
    return pgn

# Import the above pgn into lichess for analysis and set the URL and headers for the API request
URL = 'https://lichess.org/api/import'
headers = {'Authorization': f'Bearer {API_KEY}'}

# set the PGN content and analysis options
def analyse_on_lichess(pgn):
    pgn_content = pgn
    analysis_options = {
        'analyse': True,
        'async': True,
    }

    # send the POST request to the API
    import_response = requests.post(URL, headers=headers, data={
        'pgn': pgn_content,
        'analyseData': analysis_options,
    }, timeout=10)

    # parse the analysis URL from the response content
    response_json = import_response.json()
    analysis_url = response_json['url']

    # open the analysis URL in a new browser window
    webbrowser.open(analysis_url)

# Using multithreading to speed the process of opening multiple websites
if __name__ == '__main__':
    games = []
    for i in range(NO_OF_GAMES):
        thread = threading.Thread(
            target=analyse_on_lichess, args=[get_game_pgn(i + 1)])
        games.append(thread)
        thread.start()

    for game in games:
        game.join()
```

## How to use:

1. First of all you will need python installed which you can get from this [website](https://www.python.org/). (Make sure to tick the add path variable while installing)
2. Then you need to create [lichess api key](https://lichess.org/account/oauth/token) and enable external study and analysis check boxes.
3. Then open command prompt and type python (for windows) and python3 (for mac) to see if you have python installed. If yes you have to install a few dependencies for this to work.
4. Run these commands:

- `pip install requests`
- `pip install` [`chess.com`](https://chess.com/)

After this, save this code in a file with {filename}.py and open command prompt at that location.

Type in command prompt python `{filename}.py` to run the file.

It will ask the number of games starting from the latest games that you want to analyse, so type in the required amount and wait for it open the analysis board in the browser.

## Now enjoy analyzing

---

## Comments

> **Continental\_\_Drifter** • [6 points](https://reddit.com/r/chess/comments/11kebcn/comment/jb7pbyy/) • 2023-03-07
> 
> why not just... play on lichess in the first place
> 
> this seems like a software equivalent of a rube goldberg machine
> 
> > **Reasonable-Review-22** • [2 points](https://reddit.com/r/chess/comments/11kebcn/comment/jb89env/) • 2023-03-07
> > 
> > I have many friends who play only on chess.com and also I have a decent rating there, but I play on both the website, but lichess mainly for puzzles

> **\[deleted\]** • [\-8 points](https://reddit.com/r/chess/comments/11kebcn/comment/jb6tgqp/) • 2023-03-06
> 
> Oh wow, the 1001th program that does the same thing 😂
> 
> By the way, next time just ask chat GPT to write it for you
> 
> > **Reasonable-Review-22** • [1 points](https://reddit.com/r/chess/comments/11kebcn/comment/jb6y67w/) • 2023-03-06
> > 
> > I asked it to write but was not very reliable, but used some of its snippets