## Using Postman to populate your Cloudant Database

**What is Cloudant?**

IBM [Cloudant](https://cloudant.com) is a hosted version of CouchDB. CouchDB is a document-oriented database that stores data as JSON, uses Javascript for writing Map/Reduce functions, and communicates with applications via HTTP. Cloundant provides a fast and easy way to get started with CouchDB without installing anything on your computer or setting up a server. These characteristics make it easy to store GeoJSON features in the "cloud" and to send those features on demand to users.

**Why do I need Postman?**

When working with multiple collaborators, giving everyone direct access to your Cloundant database may not be the wisest choice.  Using [Postman](https://www.getpostman.com/), a free Chrome app, allows your collaborators to contribute to your database via HTTP without ever accessing Cloudant.

### Setting up Accounts and Installing Apps

#### Create a Cloudant account:  [https//cloudant.com](https//cloudant.com)

**Let's change some account settings now that you are logged in:**

**Click on Account in the left-hand column.**

![Cloudant Account]](http://i.imgur.com/y507yI9.png)

**Then click on CORS**

![Imgur](http://i.imgur.com/AykIREl.png?1)

**Make sure CORS is enabled and that the radio button for All domains(*) is selected.**

![Imgur](http://i.imgur.com/BhiBQg0.png)

#### Install Postman app for Chrome: [https://www.getpostman.com/docs/introduction](https://www.getpostman.com/docs/introduction)

**You can skip the account creation portion of the install.  An account is not necessary to use Postman.**

**Open Postman, if it doesn't open automatically after the install.**

### Create a Database in Cloudant

#### Make sure Databases is selected and then click on *Create Database*

![Imgur](http://i.imgur.com/ic0cNrO.png)

#### Name that database!

![Imgur](http://i.imgur.com/576K3fX.png)

#### Click on the lock icon next to your database (see above image) to set up the permissions.

#### Click *Generate API key* - this is what you need to get Cloudant and Postman to talk to each other.

![Imgur](http://i.imgur.com/0LgxPUQ.png)

#### Make sure the *Reader* and *Writer* boxes are checked for your new API, and save a copy of the API key and password for future uses (see areas highlighted in yellow).  Do not navigate away from this screen as we need to get this data into Postman.

![Imgur](http://i.imgur.com/chW17M4.png)

### Setting up Postman

#### Go to Postman and change *Get* to *Post*, and paste in the URL for the database you created in Cloudant in the address bar highlighted in yellow.

![Imgur](http://i.imgur.com/AmQTarl.png)

#### Click on the *Authorization* tab and change *No Auth* to *Basic Auth*

![Imgur](http://i.imgur.com/wbBu4dM.png)

#### Go back to Cloudant and paste the API key into the user name field and the password into the password field, and the click update request.

![Imgur](http://i.imgur.com/t0TchRH.png)

#### Click on the *Body* tab, and select the radio button for *raw* and *JSON9application/json)* from the drop down menu.

![Imgur](http://i.imgur.com/eGwHhSf.png)

#### Paste the following GeoJSON point into the text editor as seen in the image above, and then click send.

``
{
  "type": "Feature",
  "geometry": {
    "type": "Point",
    "coordinates": [125.6, 10.1]
  },
  "properties": {
    "name": "Dinagat Islands"
  }
}
``

#### In Postman click the *Save* button, to save this as a collection for future use.

![Imgur](http://i.imgur.com/U0jRKQ9.png)

#### Go back to Cloudant. Your database should now contain a new point.
