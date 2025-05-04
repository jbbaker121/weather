import requests
import tkinter as tk
from tkinter import messagebox
# Create the main window
root = tk.Tk()
root.title("Weather App")

# Create the entry field for input
city_label = tk.Label(root, text="City:")
city_label.pack()
city_entry = tk.Entry(root)
city_entry.pack()

# Create a button to fetch weather data
fetch_button = tk.Button(root, text="Fetch Weather")
fetch_button.pack()

# Create a label to display weather information
weather_label = tk.Label(root, text="")
weather_label.pack()

# Define the function to fetch weather data
def fetch_weather():
    city = city_entry.get()
    # Add your API key here
    api_key = "3311c1c85ee040b5b32174905251804"
    url = f"http://api.weatherapi.com/v1/current.json?key={api_key}&q={city}"

    
    try:
        response = requests.get(url)
        data = response.json()

        # Weather Searching Structure for WeatherAPI
        temperature = data["current"]["temp_c"]
        weather = data["current"]["condition"]["text"]

        weather_label.config(text=f"Temperature: {temperature}°C\nWeather: {weather}")
    except Exception as e:
        messagebox.showerror("Error", "Unable to fetch weather data")

fetch_button.config(command=fetch_weather)

# Start the GUI main loop
root.mainloop()
