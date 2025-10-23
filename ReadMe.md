School Signage Project

How Our School's Digital Signage Works
Welcome! This guide explains our digital signage system. It's designed to be simple, with all the "brains" in a single file and all the content managed through Google and GitHub.

The Big Picture 🗺️
The "digital sign" is just a simple webpage (index.html) running in Kiosk Mode on the Chromebits attached to our TVs.

This webpage has three main jobs:

By default, it shows a looping Google Slides presentation.

It checks a Google Calendar every minute. If it finds a scheduled event (like "Assembly"), it will interrupt the slideshow to show that announcement.

It reads a text file (ticker.txt) to display the scrolling banner at the bottom.

The 3 Key Components
You only need to know about three places to manage everything:

GitHub Repository (The "Brain" & "Host"):

Where: https.github.com/iesv-swe/IESV_TV

This holds our two code files: index.html (the main app) and ticker.txt (the banner text).

We use GitHub Pages to host this code as a live website. The TV Chromebits are pointed to this website: https://iesv-swe.github.io/IESV_TV/

Google Slides (The "Content"):

These are the looping slideshows that show by default.

We have two different slide decks (one for Junior, one for Senior), which are defined in the index.html file.

To update the default slides, you just edit the Google Slide deck. That's it. The changes are live immediately.

Google Calendar (The "Remote Control"):

This is how you schedule announcements.

We have two calendars: "Junior TV Schedule" and "Senior TV Schedule."

When you create an event, the description field is used to send a command to the TV.

How to Use It (Day-to-Day)
This is what you'll be doing most often.

How to Update the Ticker Banner
Go to the GitHub repository: iesv-swe/IESV_TV.

Click on the ticker.txt file.

Click the pencil icon (Edit) in the top-right.

Change the text.

Click the green "Commit changes" button.

The TV will update within 5 minutes.

How to Schedule an Announcement (Show a Specific Slide)
Use this to show a single slide (like "Lunch Menu" or "Welcome") at a specific time.

Open the correct Google Calendar ("Junior" or "Senior").

Create a new event and set the start and end time.

In the Description box, type this command: show=slide&id=4 (This would show slide #4 from that sign's default slide deck).

How to Schedule a Text Announcement
Use this to show a simple text message (like "Fire Drill") on a black screen.

Open the correct Google Calendar.

Create a new event and set the start and end time.

Type your message in the Event Title (e.g., "Assembly Today").

In the Description box, type this command: show=event

The TV will display "Assembly Today" in large text.

How to Schedule a "Welcome" Slide (from a different presentation)
Use this to show a "Welcome, Guest!" slide from a separate Google Slides deck.

First, get the Presentation ID of your "Welcome" slide deck. (It's the long string in the edit URL).

Open the correct Google Calendar and create an event.

In the Description box, type this command: show=externalSlide&presId=...&slideId=...

Example: show=externalSlide&presId=1aBcDeFgHi...&slideId=2 (This would show slide #2 from the "Welcome" deck).

Admin Guide (The "Takeover" Info)
Here is what you need to take full control.

1. Hardware: The Chromebits
What: The small computers plugged into the TVs.

How: They are managed in our Google Admin Console (under Devices > Chrome > Kiosk).

The URLs: We use the same code for both TVs. The ?sign= part tells the code which content to load.

Junior TV URL: https://iesv-swe.github.io/IESV_TV/?sign=junior

Senior TV URL: https://iesv-swe.github.io/IESV_TV/?sign=senior

2. The Code: index.html
This file holds all the logic. You can edit it in the GitHub repo.

The Configuration: At the top of the <script> section is the SIGNAGE_CONFIGS object. This is where you link the "Junior" and "Senior" signs to their specific Google Calendar and Google Slide IDs.

3. The "Key": Google Cloud Project 🔑
Why does this exist? To let our code (GitHub) talk to Google Calendar (Google's data), we need an "API Key."

Where is it? It's stored in a Google Cloud project. You will need to find which Google account owns this project.


How to Schedule Content
Choose the Calendar: Open either your "Junior TV Schedule" or "Senior TV Schedule" calendar.

Create an Event: Set the start and end times for when you want the special content to appear.

Use the Description Box for Commands:

Show a Specific Slide (from the main deck):

Description: show=slide&id=X (Replace X with the slide number, e.g., show=slide&id=5)

Show a Text Announcement:

Event Title: Your message (e.g., "Meeting in Library")

Description: show=event

Show a Specific Slide (from a different presentation):

Description: show=externalSlide&presId=[Presentation ID]&slideId=Y (Replace [Presentation ID] with the ID of the other slide deck and Y with the slide number, e.g., show=externalSlide&presId=1aBcDeFg...&slideId=1)

Save the Event.

The Key itself is pasted into the index.html file (near the top of the <script> tag): const API_KEY = '...'

SECURITY: This key is publicly visible in our GitHub code. This is okay because it is restricted. In the Google Cloud Console, the key is locked down to only accept requests from our website (httpsiesv-swe.github.io/*). It is useless to anyone else.

If you get an email from GitHub about a "secret exposed," this is why. You can safely go to the "Security" tab in GitHub and "Dismiss" the alert, marking it as "Risk is accepted."
