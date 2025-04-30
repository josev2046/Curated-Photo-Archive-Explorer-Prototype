# Curated photo archive explorer 
[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.15308602.svg)](https://doi.org/10.5281/zenodo.15308602)

A web-based prototype for exploring a curated digital archive of photographic assets. The code fetches a curated list of photos and their metadata from a Digital Asset Manager (DAM), displays them in a user-friendly grid with names, and allows users to view individual photos using an embedded media player with basic navigation. The primary API methods used in this example are Kaltura's `media.count`, and `media.list` for data retrieval, and the embed URL structure for displaying the photos via the media player.

![image](https://github.com/user-attachments/assets/52e62e70-5207-413b-8d03-b4be12896309)

This web app displays a photo gallery fetched from a Digital Asset Manager.

## Authentication: 
When the page loads, a form prompts the user to enter a secret code. Upon submission (`startApp` function), the code attempts to start a user session with the DAM using the `session.start` method. If successful, a `sessionKey` is obtained.

## Fetching photo gallery data: 
The `getCategoryEntries` function then retrieves the photo metadata from the DAM. It uses the following API methods:

* `media.count`: To get the total number of photos in a specific category ("Curated Photo Archives").

* `media.list`: To fetch batches of photo details (including thumbnail URLs and names) from the specified category, using pagination to handle potentially large numbers of photos.

## Displaying the photo grid: 
The fetched photo data is stored in the `allPhotos` array. The `displayPhotosInGrid` function dynamically generates HTML for each photo, creating a grid of thumbnails. Each thumbnail is clickable and displays the photo's name below it.

## Viewing a single photo: 
When a user clicks a thumbnail (`showPlayer` function):

* The photo grid is hidden.
* The `embedPlayer` function creates and displays an embedded Kaltura video player (using an `<iframe>`). The player's source URL is constructed using your Kaltura `partnerId`, a player configuration ID (`uiConfId`), and the specific `id` of the selected photo. This leverages Kaltura's playback capabilities.
* Navigation buttons ("Previous", "Next") are enabled to browse through the photos in the gallery.

## Navigation: 
The `navigateBackward` and `navigateForward` functions update the currently viewed photo index and reload the media player with the previous or next photo's ID, allowing sequential viewing. The `updateNavigationButtons` function manages the enabled/disabled state of these buttons.

## Returning to the gallery: 
The "Back to Gallery" button (`showGrid` function) hides the single photo player and redisplays the thumbnail grid.
