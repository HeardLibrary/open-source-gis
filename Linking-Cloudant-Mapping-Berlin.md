## Cloudant and Mapping Berlin

The first step to customizing the Mapping Berlin for your own projects is swapping out the current Cloudant database for your own. Just follow these easy steps:

### Create a Database in Cloudant (or use and existing database)

#### Make sure Databases is selected and then click on *Create Database*

![Imgur](http://i.imgur.com/ic0cNrO.png)

#### Name that database!

![Imgur](http://i.imgur.com/576K3fX.png)

### Populate the Database with a Sample Point

#### Open your database and click on the + next to *All Documents* and then select *New Doc*.

![Imgur](http://i.imgur.com/1XwCjgt.png)

#### In the text editor that opens insert a comma after the id number and insert the following code (note that the { } have not been included as they have already been provided by the text editor), and then save the changes.

``
  "type": "Feature",
  "properties": {
    "title": "World Clock Tower (Weltzeituhr)",
    "series": "Spring 2016",
    "tour": "1970",
    "marker-size": "medium",
    "marker-color": "#990000",
    "marker-symbol": "circle-stroked",
    "images": [
      {
        "format": "Image",
        "url": "https://upload.wikimedia.org/wikipedia/commons/1/18/World_Time_Clock_%2816810626209%29.jpg",
        "description": "A simplified representation of the solar system with planets (balls) and orbits shown with steel circles rotates once per minute, with the 24 times zones and respective major cities encircling the base. (\"The World Time Clock on Berlin's Alexanderplatz\" by Marcus Holland-Moritz)"
      },
      {
        "format": "Image",
        "url": "https://upload.wikimedia.org/wikipedia/commons/3/3e/Weltzeituhr%2C_Berlin_%2815910006062%29.jpg",
        "description": "A close up of the time zone plates (\"Weltzeituhr, Berlin\" by Tony Webster)"
      },
      {
        "format": "Image",
        "url": "https://upload.wikimedia.org/wikipedia/commons/0/01/Bundesarchiv_Bild_183-H1218-0025-001%2C_Berlin%2C_Alexanderplatz%2C_Weltzeituhr%2C_Winter.jpg",
        "description": "Designed by Erich John, the Weltzeituhr was presented in September of 1969 to the public in advance of the 20th anniversary of the GDR. It’s completion was part of an extensive redesign of Alexanderplatz in the sense of socialist modernism and city planning. (\"Berlin-Dezember 1969\" by Klaus Franke)"
      }
    ]
  },
  "geometry": {
    "type": "Point",
    "coordinates": [
      13.413333,
      52.521667
    ]
  }
``

![Imgur](http://i.imgur.com/ARR4AC8.png)

### Create a New View

#### Click on the + next to *Design Documents* and select *New View*

![Imgur](http://i.imgur.com/8dVONv5.png)

#### Follow the illustration below.  Your design document should be named *tour*, the index name is *1970* and the map function should say the following:

``
function (doc) {
  if (doc.properties.tour == "1970") {emit(doc._id, doc);}
}
``

![Imgur](http://i.imgur.com/lcPsEVk.png)

### Create a Search Index

#### Click on the + next to your newly created view called *tour* and select *New Search Index*

![Imgur](http://i.imgur.com/x3OGNhC.png)

#### Name your index *ids*, and paste in the following code for the search index function:

``
function(doc){
  index("default", doc.properties.title);
  if (doc._rev){
    index("rev", doc._rev, {"store": "yes"});
  }
  if(doc.properties.title){
    index("title", doc.properties.title, {"store": "yes"});
  }
}
``

![Imgur](http://i.imgur.com/b4r7Lti.png)

### Linking your Cloudant Database to Mapping Berlin

#### Go to your forked copy of the Mapping Berlin Github repository and switch from the Master branch to the gh-pages branches.  All your changes will be made on the gh-pages branch!
*If you forked this repository over 2 weeks ago you will need to update your fork as there have been significant changes. If updating becomes too complicated, simply delete your existing fork and refork the repository from HeardLibrary/mapping-berlin.*

![Imgur](http://i.imgur.com/n66nzn6.png)

#### Open the Scripts folder on your gh-pages branch

![Imgur](http://i.imgur.com/rD9s5lG.png)

#### Click on the maps.js file

![Imgur](http://i.imgur.com/VgqYw3G.png)

#### To edit this file, click on the pencil icon to the right

![Imgur](http://i.imgur.com/DO8GfFs.png)

#### Replace the URLs linking the repository to the Heard Library's cloudant database your your own cloudant database URL.  Everywhere you see https://vulibrarygis.cloudant.com/map-berlin, replace that portion of the URL with your database URL.  For example, my database URL is https://ramonav.cloudant.com/open-gis.
#### You will make these changes at line:  85, 124, 140 and 159.

![Imgur](http://i.imgur.com/UYPMFYw.png)

#### If everything has been formatted correctly you should be able to view your test point on the GitHub Pages site for your repository.
#### View mine at [http://ramona2020.github.io/mapping-berlin/](http://ramona2020.github.io/mapping-berlin/)
