import requests

API_KEY = '3311c1c85ee040b5b32174905251804'
BASE_URL = 'http://api.weatherapi.com/v1/current.json'

# Ask the user for a location
location = input("Enter a city or location: ")

# Build the request URL
url = f"{BASE_URL}?key={API_KEY}&q={location}"

# Make the request
response = requests.get(url)

# Parse the JSON response
if response.status_code == 200:
    data = response.json()
    location_name = data['location']['name']
    region = data['location']['region']
    country = data['location']['country']
    temp_c = data['current']['temp_c']
    condition = data['current']['condition']['text']
    humidity = data['current']['humidity']
    wind_kph = data['current']['wind_kph']

    print(f"Weather for {location_name}, {region}, {country}:")
    print(f"Temperature: {temp_c}°C")
    print(f"Condition: {condition}")
    print(f"Humidity: {humidity}%")
    print(f"Wind Speed: {wind_kph} kph")

else:
    print("Error fetching weather data. Please check the city name or try again later.")
