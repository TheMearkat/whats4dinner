# This is my app that will help you choose what's for dinner.

import tkinter as tk
from io import BytesIO
from PIL import Image, ImageTk
import requests
import random
import configparser

# Read API key from configuration file for privacy
config = configparser.ConfigParser()
config.read('config.ini')

# Function to fetch restaurant data from Yelp API
def get_restaurant_data(cuisine, location='Dallas'):
    api_key = config.get('API','key')
    url = f'https://api.yelp.com/v3/businesses/search?categories={cuisine}&location={location}&open_now=true&sort_by=best_match'
    headers = {'accept': 'application/json', 'Authorization': f'Bearer {api_key}'}
    response = requests.get(url, headers=headers)
    return response.json()

# Function to pick a random restaurant
def pick_restaurant():
    random_cuisine = random.choice(cuisines)
    data = get_restaurant_data(random_cuisine)

    if 'businesses' in data and len(data['businesses']) > 0:
        random_restaurant = random.choice(data['businesses'])
        restaurant_name = random_restaurant['name']
        image_url = random_restaurant['image_url']
        display_restaurant_image(image_url)
    else:
        restaurant_name = 'No restaurant found'
        clear_restaurant_image()

    # Update the label with the selected restaurant
    label.config(text=restaurant_name)

# Function to display the restaurant image
def display_restaurant_image(url):
    response = requests.get(url)
    if response.status_code == 200:
        image_data = response.content
        image = Image.open(BytesIO(image_data))
        image = image.resize((300, 300))  # Adjust the image size as desired
        photo = ImageTk.PhotoImage(image)
        image_label.config(image=photo)
        image_label.image = photo
        window.geometry("500x500")
    else:
        clear_restaurant_image()
        window.geometry("500x500")  # Default window size

# Function to clear the restaurant image
def clear_restaurant_image():
    image_label.config(image='')

# Your list of cuisines
if __name__ == '__main__':
    cuisines = ['Afghan', 'African', 'Senegalese', 'South African', 'American (New)', 'American (Traditional)',
                'Arabian', 'Argentine', 'Armenian', 'Asian Fusion', 'Australian', 'Austrian', 'Bangladeshi', 'Barbeque',
                'Basque', 'Belgian', 'Brasseries', 'Brazilian', 'Breakfast & Brunch', 'British', 'Buffets', 'Burgers',
                'Burmese', 'Cafes', 'Cafeteria', 'Cajun', 'Cambodian', 'Caribbean', 'Puerto Rican', 'Chicken Wings',
                'Chinese', 'Cantonese', 'Dim Sum', 'Szechuan', 'Comfort Food', 'Creperies', 'Cuban', 'Czech', 'Delis',
                'Diners', 'Ethiopian', 'Fast Food', 'Filipino', 'Fish & Chips', 'Fondue', 'Food Court', 'Food Stands',
                'French', 'Gastropubs', 'German', 'Gluten-Free', 'Greek', 'Halal', 'Hawaiian', 'Himalayan/Nepalese',
                'Hot Dogs', 'Hot Pot', 'Hungarian', 'Iberian', 'Indian', 'Indonesian', 'Irish', 'Italian', 'Japanese',
                'Korean', 'Kosher', 'Laotian', 'Latin American', 'Columbian', 'Salvadoran', 'Venezuelan',
                'Malaysian', 'Meditteranean', 'Mexican', 'Middle Eastern', 'Egyptian', 'Lebanese',
                'Mongolian', 'Pakistani', 'Persian/Iranian', 'Peruvian', 'Pizza', 'Polish', 'Portuguese', 'Russian',
                'Salad', 'Sandwiches', 'Scandinavian', 'Scottish', 'Seafood', 'Singaporean', 'Soul Food',
                'Soup', 'Southern', 'Spanish', 'Steakhouses', 'Sushi Bars', 'Taiwanese', 'Tapas Bars',
                'Tapas/Small Plates', 'Tex-Mex', 'Thai', 'Turkish', 'Ukranian', 'Vegan', 'Vegetarian', 'Vietnamese']

    window = tk.Tk()
    # Create a label widget
    label = tk.Label(
        text="What's 4 Dinner",
        fg="black",
        width=50,
        height=2
    )
    label.pack()

    # Create an image label widget
    image_label = tk.Label()
    image_label.pack()

    # Create a button widget
    button = tk.Button(
        text="Pick Restaurant",
        width=20,
        height=5,
        command=pick_restaurant
    )
    button.pack()

    # Initial window size
    window.geometry("500x500")

    window.mainloop()
