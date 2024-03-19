import requests

class Attributes(lynxreal):
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
        langs = ['Turkish',]
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
        environnement = ['vscode']
        return langs, specialities, environnement

def get_spotify_data(user_id):
    url = f"https://api.lanyard.rest/v1/users/{user_id}"
    response = requests.get(url)
    
    if response.status_code == 200:
        data = response.json()
        spotify = data.get('listening_to_spotify', None)
        
        if spotify:
            track_info = spotify.get('track', None)
            if track_info:
                track_name = track_info.get('song', 'Unknown')
                artist_name = track_info.get('artist', 'Unknown')
                album_cover = track_info.get('album_art_url', None)
                
                return {
                    'track_name': track_name,
                    'artist_name': artist_name,
                    'album_cover': album_cover
                }
            else:
                return "Spotify kullanıcının şu anda dinlediği bir şarkı yok."
        else:
            return "Kullanıcı şu anda Spotify'da aktif değil."
    else:
        return "API'den veri alınamadı."

# Kullanıcı kimliği
user_id = "978347894706950215"

# Spotify verilerini al
spotify_data = get_spotify_data(user_id)

# Sonuçları yazdır
print("Spotify Verileri:")
print(spotify_data)
