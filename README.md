import request
import sys
import os

API_KEY = os.getenv("OPENWEATHER_API_KEY") or "YOUR_API_KEY"
BASE_URL = "https://api.openweathermap.org/data/2.5/weather"

def get_weather(city):
    if API_KEY == "YOUR_API_KEY":
        print("⚠️  API KEY bulunamadı! Lütfen bir OpenWeatherMap API key ekleyin.")
        return

    try:
        url = f"{BASE_URL}?q={city}&appid={API_KEY}&units=metric&lang=tr"
        response = requests.get(url, timeout=5)

        if response.status_code == 404:
            print("❌ Şehir bulunamadı. Lütfen doğru yazdığınızdan emin olun.")
            return

        response.raise_for_status()  # diğer hataları yakalar
        data = response.json()

        print(f"\n🌤  {city} için hava durumu:")
        print(f"🌡  Sıcaklık: {data['main']['temp']}°C")
        print(f"🤔 Hissedilen: {data['main']['feels_like']}°C")
        print(f"💧 Nem: {data['main']['humidity']}%")
        print(f"🌬  Rüzgar: {data['wind']['speed']} m/s")
        print(f"☁️  Durum: {data['weather'][0]['description'].capitalize()}\n")

    except requests.exceptions.Timeout:
        print("⏳ Sunucu geç yanıt verdi. Lütfen tekrar deneyin.")
    except requests.exceptions.ConnectionError:
        print("📡 İnternet bağlantısı bulunamadı.")
    except Exception as e:
        print(f"⚠️ Beklenmeyen bir hata oluştu: {e}")


if __name__ == "__main__":
    if len(sys.argv) > 1:
        city = " ".join(sys.argv[1:])
        get_weather(city)
    else:
        print("Kullanım: python weather.py Istanbul")

