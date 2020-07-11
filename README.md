## Deployment 

### b) PRODUCTION

#### Launch a workspace container at Gitpod

##### 1. Create file --> requirements.txt  

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

* `pip3 install flask`
* `pip3 install pymongo` -- to use Mongo DB
* `pip3 install dnspython` -- is to allow us to connect to Mongo with just the URL
* `pip3 install python-dotenv` -- allows the use of `.env` files for environment variables

##### 2. How to use requirements.txt
```
pip3 install -r requirements.txt
```
##### 3. Create `.env` file to store the passwords and security-sensitive information.
##### 4. Create `.gitignore` file to git ignore the environment variables file, which are never committed to the repository.
```
.env
```
##### 5. Connect mongodb 
