# Downloader for Yoto
Audio file downloader for Yoto Player

This project provides a simple and efficient tool for downloading audio files from Yoto cards and MYO playlists. The tool is designed to help users easily backup their purchased content in a future-proof medium. 

## Features

- Download audio files from Yoto.
- Download icon files from Yoto.
- User-friendly interface for hassle-free operation.
- When used with Simple Mass Download, batch download multiple files simultaneously and retain the original file names


## Prerequisites

- The Downloader for Yoto bookmarklet (see next section)
- [Simple Mass Download](https://chromewebstore.google.com/detail/simple-mass-downloader/abdkkegmcbiomijcbdaodaflgehfffed) (optional but very much recommended)
- NFC Tools app

### Installing the Downloader for Yoto bookmarklet
  
  1. In Google Chrome, right-click on the bookmarks bar and click **Add Page**
  2. Enter "Downloader for Yoto" for the **name**
  3. For **URL**, copy and paste the code block below:
     
```
javascript:(function()%7B%2F%2F%20First%2C%20find%20the%20script%20element%20by%20its%20ID%0Aconst%20scriptElement%20%3D%20document.getElementById('__NEXT_DATA__')%3B%0A%0A%2F%2F%20Check%20if%20the%20element%20exists%0Aif%20(scriptElement)%20%7B%0A%20%20%20%20%2F%2F%20Parse%20the%20JSON%20content%20of%20the%20script%20element%0A%20%20%20%20const%20jsonData%20%3D%20JSON.parse(scriptElement.textContent)%3B%0A%0A%20%20%20%20%2F%2F%20Navigate%20to%20the%20specific%20path%20where%20trackUrl%2C%20title%2C%20and%20icon16x16%20are%20located%0A%20%20%20%20const%20chapters%20%3D%20jsonData.props.pageProps.card.content.chapters%3B%0A%0A%20%20%20%20%2F%2F%20Create%20a%20container%20for%20the%20links%0A%20%20%20%20const%20container%20%3D%20document.createElement('div')%3B%0A%20%20%20%20container.style.margin%20%3D%20'20px'%3B%0A%20%20%20%20container.style.backgroundColor%20%3D%20'%23deefff'%3B%0A%20%20%20%20container.style.padding%20%3D%20'20px'%3B%0A%0A%20%20%20%20%2F%2F%20Add%20a%20title%20to%20the%20container%0A%20%20%20%20const%20containerTitle%20%3D%20document.createElement('h2')%3B%0A%20%20%20%20containerTitle.textContent%20%3D%20'Track%20and%20Image%20Links'%3B%0A%20%20%20%20container.appendChild(containerTitle)%3B%0A%0A%20%20%20%20%2F%2F%20Add%20an%20explanatory%20paragraph%20to%20the%20container%0A%20%20%20%20const%20containerP%20%3D%20document.createElement('p')%3B%0A%20%20%20%20containerP.textContent%20%3D%20'You%20can%20download%20the%20MP3%20files%20and%20view%20the%20images%20directly%20from%20the%20links%20below.%20Use%20Batch%20Link%20Downloader%20to%20download%20all%20at%20once'%3B%0A%20%20%20%20container.appendChild(containerP)%3B%0A%20%20%20%20%0A%20%20%20%20%2F%2F%20Loop%20through%20chapters%20and%20tracks%20to%20create%20links%0A%20%20%20%20chapters.forEach(chapter%20%3D%3E%20%7B%0A%20%20%20%20%20%20%20%20chapter.tracks.forEach(track%20%3D%3E%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%2F%2F%20Create%20a%20link%20element%20for%20each%20track%0A%20%20%20%20%20%20%20%20%20%20%20%20const%20trackLink%20%3D%20document.createElement('a')%3B%0A%20%20%20%20%20%20%20%20%20%20%20%20trackLink.href%20%3D%20track.trackUrl%3B%0A%20%20%20%20%20%20%20%20%20%20%20%20trackLink.textContent%20%3D%20%60Track%3A%20%24%7Btrack.title%7D%60%3B%0A%20%20%20%20%20%20%20%20%20%20%20%20trackLink.target%20%3D%20'_blank'%3B%20%2F%2F%20Open%20in%20new%20tab%0A%20%20%20%20%20%20%20%20%20%20%20%20trackLink.style.display%20%3D%20'block'%3B%20%2F%2F%20Display%20each%20link%20on%20a%20new%20line%0A%0A%20%20%20%20%20%20%20%20%20%20%20%20%2F%2F%20Append%20the%20track%20link%20to%20the%20container%0A%20%20%20%20%20%20%20%20%20%20%20%20container.appendChild(trackLink)%3B%0A%0A%20%20%20%20%20%20%20%20%20%20%20%20%2F%2F%20Create%20a%20link%20element%20for%20each%20image%0A%20%20%20%20%20%20%20%20%20%20%20%20if%20(chapter.display%20%26%26%20chapter.display.icon16x16)%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20const%20imageLink%20%3D%20document.createElement('a')%3B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20imageLink.href%20%3D%20chapter.display.icon16x16%3B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20imageLink.textContent%20%3D%20%60Image%3A%20%24%7Btrack.title%7D%60%3B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20imageLink.target%20%3D%20'_blank'%3B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20imageLink.style.display%20%3D%20'block'%3B%0A%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%2F%2F%20Append%20the%20image%20link%20to%20the%20container%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20container.appendChild(imageLink)%3B%0A%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%7D)%3B%0A%20%20%20%20%7D)%3B%0A%0A%20%20%20%20%2F%2F%20Insert%20the%20container%20at%20the%20top%20of%20the%20body%20of%20the%20page%0A%20%20%20%20document.body.insertBefore(container%2C%20document.body.firstChild)%3B%0A%7D%20else%20%7B%0A%20%20%20%20console.error('Script%20element%20not%20found')%3B%0A%7D%7D)()%3B
```
  4. Click **save**

## Usage

1. Scan a Yoto card with a third-party NFC reader app (like NFC Tools) to read the card's content. Look for Record 1. This should have a URL that looks like this: yoto.io/ABC123?xxxxxxx=yyyyyyyy
2. Open the URL in your web browser on your computer (not your phone).
3. Click the bookmarklet to activate the tool. This should populate links to download the files at the top of the page. 
4. Download the files you'd like using "save as.." or select multiple files for batch downloading using Simple Mass Download.

## Disclaimer 

This tool is not affiliated with Yoto. Yoto is a registered trademark of Yoto Limited.

This tool is provided as-is without any warranty of any kind, either express or implied, including but not limited to the implied warranties of merchantability, fitness for a particular purpose, or non-infringement. The developers are not affiliated with, endorsed by, or sponsored by Yoto or any associated entities. The use of this tool for downloading content should be done in accordance with the copyright laws and terms of service of the respective audio content providers. Users are responsible for ensuring that their use of the tool complies with all relevant laws and regulations.


