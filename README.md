import os
import requests
import datetime
import random

# API to get a random motivational quote
API_URL = "https://api.quotable.io/random"

def get_random_quote():
    try:
        response = requests.get(API_URL)
        data = response.json()
        return f'"{data["content"]}" — {data["author"]}'
    except:
        # Fallback message if API fails
        fallback_quotes = [
            "Believe you can and you're halfway there. — Theodore Roosevelt",
            "The only way to do great work is to love what you do. — Steve Jobs",
            "Success is not final, failure is not fatal: it is the courage to continue that counts. — Winston Churchill"
        ]
        return random.choice(fallback_quotes)

# Get quote
quote = get_random_quote()

# Append to quotes file
with open("motivational_quotes.txt", "a", encoding="utf-8") as f:
    f.write(f"{datetime.datetime.now()}: {quote}\n")

# Git commands
os.system("git add motivational_quotes.txt")
os.system(f'git commit -m "Added motivational quote: {quote[:50]}..."')
os.system("git push")

print(f"✅ Commit pushed with motivational quote: {quote}")
