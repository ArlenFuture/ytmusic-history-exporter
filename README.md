# YouTube Music History Exporter

**ytmusic-history-exporter** is a simple tool for extracting song titles and URLs from the YouTube Music history page and saving the results as a JSON file.

## Features

- Extract song titles and URLs from YouTube Music history
- Generate a downloadable JSON file

## Usage Instructions

1. Open the [YouTube Music History page](https://music.youtube.com/history) (make sure you are logged in and your history is loaded).

2. Open your browser's Developer Tools (press `F12` or `Ctrl+Shift+I` / `Cmd+Option+I`).

3. Switch to the "Console" panel.

4. Copy and paste the following code into the console and press Enter:

   ```javascript
   // Select all matching <a> elements
   const linkElements = document.querySelectorAll('a.yt-simple-endpoint.style-scope.yt-formatted-string');

   // Extract titles and URLs
   const songs = Array.from(linkElements).map(linkElement => {
       return {
           title: linkElement.textContent.trim(),  // Extract song title
           url: linkElement.href                    // Extract URL
       };
   });

   // Convert results to JSON string
   const jsonOutput = JSON.stringify(songs, null, 2);  // `null` and `2` are used for formatting output for readability

   // Create Blob object
   const blob = new Blob([jsonOutput], { type: 'application/json' });

   // Create download link
   const url = URL.createObjectURL(blob);
   const a = document.createElement('a');
   a.href = url;
   a.download = 'songs.json';  // File name
   a.textContent = 'Download JSON';

   // Automatically click the download link
   a.click();

   // Clean up URL object
   URL.revokeObjectURL(url);
   ```
## Notes
- Ensure that your history page is fully loaded and that your history is visible on the page.
- This tool is for personal use only and is not guaranteed to be compatible with future versions of YouTube Music.
## Contributing
Feel free to submit issues and feature requests. If you have any improvements or suggestions, please submit a pull request.

## License
This project is licensed under the MIT License. See the LICENSE file for details.
