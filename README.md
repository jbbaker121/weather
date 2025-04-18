# Weather
Generating the real-time weather of any location

import requests

def get_weather(city_name, api_key):
    # Base URL of OpenWeatherMap API
    base_url = "http://api.openweathermap.org/data/2.5/weather"

    # Parameters for the request
    params = {
        "q": city_name,
        "appid": api_key,
        "units": "metric"  # use "imperial" for Fahrenheit
    }

    # Send GET request
    
    response = requests.get(base_url, params=params)
    
    # Convert to JSON
    
    data = response.json()

    if response.status_code == 200:
        # Extract data
        
        temp = data["main"]["temp"]
        weather = data["weather"][0]["description"]
        print(f"\nWeather in {city_name}:\nTemperature: {temp}°C\nCondition: {weather}")
    else:
        print("\nCity not found or error occurred.")

# === Run the app ===
if __name__ == "__main__":
    api_key = "YOUR_API_KEY_HERE"  # Replace with your OpenWeatherMap API key
    city = input("Enter a city name: ")
    get_weather(city, api_key)
