key:
	!! important / required
	?? optional / idea
	// bug / issue / fixme
	
___
# Goals

## Certifications & Courses
-   do Linkedin tests
-   practice algos with hackerrank, leetcode, etc.

## Backend Development
-   what’s the difference between NGINX, Apache, NodeJS?
-   how servers, IPs, ports, work in general with serving files
-   different ways to serve files
-   in general, explore a LOT more about docker
    -   using docker desktop, using CLI
-   use Mac Mini server to have a separate computer to tinker on
-   understand message “brokers”, message queueing - RabbitMQ
-   look into PHP
-   look into Ruby on Rails
-   look into Python backend
-   look into Java backend

## Frontend Development
-   Explore Vite, Webpack
-   figure out how to create React applications without toolchains like create-react-app
-   explore core javascript libraries like jQuery

## DevOps
-   Look into GitHub Actions, Jenkins
-   Look into Terraform, Ansible
___
# Mock Websites
- mock websites and gallerys to practice and create "templates" and projects

# Personal Portfolio

- **Global**
	- create global "theme" context
		a. extract RGB/HEX values for tailwind color values
		b. figure out if there's some way to configure tailwind "themes" that are easily usable
	- use Responsively to check and fix responsiveness of all pages

-   **About**
	- a. figure out how to constrain / attach boxes to each *other*
	- b. perhaps implement this with a sketch 
-   **Education**
	- FIXME: information icon for grade breakdown breaks line weirldy
	- add more color
-   **Experience**
	- add more color 
-   **Projects**
	- figure out how to create various "components" for project showcases
		- image/carousels, text + image
	- components should be focusable into modal 
-   **Links**
	- create rotary 'ferris'-wheel (marquee) element for links
-   **Files**
	- create interesting typographic-based file picker
	- include the "symbol" design that was used for initial resume
-   **Contact**
	- send button should connect to a service to send a message
		- perhaps SES ???
-   **Tools**
    -   create draggable elements that align to grid
    -   perhaps `useSound` for simple 'system' sound (clicks, window open, etc)
	    - create "icon" and "window" elements
	
-   **Blog**
    -   DETERMINE:
        -   a. use GH API to fetch zip archive
        -   b. use GP API to fetch / populate single folders and files
        -   c. create custom backend to serve the files
            -   meaning that the server needs to listen via webhooks for updates and fetch new files
    -   B) individual (infinite) fetching
        -   get tree structure to display properly, manipulate/group resulting data based on incoming data (parentId, etc.) to create hierarchical structure
        -   OR, display one directory at a time (current traversed directory)
-   **Sketch**
    -   start developing simple, efficient sketches
        -   with or without shaders
-   **Components**
    -   Modal
        -   create a modal
-   **Music Player**
    -   create custom Web Audio API player with visualizer support, timing
    -   ? use youtube playlists

### Mini Ideas

-   develop small “games” or “applets” for the utilities section
    -   snake, game of life, etc.
    -   neofetch mock
    -   image-2-ASCII/SYMBOL
-   create audio-reactive backgrounds to music
-   Important Elements:
    -   really fast to load, smooth
        -   use pre-loading, lazy-loading (look up various other techniques)
    -   clean interface
-   New Stack:
    
    -   TypeScript
    -   react-router
    -   Reducers
    -   use better rendering and effect patterns

# Media Browser & File Server App

-   Description
-   [ ] implement automatic network-wide access to file server
-   [ ] re-factor the entire frontend to use good effect usage, and proper React patterns
-   Stack
    -   React
    -   react-window / react-virtualized-tree
    -   redux toolkit + query

# “Let It Out”

-   Description
    -   an ominous interface, shifting/dithering/banded colors, warping images, etc...
        -   allows you to type
            -   simple font controls
            -   typewriter sounds
        -   typographic design
        -   offers options to "resolve" your thought
            -   "kill it", through various methods (throw into void, fire, axe, etc)
        -   offers positive feedback "i know", "i understand"
        -   perhaps can add a survey element, to get anonymized input on stress and suicide
            -   display research cited stats, along with collected stats
-   Determine stack to build application in
-   Ideally, something that allows for a very cinematic experience
    -   going to need a very good rendering / graphics library (threejs?)

# Steam Library Utilities App

-   Description
    -   Library statistics and analytics
        -   maybe provides GPT-based recommendations of games to play, buy based on most played
    -   Game news timeline
    -   Roulette
    -   Library sort, filter, organizer
-   full-stack application
    -   very responsive front-end
    

# Job Application Organizer App

-   Description
    -   "glorified" excel table to allow adding items in row-field format
    -   meant as a way to track applications
        -   creates referential data between applications and cover letters
        -   upload and modify application documents
            -   resume
            -   cover letter
        -   ability to upload a template, define template patterns and auto-create new cover letter from template from application
            -   fills in (any maybe generates) content from tags into cover letter
        -   ability to convert .docx to plaintext + copy to clipboard (for those
        -   perhaps can use chatGPT API to generate career-related content
            -   buzzwords, simple templates, etc.
        -   allows filtering and sorting of data by criteria
        -   ADVANCED: can attempt to "scan" document as ATS scanners would to determine "score" of resume.
        -   "Marketing video"
            -   Montage of stress-inducing clips (news of war, poverty, inflation, etc...)
            -   lay off happens to person
            -   frantic job search (rapid eye movements - intense reflection of the eyes)
                -   rejection after rejection, clicks and clicks and error noises
                -   anxious, heavy, panicked breathing gets worse and worse
            -   arrives at marketing website, breathing stops.
-   full-stack application