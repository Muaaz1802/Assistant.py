# Assistant.py
# Here is a simple virtual assistant which performs some sort of basic tasks.

import pyttsx3  # for voice --> text to speech
import speech_recognition as sr  # for voice recognition --> speech to text
import time
from datetime import datetime
import os
import webbrowser
from PIL import ImageGrab
import wikipedia


def speak(audio):
    engine = pyttsx3.init()
    engine.say(audio)
    engine.runAndWait()


r = sr.Recognizer()


def greet():

    currentHour = datetime.now().hour

    if currentHour >= 4 and currentHour < 12:
        print("Good morning sir! I'm Max, how may I help you?")
        speak("Good morning sir! I'm Max, how may I help you?")

    elif currentHour >= 12 and currentHour < 17:
        print("Good afternoon sir! I'm Max, how may I help you?")
        speak("Good afternoon sir! I'm Max, how may I help you?")

    elif currentHour >= 17 and currentHour < 22:
        print("Good evening sir! I'm Max, how may I help you?")
        speak("Good evening sir! I'm Max, how may I help you?")

    else:
        print("Hello sir! I'm Max, how may I help you?")
        speak("Hello sir! I'm Max, how may I help you?")


def takeSS():
    time.sleep(2)
    image = ImageGrab.grab()
    print("Showing image")
    speak("Showing image")
    image.show()


if __name__ == "__main__":

    os.system("cls")

    greet()

    while True:

        try:
            print("Listening.....")
            with sr.Microphone() as source:  # uses the microphone as a source for speech to text
                # adjusting voice inputs
                r.adjust_for_ambient_noise(source, duration=0.5)

                audio = r.listen(source)

                # uses google to recognise audio
                userQuery = r.recognize_google(audio)
                userQuery = userQuery.lower()

                print("Recognising....")
                time.sleep(1)

                print("You said: " + userQuery)

        except sr.RequestError as e:
            speak("I'm Sorry, Say that again plaese!")
            print(e)
            continue

        except sr.UnknownValueError:
            print("I'm sorry I didn't recognised it. Say it again please!")
            speak("I'm sorry I didn't recognised it. Say it again please!")
            continue

        # query checking

        # program exit
        if 'quit' in userQuery:
            print("OK bye! Let Me know if you need some help.")
            speak("OK bye! Let Me know if you need some help.")
            quit()

        # youtube
        elif 'open youtube' in userQuery:
            print("Opening YouTube....")
            speak("Opening YouTube....")
            webbrowser.open("https://www.youtube.com/")

        # stackoverdflow
        elif 'open stackoverflow' in userQuery:
            print("Opening StackOverflow....")
            speak("Opening stackoverflow....")
            webbrowser.open("https://stackoverflow.com/")

        # github
        elif 'open github' in userQuery:
            print("Opening Github....")
            speak("Opening Github....")
            webbrowser.open("https://github.com/")

        # vs code
        elif 'open code' in userQuery:
            print("Opening VS code....")
            speak("Opening VS code....")
            webbrowser.open("https://vscode.dev/")

        # whatsapp
        elif 'open whatsapp' in userQuery:
            print("Opening WhatsApp....")
            speak("Opening WhatsApp....")
            webbrowser.open("https://web.whatsapp.com/")

        # telegram
        elif 'open telegram' in userQuery:
            print("Opening telegram....")
            speak("Opening telegram....")
            webbrowser.open("https://web.telegram.org/k/")

        # ss
        elif 'take screenshot' in userQuery:
            print("On it!")
            speak("On it!")
            takeSS()

        # wiki
        elif 'wikipedia' in userQuery:
            print('Searching Wikipedia...')
            speak('Searching Wikipedia...')
            userQuery = userQuery.replace("wikipedia", "")
            results = wikipedia.summary(userQuery, sentences=3)
            print("According to Wikipedia...")
            speak("According to Wikipedia...")
            print(results)
            speak(results)

        # time
        elif 'the time' in userQuery:
            strTime = datetime.now().strftime("%H:%M:%S")
            print(f"Sir, the time is {strTime}")
            speak(f"Sir, the time is {strTime}")

        # weather
        elif 'weather' in userQuery:
            print("Opening Weather details")
            speak("Opening Weather details")
            webbrowser.open(
                "https://www.google.com/search?q=weather&oq=weather&aqs=chrome..69i57j0i67i650j0i67i131i433i457i650j0i402i650j0i67i131i433i650j0i131i433i512j69i60l2.2157j1j1&sourceid=chrome&ie=UTF-8")
        
        elif 'open google' in userQuery:
            print("Opening Google....")
            speak("Opening Google....")
            webbrowser.open("https://www.google.co.in/")
