# oibsip_taskno.1 (weather forecasting)
#arnav tyagi
import requests
import json

def get_weather(api_key, location):
    base_url = "http://api.openweathermap.org/data/2.5/weather"

    # Prepare parameters for the API request
    params = {
        'q': location,
        'appid': api_key,
        'units': 'metric'  # Use 'imperial' for Fahrenheit
    }

    try:
        # Make the API request
        response = requests.get(base_url, params=params)
        data = response.json()

        # Check if the request was successfulr̥
        if response.status_code == 200:
            return data
        else:
            print(f"Error: {data['message']}")
            return None

    except requests.RequestException as e:
        print(f"Request Error: {e}")
        return None

def display_weather(data):
    if data:
        temperature = data['main']['temp']
        humidity = data['main']['humidity']
        weather_condition = data['weather'][0]['description']

        print("\nCurrent Weather:")
        print(f"Temperature: {temperature}°C")
        print(f"Humidity: {humidity}%")
        print(f"Weather Condition: {weather_condition}")
    else:
        print("Unable to fetch weather data.")

def main():
    print("Command-line Weather App")
    print("------------------------")

    # Input your OpenWeatherMap API key
    api_key = input("Enter your OpenWeatherMap API key: ")

    # Input the location (city or ZIP code) from the user
    location = input("Enter the city or ZIP code: ")

    # Get weather data
    weather_data = get_weather(api_key, location)

    # Display weather information
    display_weather(weather_data)

if __name__ == "__main__":
    main()
