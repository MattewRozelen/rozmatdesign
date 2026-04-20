






01 — Getting Started
Before you touch anything, read this section. It explains what the file is and how to open it safely so you don't break anything.

What is the file?
Your portfolio is a single file called matroz-portfolio.html. It is a plain text file — like a Word document but for websites. You open it in a browser to see the result, and open it in a text editor to make changes.

How to open it in a browser
Double-click the file. It should open automatically in Chrome, Firefox, Edge, or Safari.
If it doesn't open, right-click the file → Open With → choose your browser.
You should see your portfolio website — no internet required.

How to open it for editing
You need a free text editor. Visual Studio Code is the best free option.



How to edit the file
Open VS Code (the program you just installed).
Go to File → Open File and select matroz-portfolio.html.
You will see the code. Don't worry — you will only be changing small, specific pieces.
After every change: File → Save (or Ctrl + S on Windows / Cmd + S on Mac).
Switch to your browser and press F5 (Refresh) to see the result.



Finding things with Ctrl+F
Inside VS Code, use Ctrl + F (Windows) or Cmd + F (Mac) to search for text inside the code. This is the most important skill you will use. Every instruction in this guide tells you exactly what text to search for.

02 — Changing Images
Images in the portfolio are loaded from web addresses (URLs). To swap an image, you replace the old web address with a new one. No image uploads required.

Where are the images?
Images appear in two places: the Hero Slider (the big slideshow on the right side of the page) and the Selected Works grid (the project thumbnails). Both work exactly the same way.

How to get a new image URL
Option A — Use Behance, Notion, Google Drive, Dropbox, etc. Upload your image, then get a shareable/public link to the image file.
Option B — Use a free image hosting site like imgbb.com or postimages.org. Upload your image, copy the Direct Link that ends in .jpg, .png, or .webp.
Option C — From your Framer project. Open your Framer site, right-click an image → Inspect → copy the src URL from the <img> tag in the browser DevTools.



Changing a Hero Slider image
The Hero Slider has 4 slides. Each slide has one image tag that looks like this:



Step-by-step:


Changing a Works Grid image
The Works Grid cards work exactly the same. Search for the project name in the alt="..." attribute, then replace the src URL.



Project names to search for:  I&R Shop · RGO · Music · Business Cards · Logos · Typography

Changing the slide title and subtitle
Each slide also has a title and a description shown over the image. Find the slide by searching for its current title and update the text between the tags:



03 — Editing Links & Email
Links in the code look like href="...". You just replace the address between the quotes.

Changing the Contact email address
Search for: mailto: — you will find this line:



Replace matviy@design.com with your real email address. Keep the mailto: prefix — it makes clicking the button open the email app automatically.

Changing the RGO Partner link
The RGO project card links to an external website. Search for: rgo-taxi.framer.website and replace the full URL with the correct project link.

Changing the Framer Site button link
Search for: Framer Site — you will find this button:



Replace the URL and the button label text as needed.

Footer links
The footer has three links: Refund Policy, Terms, and Contact. Search for: articles/refund and you will see all three close together:



Replace each URL with the correct address. If you don't have these pages, you can replace them with # as a placeholder (this keeps the link but makes it go nowhere).

Copyright / footer text
Search for: Matviy Rozlutskyy — find and edit this line:



04 — Social Media Icons
There are three social icon groups: in the Header, in the Hero section, and in the Mobile Nav menu. All are simple links — just update the href value.

Changing social media profile URLs
Search for: title="Instagram" — this finds the first icon. You will see three icons close together:



Example after editing:  href="https://www.instagram.com/yourhandle"

Replacing an icon with a different social network
Each icon is an SVG shape drawn inside the <svg> tag. The easiest way to swap it is to use a free icon library.



How to replace one icon:
Open simpleicons.org, find your icon, click Copy SVG.
In your code, search for title="Instagram" (or whichever icon you're replacing).
Find the <svg opening tag — it will be on the next line after the <a tag.
Select everything from <svg to </svg> and paste the new icon code in its place.
Add style="fill:currentColor" to the new <svg tag so it picks up the hover color automatically.

Changing the title tooltip text
The title="..." attribute is what shows when someone hovers over the icon. Change title="Instagram" to title="TikTok" (or whatever the new network is) for correct accessibility.

05 — Selected Works Grid
The Works grid uses a newspaper-style layout where the first card is bigger than the rest. This section explains how to edit existing cards, add new ones, and change the grid arrangement.

Structure of one Work Card
Each project card follows this exact pattern:



Editing a card's content


Adding a new project card
Search for: <!-- end of works grid --> or look for the closing </div> after the last work card. Paste the block below just before that closing tag:



Changing the grid layout (which card is big)
The grid layout is controlled by CSS rules. The first card is always the large one. To change which card is big, simply reorder the cards in the code — move the card you want to be big to be first inside the <div class="works-grid"> container.



06 — Adding Filter Buttons
The Works section has filter buttons (All, Web, Branding, Print). You can rename them, add new ones, or remove existing ones.

How filters work
Each filter button has a data-filter attribute. Each project card has a data-category attribute. When you click a filter, only cards with a matching category are shown. The values must match exactly (same spelling, same lowercase).



Adding a new filter button
Search for: data-filter="print" — you will see the existing filter buttons together. Add a new button right after the last one:



Then set data-category="motion" on any cards you want this filter to show.

Renaming a filter button
Search for the button text (e.g. >Branding<) and change the text between the > and <. Do not change the data-filter value unless you also update all matching card data-category values.

Removing a filter button
Simply delete the entire <button ... </button> line for that filter. Cards with that category will still show when All is selected.

Full filter category list (default)


07 — Language Switching (EN / PL / UA)
Currently the language button cycles between EN and PL but doesn't actually translate the text. This section shows you how to make it fully work with real translations for English, Polish, and Ukrainian.



Step 1 — Add language labels to each text element
Find a text element you want to translate. Add a data-en, data-pl, and data-ua attribute to it with the translated text.

Before (original):


After (with translations added):


Repeat this for every piece of text you want translated: hero title lines, bio, button labels, section headings, contact text, etc.

Step 2 — Replace the language toggle script
Search for: const langs = ['EN','PL'] — find and replace the entire language script block (from // LANGUAGE TOGGLE to the end of that block) with the following:



Step 3 — Test it
Save the file (Ctrl+S) and refresh in the browser (F5).
Click the EN button in the header — it should now cycle: EN → PL → UA → EN.
All elements with data-pl attributes should update to Polish when PL is active.



08 — Hero Slider: Add, Remove & Reorder Slides
The Hero Slider currently shows 4 projects. You can add more, remove some, or reorder them. The slider auto-advances every 4.5 seconds and creates navigation dots automatically.

Finding the slider in the code
Search for: id="sliderTrack" — you will find the container that holds all slides:



Adding a new slide
Copy the block below and paste it inside the <div id="sliderTrack">, after the last </div> of the last existing slide:



The navigation dots and the slide counter update automatically — no extra code needed.

Removing a slide
Find the slide you want to remove by searching for its title text (e.g. MUSIC STREAMING). Select everything from <div class="slide"> to the matching </div> and delete it.

Reordering slides
Cut a full <div class="slide">...</div> block and paste it in a different position inside sliderTrack. The first slide in the code will be shown first.

Changing the auto-advance speed
Search for: 4500 — you will find this line:



Change 4500 to any number of milliseconds. 1000 = 1 second. 6000 = 6 seconds. 0 disables auto-advance (just set a very large number instead, like 999999).

Quick Reference Cheatsheet
Use Ctrl+F (Cmd+F on Mac) in VS Code to find these search terms instantly.



ONE DESIGN by MatRoz  ·  Portfolio Documentation  ·  Version 1.0  ·  2025
