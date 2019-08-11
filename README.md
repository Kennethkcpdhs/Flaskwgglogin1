# Flaskwgglogin1
First attempt at using Google Login

An environment variable is a variable whose value is set outside the program, typically through functionality built into the operating system or microservice. An environment variable is made up of a name/value pair, and any number may be created and available for reference at a point in time.

# Page Layout
Homepage: /

Login: /login

Login Callback: /login/callback

Logout: /logout

## Debug Log

### Problem 1
#### Internal Server Error
![Internal Server Error 500](https://mediatemple.zendesk.com/hc/article_attachments/202382660/500ise.jpg)

Found out the reason: Made use of http in google authentication, instead of https

#### HTTP stands for Hypertext Transfer Protocol. 
At it’s most basic, it allows for the communication between different systems. It’s most commonly used to transfer data from a web server to a browser in order to allow users to view web pages. It’s the protocol that was used for basically all early websites.

#### HTTPS stands for Hypertext Transfer Protocol Secure. 
The problem with the regular HTTP protocol is that the information that flows from server to browser is not encrypted, which means it can be easily stolen. HTTPS protocols remedy this by using an SSL (secure sockets layer) certificate, which helps create a secure encrypted connection between the server and the browser, thereby protecting potentially sensitive information from being stolen as its transferred between the server and the browser.

### Problem 2
#### Did not make proper use of environment variables when utilising pythonanywhere website.
```python
# Configuration
# Set from your system environment variables, meant to be kept secret
GOOGLE_CLIENT_ID = os.environ.get("GOOGLE_CLIENT_ID", None)
GOOGLE_CLIENT_SECRET = os.environ.get("GOOGLE_CLIENT_SECRET", None)
GOOGLE_DISCOVERY_URL = (
    "https://accounts.google.com/.well-known/openid-configuration"
)

# Flask app setup
app = Flask(__name__)
app.secret_key = os.environ.get("SECRET_KEY") or os.urandom(24)

```
In the line of code, on a local host, you store the CLIENT_ID and CLIENT_SECRET in a local computer with the command:

##### Windows, you can use   set GOOGLE_CLIENT_ID=your_client_id in Command Prompt.
##### Linux & Mac OS X you can use   export GOOGLE_CLIENT_ID=your_client_id (similarly for GOOGLE_CLIENT_SECRET)

But, on python anywhere, you can't simply key in the environment variables into the bash console.

You need to copy the files to a created environment variable file
```python
cd ~/my-project-dir
echo "export SECRET_KEY=sekritvalue" >> .env
echo "export OTHER_SECRET=somethingelse" >> .env
# etc
```
Of course, its possible to simply dump the "secret codes directly and safe the trouble but __please dont do this for official important projects__!

#### References
https://realpython.com/flask-google-login
https://help.pythonanywhere.com/pages/environment-variables-for-web-apps
https://www.mattbutton.com/2019/01/05/google-authentication-with-python-and-flask/
