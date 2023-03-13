The purpose of the `fileBrowser` project is to be able to locally host a backend AND frontend. The frontend serves as a file and media browser, able to browse any files on the local server.
- The MOST important point is that there is no need to move or host the files anywhere but the server.

> In the future, it is possible to containerize the function into Docker containers and host the images in a single container to reduce the need to individually run the front and backend.


# Problems & Solutions

> [! Statically serving dynamically ]
> Dynamically serving files requires a lot of overhead with sending individual files when requested, but this can be bypassed when using Express JS.

Walking directories.