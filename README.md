## Deployment 

### b) PRODUCTION

#### Launch a workspace container at Gitpod

#### 1. Create file --> requirements.txt  

```
click==7.1.2
dnspython==1.16.0
Flask==1.1.2
itsdangerous==1.1.0
pymongo==3.10.1
python-dotenv==0.13.0
Werkzeug==1.0.1
```

The requirements we are installing are:
```
`pip3 install flask`
`pip3 install pymongo` -- to use Mongo DB
`pip3 install dnspython` -- is to allow us to connect to Mongo with just the URL
`pip3 install python-dotenv` -- allows the use of `.env` files for environment variables
```
#### 2. How to use requirements.txt
```
pip3 install -r requirements.txt
```
#### 3. Create `.env` file to store the passwords and security-sensitive information.
#### 4. Create `.gitignore` file to git ignore the environment variables file, which are never committed to the repository.
```
.env
```
#### 5. Create file `app.py` and insert flask template

#### 6. Connect mongodb 
```
MONGO_URI = os.environ.get("MONGO_URI")
client = pymongo.MongoClient(MONGO_URI)
DB_NAME = "pro3"
```

#### 7. Open Browser
To run a backend Python file, type `python3 app.py`, if Python file is named `app.py` of course.
A blue button should appear to click: *Make Public*,
Another blue button should appear to click: *Open Browser*.

#### 8. "C"RUD = Create function & template
To insert a document into the collection use `<database>.<collection>.insert_one()`

#### 9. C"R"UD = Reading function & template
Using <a href="https://getbootstrap.com/docs/4.4/content/tables/">Bootstrap Table</a> to show the schedule list, added Create button at the home page to bring external user to the create form page. Also, use of Flask `redirect` to bring external user back to the home page. 

#### 10. CR"U"D = Update function & template
* Import `from bson.objectid import ObjectId` at `app.py`
* Getting a single document use `<database>.<collection>.find_one()`
* Use `"$set":` for pymongo 


#### 11. CRU"D" = Delete function & template
To delete a document use `<database>.<collection>.remove()`

#### 12. import datetime, Python strptime()
```datetime.datetime.strptime(date, "%Y-%m-%d")```

#### 13. Flash Messages 
* Import Flash `from flask import flash` at `app.py` file
* Generate Session Key from https://randomkeygen.com/
* Save the Session Key in the `.env` file 
* Save & restart server `python3 app.py`
* Read in the SESSION_KEY variable from the operating system environment `SESSION_KEY = os.environ.get('SESSION_KEY')`
* Set the session Key `app.secret_key = SESSION_KEY`
* In the `layout.template.html` add in the code to display the flash messages:
    ```
    {% with messages = get_flashed_messages() %}
        {% if messages %}
            {% for m in messages %}
            <div class="alert alert-success">
                {{m}}
            </div>
            {% endfor %}
        {%endif%}
    {%endwith%}
    ```

#### 14. Search function
* NOTE : method is GET
* HTML : Use <a href="https://getbootstrap.com/docs/4.0/components/forms/#inline-forms">Bootstrap 4 Inline Forms</a>
* app.py : added coding 
* Use of `"$regex"` Regular Expression forms a search pattern.
* Use of `"$options": "i"` to carry out search without considering upper or lower case.

#### 15. "C"RUD = Upload profile image for advertisement ('ads')
* Sign up <a href="https://cloudinary.com/users/login">Cloudinary</a>
* Save the could name & the upload preset in `.env` file. 
* Retrieve the cloud name and the upload preset from the .env file in the Flask app
    ```
    CLOUD_NAME = os.environ.get("CLOUD_NAME")
    UPLOAD_PRESET = os.environ.get("UPLOAD_PRESET")
    ```
* Run server `python3 app.py` again
* Create `@app.route("/profile/upload")` for view route
* Create `profile_upload.template.html` 
* Pass the cloud name and the upload preset to the Upload Widget script
    ```
    <script src="https://widget.cloudinary.com/v2.0/global/all.js" type="text/javascript"></script> 
    
    <script type="text/javascript">
        var myWidget = cloudinary.createUploadWidget({
            cloudName: '{{cloud_name}}', 
            uploadPreset: '{{upload_preset}}'}, (error, result) => { 
                if (!error && result && result.event === "success") { 
                console.log('Done! Here is the image info: ', result.info); 
                }
            }
        )

        document.getElementById("upload_widget").addEventListener("click", function(){
                myWidget.open();
        }, false);
    </script>
    ```
* Setup a `<form method="POST">` to capture the uploaded image url
    ```
    <div>
        <a id="upload_widget" class="cloudinary-button mt-3">Upload Image</a>
        <input type="hidden" id="uploaded_image_url" name="uploaded_image_url"/>
    </div>
    ```
* Change the JavaScript to put in the image url into the hidden form field
    ```
    let myWidget = cloudinary.createUploadWidget({
        cloudName: '{{cloud_name}}', 
        uploadPreset: '{{upload_preset}}'}, (error, result) => { 
            if (!error && result && result.event === "success") { 
            console.log('Done! Here is the image info: ', result.info); 
            let fileURL = document.querySelector("#uploaded_image_url");
            fileURL.value = result.info.url;
            }
        }
    )
    ```
* Process the form and save its data to Mongo

#### 16. C"R"UD = Reading function for Uploaded profile ads image & description 
* <a href="https://getbootstrap.com/docs/4.1/components/card/"></a>Bootstrap 4 Cards</a>
* Using the grid, wrap cards in columns and rows.

#### 17. CR"U"D = Update function for profile ads 
* Import `from bson.objectid import ObjectId` at `app.py`
* Getting a single document use `<database>.<collection>.find_one()`
* Use `"$set":` for pymongo 

#### 18. CRU"D" = 

#### 19. Static CCS 
* To create & link the style.css file
    * At the folder, create a new folder `static`
    * At the `static` folder, create a new file `style.css`
    * Inside `<head>` of `layout.template.html`, added `<link rel="stylesheet" href="/static/style.css"/>`
    * run `python3 app.py` for testing
* Import <a href="https://fonts.google.com/specimen/Open+Sans?category=Sans+Serif&selection.family=Open+Sans:wght@600&sidebar.open=true">Google Font</a>
* Added <a href="https://getbootstrap.com/docs/4.0/components/navbar/">Bootstrap fixed top navigation bar</a>
* Added a landing image by using <a href="https://www.w3.org/TR/css-images-3/#linear-gradients">linear-gradients</a> to make the image darker
* Manage the "search function" layout, alignment and responsive variations by using <a href="https://getbootstrap.com/docs/4.1/utilities/flex/">.d-lg-flex</a>. 
* Used of <a href="https://getbootstrap.com/docs/4.4/components/jumbotron/">Jumbotron</a> to extend the entire viewport at home page 
* Fixed Ads Profile Card responsive by using <a href="https://getbootstrap.com/docs/4.0/utilities/spacing/">`mx-auto`</a> and <a href="https://getbootstrap.com/docs/4.3/components/card/">Bootscrap Card</a>

#### 20. API = 

### C) PUBLICATION
* Sign up for a <a href="https://www.heroku.com">Heroku</a> account
* At Gitpod terminal : 
    * log into Heroku using  `heroku login`
    * create a new app  `heroku create <app_name>` 
    * add new remote `git remote -v`
    * to can run Python web applications that implement the application interface `pip3 install gunicorn`
* At the folder, create a new file `Procfile`
* Save `web gunicorn <your python file name without .py>:app` inside the `Procfile`file
* At Gitpod terminal : 
    * create requirements file `pip3 freeze --local > requirements.txt`
    * `git add .`
    * commit everything `git commit -m "<Commit Message>"`
    * push to heroku using `git push heroku master`
* Go the <a href="https://www.heroku.com">Heroku</a> Site :
    * click on your project 
    * ciick on Setting
    * click on Reveal Config Vars
    * save all your environment variables (in .env file) into Reveal Config Vars 
    * at the top left, cilck on "Open App" 
* Done publication!!

