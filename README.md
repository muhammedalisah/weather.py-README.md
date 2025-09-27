# weather.py-README.md
To-Do List App in pyt
# Python To-Do List App

Basit bir komut satırı yapılacaklar listesi uygulaması.

## Özellikler
- Görev ekleme
- Görevleri listeleme
- Görevleri silme

## Kullanım
```bash
python todo.py add "alışveriş yap"
python todo.py list
python todo.py remove 1
# Weather CLI App

OpenWeatherMap API kullanarak hava durumu bilgisini getirir.

## Kullanım
```bash
python weather.py Istanbul

4. Sayfanın en altındaki **Commit changes** butonuna tıkla.

---

## C. Kod Dosyası Ekle (weather.py)
1. Repo ana sayfasında → **Add file → Create new file** seç.  
2. Dosya adı: `weather.py` yaz.  
3. İçine bu kodu yapıştır:  

```python
import requests
import sys

API_KEY = "YOUR_API_KEY"  # Buraya OpenWeatherMap API Key'inizi yazın
BASE_URL = "https://api.openweathermap.org/data/2.5/weather"

def get_weather(city):
    url = f"{BASE_URL}?q={city}&appid={API_KEY}&units=metric&lang=tr"
    response = requests.get(url)
    if response.status_code == 200:
        data = response.json()
        print(f"{city} için hava durumu:")
        print(f"Sıcaklık: {data['main']['temp']}°C")
        print(f"Durum: {data['weather'][0]['description']}")
    else:
        print("Hava durumu alınamadı. Şehri doğru yazdığınızdan emin olun.")

if __name__ == "__main__":
    if len(sys.argv) > 1:
        city = " ".join(sys.argv[1:])
        get_weather(city)
    else:
        print("Kullanım: python weather.py Istanbul")
