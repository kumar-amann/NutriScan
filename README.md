# NutriScan🥗
NutriScan: "Revitalize your wellness, one bite at a time with NutriScan!". Powered by the Gemini Pro-Vision API and built on Streamlit, transforms nutrition tracking. Easily obtain calorie values by inputting images, making your fitness goals more achievable. NutriScan acts as your personal nutritionist bot, seamlessly integrated and user-friendly.Take charge of your health and enjoy informed nutritional decisions with NutriScan.

# Live Link: 
https://aman-nutriscan.streamlit.app/
# Demo Video:


#Introduction
In the age of information overload, it’s more important than ever to have tools that simplify healthy choices. Enter NutriScan🥗, a revolutionary app that puts a personal nutritionist✨ right in your pocket. Powered by Google’s Gemini Pro Vision AI, it takes the guesswork out of meal planning and calorie tracking, making it easier than ever to achieve your wellness goals✨.

The NutriScan app🥗 is designed to help users analyze🔍 the nutritional content📄 of their meals by leveraging advanced image recognition technology with the help of Generative AI💡. Users can upload an image🖼️of their food, and the app will provide details about each item along with the total calorie count💪✨. The app utilizes Google’s Gemini Pro Vision API for content generation and Streamlit for building the user interface.
![image](https://github.com/kumar-amann/NutriScan/assets/137410641/2817b6e0-d77e-494e-a942-ca72506d8da5)



“Let food be thy medicine, and medicine be thy food.” — Hippocrates
“What we eat should not simply fill the stomach; it should nourish the soul.” — — ✨G.K. Chesterton✨

#Explore the Live Project:
You can access the live version of the NutriScan app💪 by visiting the following URL: 🔗 NutriScanAppLiveProjectLink


#NutriScan App Interface
A Glimpse into the Tech Behind the Scenes
NutriScan🥗 leverages the cutting-edge Google Gemini Pro Vision API to analyze food items from images🖼️, calculate total calories, and deliver detailed information about each item’s caloric intake. Let’s delve into the technology stack that powers this intelligent nutrition app✨.

#Unveiling the Technology Behind NutriScan :
At the heart of NutriScan lies a sophisticated technology stack that seamlessly integrates AI capabilities ✨with nutrition expertise. Let’s take a closer look at the underlying technologies that power NutriScan’s intelligent nutrition management.

1. Setting Up the Environment:
Our NutriScan app kicks off by establishing a robust environment. The .env file stores sensitive information like API keys, ensuring secure access to external services. Utilizing the dotenv library, we load these variables for seamless integration. The app is built using Streamlit, a powerful Python library💪 for creating web applications. Additionally, we leverage the Google Generative AI library and the ever-reliable Pillow library (PIL) for image processing.

from dotenv import load_dotenv
load_dotenv() 
import streamlit as st
import os
import google.generativeai as genai
from PIL import Image
genai.configure(api_key=os.getenv("GOOGLE_API_KEY"))
2. Connecting to Google’s Gemini Pro Vision API:
The heartbeat of NutriScan lies in its ability to interpret images and generate insightful content. The get_gemini_response function orchestrates this connection with the Google Gemini Pro Vision API. It takes inputs such as the user query, uploaded image, and a prompt. The API✨ then processes this information and responds, unraveling the nutritional details of the food items in the image🖼️.

Two main functions handle the interaction with the Gemini Pro Vision API:

(i). get_gemini_response: This function takes an input, an image, and a prompt. It uses the Gemini Pro Vision model to generate content based on these inputs and returns the API response.

def get_gemini_response(input, image, prompt):
    model = genai.GenerativeModel('gemini-pro-vision')
    response = model.generate_content([input, image[0], prompt])
    return response.text
(ii). input_image_setup: This function prepares the uploaded image for processing. It checks if a file has been uploaded, reads the file into bytes, and returns the image data🖼️📄 in the required format.

def input_image_setup(uploaded_file):
    if uploaded_file is not None:
        bytes_data = uploaded_file.getvalue()
        image_parts = [
            {
                "mime_type": uploaded_file.type,
                "data": bytes_data
            }
        ]
        return image_parts
    else:
        raise FileNotFoundError("No file uploaded")
3. Streamlit App Initialization:
Upon launching the app, users are greeted with an inviting interface. The Streamlit app is configured with a title, header, and an interactive text input field prompting users to share additional details about the uploaded image✨. The file uploader feature allows users to seamlessly upload an image of their meal, while the app dynamically displays the uploaded image.

st.set_page_config(page_title="NutriScan App")

st.header("NutriScan 🥗")
st.write("Revitalize Your Wellness, One Bite at a Time with NutriScan!😋")
input = st.text_input("Let me Check : ", key="input")
uploaded_file = st.file_uploader("Choose an image...", type=["jpg", "jpeg", "png"])
image = ""   
if uploaded_file is not None:
    image = Image.open(uploaded_file)
    st.image(image, caption="Uploaded Image.", use_column_width=True)
4. Engaging with NutriScan:
Users can actively participate in their nutrition journey by providing additional details in the text input field. Upon clicking the “Tell me the total calories” button, the app processes both the uploaded image🖼️ and user input. The intricate dance between the input_image_setup function and the get_gemini_response function transforms this information into a detailed nutritional analysis.

submit = st.button("Tell me the total calories")

input_prompt = """
You are an expert in nutritionist where you need to see the food items from the image
               and calculate the total calories, also provide the details of every food items with calories intake
               in below format:

               1. Item 1 - no of calories   
               2. Item 2 - no of calories
               ----
               ----
"""

if submit:
    image_data = input_image_setup(uploaded_file)
    response = get_gemini_response(input_prompt, image_data, input)
    st.subheader("The Response is")
    st.write(response)
    
#NutriScan in Action:
User-Friendly Interface: NutriScan boasts an intuitive interface, allowing users to effortlessly input their queries and upload images🖼️ for analysis.
AI-Powered Analysis: Behind the scenes, NutriScan employs the Google Gemini Pro Vision API,✨ a generative AI model, to analyze food items and provide accurate details on caloric content.
Detailed Caloric Information: Upon submitting a request, NutriScan delivers a detailed breakdown of each food item’s caloric intake✨, following the specified format.
Technologies Used in NutriScan App
1. Python 🐍
Python serves as the backbone of NutriScan, providing a versatile and powerful programming language for implementing the app’s core functionality. Its readability and extensive libraries make it an ideal choice for handling complex tasks seamlessly.

2. Streamlit 🌟
Streamlit is the framework of choice for NutriScan’s user interface. Its simplicity and interactive features make it easy to create a user-friendly environment where users can input data and receive real-time nutrition analysis.

3. Google Gemini Pro Vision API 🧠
The Google Gemini Pro Vision API is the powerhouse behind NutriScan’s AI capabilities. Leveraging generative AI models, this API processes images, understands nutrition-related queries, and provides detailed responses to empower users with valuable insights.

4. PIL (Python Imaging Library) 🖼️
The Python Imaging Library (PIL) is utilized for handling image-related operations within NutriScan. It ensures that uploaded images are processed seamlessly, allowing for a smooth user experience.


#The NutriScan Feature:
1. Personalized Nutrition Guidance: NutriScan acts as your nutritionist, offering tailored insights into the caloric content of your meals✨. Whether you’re tracking your daily intake or planning a new dietary regimen, NutriScan provides the information you need to make informed decisions.

2. Effortless and Quick: Gone are the days of manual calorie counting. NutriScan streamlines the process, making it as simple as uploading an image and clicking a button. The AI-powered analysis ensures quick and accurate results✨.

3. Informed Food Choices: With NutriScan, you gain a deeper understanding of your food choices. The detailed breakdown allows you to identify high-calorie items, balance your meals, and work towards your health and wellness goals💪.

#Challenges Faced During Development:
The development journey of NutriScan was marked by various challenges, each serving as a stepping stone towards creating a robust and user-friendly nutrition management app. Here’s a glimpse into the hurdles we faced and conquered📑:

1. Integration of Google Gemini Pro Vision API:

The seamless integration of the Google Gemini Pro Vision API was a significant challenge. Navigating through the intricacies of the API documentation and establishing a reliable connection demanded meticulous attention.

Solution: Rigorous testing and collaboration with API documentation allowed us to create a robust integration. Continuous monitoring ensures NutriScan’s dependence on Google Gemini Pro Vision remains efficient.

2. User-Friendly Interface Design:

Designing an interface that caters to users with varying technical backgrounds posed a challenge. We aimed to create an app that is both intuitive and user-friendly, ensuring a seamless experience for everyone.

Solution: Extensive user testing and feedback sessions were conducted to refine the interface. Iterative design improvements were implemented based on user input, resulting in an interface that prioritizes simplicity and functionality.

3. Streamlit and Python Compatibility:

Integrating Streamlit with the existing Python codebase and ensuring compatibility presented its own set of challenges. Streamlit’s continuous updates required adaptation to keep the app seamlessly functional.

Solution: Regular updates and testing of NutriScan with the latest Streamlit versions ensured compatibility. The use of modular and well-documented code facilitated smooth integration and adaptability to changes.

#Future Plans for Overcoming Challenges:
Challenges are an inherent part of app development, and our commitment extends to proactively addressing emerging obstacles. NutriScan’s future updates will focus on overcoming new challenges and continually enhancing user experiences.

Facing and conquering these challenges during NutriScan’s development journey has not only strengthened the app but has also shaped it into a reliable and user-centric nutrition management tool. We remain dedicated to addressing new challenges as they arise, ensuring NutriScan continues to empower💪 users on their wellness journey.

#The Future of NutriScan:
NutriScan is not just an app; it’s a commitment to your well-being. Our development roadmap includes exciting features✨ to further enhance your nutrition management experience📑:

Meal Planning Integration: Seamlessly integrate NutriScan with meal planning apps to create comprehensive and personalized nutrition plans.
Nutritional Trends Analysis: Track your nutritional trends over time, allowing you to make proactive adjustments to your diet for optimal health.
Interactive Nutritional Workshops: Engage in interactive workshops within the app, providing you with expert insights and guidance on nutrition.
Community Collaboration: Connect with like-minded individuals, share your nutrition journey, and gain inspiration from the NutriScan community.

#Conclusion: Empowering Your Nutritional Choices
NutriScan is not just an app; it’s your virtual nutritionist, ready to empower you on your journey towards healthier eating habits✨. By combining the sophistication of Google’s Gemini Pro Vision API and the accessibility of Streamlit, NutriScan makes nutrition management a breeze. Whether you’re a health enthusiast✨ or someone looking to make more informed dietary choices.

NutriScan is here to “revitalize your wellness, one bite at a time”. Explore the app, embrace the insights, and embark on a healthier lifestyle with NutriScan! 🌱🍏

#Glimpse of NutriScan🖼️:
Check out these screenshots to get a glimpse of NutriScan in action:
![image](https://github.com/kumar-amann/NutriScan/assets/137410641/3b0c32cc-af01-46e5-84e0-f2e8fcd77c2f)


NutriScan App landing page interface



![image](https://github.com/kumar-amann/NutriScan/assets/137410641/479d56a7-9d89-408c-a7b8-295d67785677)

Ask your questions and give the image as input for analyzing your meal.
![image](https://github.com/kumar-amann/NutriScan/assets/137410641/da12970e-44be-4595-afae-1025078ba7ec)


The Nutritionist Response by NutriScan
Join the NutriScan Revolution:
Embark on a journey towards healthier living with NutriScan. Experience the power of AI-driven nutrition analysis📑, simplified for your convenience. Whether you’re a fitness 💪 enthusiast, a wellness advocate, or someone starting their nutrition journey, NutriScan is here to support you✨.

Provide Your Feedback
We value your feedback and suggestions for improving NutriScan. If you have any ideas💡, feature requests🚀, or general comments💬, please don’t hesitate to reach out us. We are committed to continually enhancing NutriScan based on your needs and preferences. ✨🙌
