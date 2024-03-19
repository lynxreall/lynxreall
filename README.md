import requests
import json

class LynxReal:
    @staticmethod
    def channels() -> str:
        """
        Returns the Discord channel for professional communication.

        :return: Discord channel link
        """
        discord = "discord.gg/perdition-development-978347894706950215"
        return discord

    @staticmethod
    def contact() -> str:
        """
        Returns the preferred contact handle for professional inquiries.

        :return: Discord handle
        """
        discord = "lynxreal"
        return discord

    @staticmethod
    def life() -> tuple:
        """
        Returns information about language proficiency and age.

        :return: Tuple containing languages and age
        """
        langs = ['Turkish']
        age = 18
        return langs, age

    @staticmethod
    def coding() -> tuple:
        """
        Returns information about coding expertise, specialties, and development environment.

        :return: Tuple containing languages, specialties, and development environment
        """
        langs = {
            'expert': ['js'],
            'beginning': ['html', 'c#'],
            'learning': ['golang']
        }
        specialities = ['web/app reverse engineering', 'fullstack']
        environment = ['vscode']
        return langs, specialities, environment

# Lanyard API'den veri çekme
response = requests.get('https://api.lanyard.rest/v1/users/978347894706950215')
data = response.json()

# Alınan verileri GitHub Actions için düzenleme
github_data = {
    "schemaVersion": 1,
    "label": "Discord Status",
    "message": f"{data['data']['discord_user']['username']} is {data['data']['listening_to_spotify']['song']}",
    "color": "blue"
}

# GitHub Actions için json dosyası oluşturma
with open('data.json', 'w') as json_file:
    json.dump(github_data, json_file)
