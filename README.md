# AWS API Creation with Flask & Zappa
## Purpose
This repo illustrates a simplified approach for deploying a flask_restful (Python Flask) app on AWS API Gateway and Lambda. This just deploys the API portion of the api (/spam-api).

## Pre-reqs and Config?
Not really, assume you have an AWS account and just do this:
* If on an AWS AMI (e.g. Cloud9), `unset PYTHON_INSTALL_LAYOUT`
* `cd spam-api`
* `virtualenv spam-api-env`
* `source spam-api-env/bin/activate`
* `pip install flask flask_restful zappa`
* Update zappa_settings.json's project_name

## Deploy
To deploy your API, simply run:
* `zappa deploy {env}`

## Assignment
Now for the task at hand, using the pre-existing code found in egg_resource.py (found within your spam-api folder: beginner-flask-zappa-Your-Name/spam-api/resources), make some changes to allow for different egg preparation methods: (Scrambled, Over-Easy, Hard-Boiled, etc.) 

## Minimum Requirements
* Create a working API
* Retrieve the endpoint for your API

## Additional Requirements (Extra Credit/Bonus Points)
* Earn some bonus points for adding attributes like toppings for an omelette or salt and pepper!
* Even more bonus points for using Booleans!

## Starting Steps
* Log onto your Cloud9 instance on AWS
* use `git clone (your repository address) `


Pay attention to the code found in your egg_resource.py file and start thinking of some changes you can make to allow for different egg combinations (adding different toppings, types of eggs, condiments, etc.).

``` python
from flask_restful import Resource, fields, marshal

class Egg:
    pass

# the things that are determined by an egg being sunny-side
resources = {
    'type' : fields.String(),
    'cook' : fields.String(),
    'sunny-side' : fields.Boolean(attribute='sunny_side')
}

class EggResource(Resource):
	
    def get(self):
        print('Ordering the egg.')
        e = Egg()
        e.type = 'Chicken'
        e.cook = 'hard'
        e.sunny_side = True
        return marshal(e,resources)
        
```
## Next Steps
For the meat and potatoes, or rather the eggs, of the assignment, your task is to make your own endpoints! Here's an example endpoint from our egg template to give you a taste of what's cookin'!

`{"type": "Chicken", "cook": "hard", "sunny-side": true, "cheese": false, "onion": false, "bacon": false, "veggie-bacon": false, "salt": true, "pepper": true}`

This endpoint tells us that for a plain hard egg, according to this API there would be no toppings, just a hard-cooked egg with some salt and pepper.

To make your own entirely new endpoint, you'll have to make your own new API.

## Making your own API
Much like before with our Egg API, you'll need to have a controller and resource file (earlier these were egg_resource.py & egg_controller.py). To start, you can make a new folder outside of spam-api in your beginner-flask-zappa folder, and name it after whatever you're making (in this example we're making a circus api, so it'll be called circus-api).

* Within your new API folder (_____-api), make two new folders, one called controllers and another called resources
* Now in each of these folders, make a file.
	* In the controllers folder, make a (your api name here)_controller.py file
	* In the resources folder, make a (your api name here)_resource.py file
* Lastly, back in the main API folder, make a (your api name here)-api.py file

When you've finished these steps, your file directory should look like this:

![directory tree](images/directorytree.png)

Now you'll need to get code into these empty python files!
* Acting as a template, copy over the pre-existing code from the corresponding egg_controller.py, egg_resource.py, & spam-api.py files to your new files
* Within the newly copied code, make chanages to reflect the type of API you're making
* In the instance of the Circus API, our circus_controller.py file looks like this:
``` python
	from resources.test_resource import *

def circus_add(api):

    api.add_resource(CircusResource,'/api/circus')

```
* In the instance of the Circus API, our circus_resource.py file looks like this:
``` python 
from flask_restful import Resource, fields, marshal

class Circus:
    pass

# the things that will make up our circus:
resources = {
    'type' : fields.String(),
    'entertainment-value' : fields.String(),
    'tent' : fields.Boolean(attribute='tent'),
    'music' : fields.Boolean(attribute='music'),
    'magician' : fields.Boolean(attribute='magician'),
    'tightrope' : fields.Boolean(attribute='tightrope'),
    'acrobats' : fields.Boolean(attribute='acrobats'),
    'tiger' : fields.Boolean(attribute='tiger'),
    'elephant' : fields.Boolean(attribute='elephant')
}

class CircusResource(Resource):
    
    def get(self):
        print('Forming the Circus.')
        c = Circus()
        c.type = 'Performing'
        c.entertainment_value = 'Entertaining'
        c.tent = True
        c.music = True
        c.magician = True
        c.tightrope = False
        c.acrobats = True
        c.tiger = True
        c.elephant = True
        return marshal(c,resources)
```
* And lastly, in the instance of our Circus API, the circus-api.py file looks like this:
``` python
from flask import Flask
from flask_restful import Api

# import all of your controllers here
from controllers.test_controller import *

app = Flask(__name__)
api = Api(app)

# Helpful for debugging your Apache config
print('adding circus')
circus_add(api)

```
## Final Steps
Now that you've made your pertinent changes to your code for your own apis, in the terminal window of your cloud 9 instance, get back to your beginner-flask-zappa-(name) directory, `cd ..` and then change directories into your new api directory `cd (your api name here)-api `

Within your new api directory:
* Run `zappa init` 
* Choose a name for your Zappa environment: (your api name here)_api_(your name)_dev
* Go through the remaining steps to finish your next Zappa Environment!

When all is said and done, your should be able to run `zappa deploy (your api name here)_api_(your name)_dev ` and receive a URL for your endpoint 

Our Circus API's example endpoint looks like this:
`{"type": "Performing", "entertainment-value": "Entertaining", "tent": true, "music": true, "magician": true, "tightrope": true, "acrobats": true, "tiger": true, "elephant": true}`

Sounds like one heck of a circus! From this, we can tell that an entertaining performing circus would have a tent, music, a magician, a tightrope, acrobats, a tiger, and an elephant!

## Rubric

| Criteria | Superior (5) | Excellent (4) | OK (3) | Not OK (2) | Unsatisfactory (1) | Grade/Comments |
| --- | --- | --- | --- | --- | --- | --- |
| Readability (50%) | The code is organized (modular) well documented, easy to read and follow. | The code is easy to read and well documented. | The code can be followed. | The code is not easily followed. | The code is a mess. |  |
| Specifications (40%) | The program works and meets all the requirements. | The program works and meets most of the requirements. | The program produces correct results but does not display/plot them correctly. | The program does not meet most of the requirements. | Program does not work at all. |  |
| Efficiency (10%) | The code is highly efficient without affecting readability. | The code is reasonably efficient without affecting readability. | The code runs within a few seconds. | The code runs within a few minutes. | The code takes over an hour to run (or doesn't run at all). | |
