import requests

API_KEY = "YOUR_API_KEY_HERE"  # Replace with your actual key
BASE_URL = "http://api.openweathermap.org/data/2.5/weather"

def get_weather(city):
    params = {
        'q': city,
        'appid': API_KEY,
        'units': 'metric'
    }
    response = requests.get(BASE_URL, params=params)
    
    if response.status_code == 200:
        data = response.json()
        print(f"\nWeather in {data['name']} ({data['sys']['country']}):")
        print(f"Temperature: {data['main']['temp']}°C")
        print(f"Weather: {data['weather'][0]['description'].capitalize()}")
        print(f"Humidity: {data['main']['humidity']}%")
        print(f"Wind Speed: {data['wind']['speed']} m/s")
    else:
        print("\n❌ City not found. Please try again.")

def main():
    print("=== Weather Dashboard ===")
    while True:
        city = input("\nEnter city name (or type 'exit' to quit): ")
        if city.lower() == 'exit':
            break
        get_weather(city)

if __name__ == "__main__":
    main()
