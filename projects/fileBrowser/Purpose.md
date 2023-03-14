thiThe purpose of the `fileBrowser` project is to be able to locally host a backend AND frontend. The frontend serves as a file and media browser, able to browse any files on the local server.
> The MOST important point is that there is no need to move or host the files anywhere but the server.
---
# Stack
| Tech    | Purpose                                                        |     |
| ------- | -------------------------------------------------------------- | --- |
| React   | Dynamic renders for frontend UI                                |     |
| NodeJS  | Handling requests from frontend to complete server tasks       |     |
| Express | Middleware to intercept requests to map endpoints to functions |     |

> In the future, it is possible to containerize the function into Docker containers and host the images in a single container to reduce the need to individually run the front and backend.
---
# Features, Scope
## Basics
1. ~~Locally host front AND back-end, with the ability for communication between~~
2. ~~Allow for "setting" a directory to examine its files ^[should be any directory on the "server" (since locally hosted, on the machine)]~~
3. ~~Randomly generated directory manifest for testing purposes~~
4. Ability to paginate or virtualize massive list to offload rendering when dealing with directories as large as 50k+ files and subfolders
5. Ability to *collapse* and *open* folder structure
6. Preview single files + Preview mutliple files
	1. PDF
	2. Video
		1. plyr
	3. ~~Image~~
	4. ~~Text (plain, markdown, js/json/html/code)~~
7. Global (root) directory statistics + counting
	1. MIME types
	2. Sizes (ranges -> small, med, big, huge, giant, etc.)
8. Local (selected/current) directory statistics + counting
9. Graphing (pie/radar) directory + file statistics
10. Global *type filters* to filter display
11. Global *sorting* to sort tree displays
	1. Sort by date
12. Displaying tree items with tree-lines
13. Displaying tree items with specific icons
	1. Directory (empty), Directory (non-empty), Directory open/close
	2. Icon by type (video/image)
14. Display per-file stats (created, modified, size, etc.)
	1. ~~Tooltip (hover)~~
	2. Stat View (previewed/selected)
15. ~~Open file externally~~
	1. via node's exec to open file in native (default) app.
16. Theater Mode
17. File Slideshow (based on type filters)
	1. shuffle + random
18. Individual file display endpoints
	1. ie. localhost:3000/view/\<filepath>
		1. `react-router` routed views

## Advanced 
1. Link "directory" and "file" views so that manipulating directories/files does the same between both
2. "Slideshow" files
	1. shuffle/random
3. Duplicate
4. Ability to select single/multi-items in list views to allow for manipulation
5. Random file list
	1. Choose only from selected directory
		1. Option to include subfolders (default ON)
	2.  Choose only from types in filter
	3. Ability to pin/unpin files to keep them in randomization
	4. Display ez-Preview for simple types (images)
6. UI to allow for walking directories via possible directories
	1. ex. "C:/" -> C:/ "users/" -> C:/users/"darko"
7. Provide prediction for directory being typed (best fit)
8. Lazy load directory contents
	1. only load when directory is "opened"
	2. "Chunk" list into "pages"
9. Ability to manipulate files directly from web UI
	1. Batch rename (given some 'formula' or 'series')
	2. Batch tag
10. More in-depth per-file metadata information (tags)
	1. filter/sort by tags


---

# Problems & Solutions

### Host Machine software
-> running the nodeJS server on Windows vs. Linux are entirely different. On Windows, we are able to access any directory given a mount point, but the filesystem in Linux is drastically different and does not seem to allow traversing absolute paths like in Windows. 
> For example, in Windows, I can ask the Web UI for the file manifest/tree of "C:/windows/system32" and it will work, but on Linux, asking for "/home/Downloads" does not work, even though "/" is root and thus, an absolute path.

> [! Statically serving dynamically ]
> Dynamically serving files requires a lot of overhead with sending individual files when requested, but this can be bypassed when using Express JS, as we can dynamic serve using the `express.static` as middleware.