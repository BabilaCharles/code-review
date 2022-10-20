## Code_review_enforced
- Background

GitHub  is a central tool to many developers’ workflows. Given that most developers work in teams and large organizations, usually halfway across the world from each other, it is imperative that only the intended team members have access to the code repository and that code is properly reviewed before it is merged into the required branch to prevent errors, failures, and bad designs.  If developers are allowed to push their code directly or merge their feature branches to the main branch without code review, there may be bugs that could break the code and lead to an unpleasant experience.


##  Why Should We Review Code?

Code reviews can be useful in:
Saving time and money: By finding bugs at an early stage we avoid disruptions to service.
Knowledge transfer: Code reviews offer developers an opportunity to share knowledge about the codebase and pull request authors gain confidence about their design approach.
Building team cohesion: encourages team members to talk to each other and brings them closer.
Finding alternative solutions to problems: In the process of discussing your code with your peers, you look at the solution from a different perspective.

##  How to set up code reviews in GitHub

Code Review Enforced is a web service that enforces code reviews in an organization. Code Review Enforced listens for organization events to know when a repository is created. Once the repository is created, this web service automates the protection of the main branch. It also notifies you with an @mention in an issue within the repository that outlines the protections that were added.

##  Steps

Install the following:

Python 3.7(https://www.python.org/downloads/release/python-370/)

Install pip

To install pip, run these two commands:

$ curl -O https://bootstrap.pypa.io/get-pip.py

$ python3 get-pip.py --user

pip install -r requirements.txt

Your shell prompt will change to show the name of the activated environment.

Install Flask(https://phoenixnap.com/kb/install-flask)

Within the activated environment, use the following command to install Flask:

$ pip install Flask

##  Ngrok : Link:(https://ngrok.com/download)

Set GH_TOKEN as an environment variable with a value that corresponds to a GitHub Token (ie. export GH_TOKEN=(insert your token) example: 208923487234780287128091)
For steps to generate GH_TOKEN, use this link (https://docs.github.com/en/enterprise-server@3.4/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token

##  Next Steps

Set the user value in app.py

Start the local web service via flask run --host=0.0.0.0 &

Start the forwarding service via ./ngrok http 80

Note the forwarding address (ie. https://cfe6d829.ngrok.io in the output of the ngrok application)

Set up a WebHook in the desired GitHub organization example

Note that the Payload URL should match the forwarding address from ngrok.

Select the individual events radio button and check repositories

Content type should be application/json

Save the Webhook

Create a repository

See that branch protection and an issue was created for the repo!


##  Dependencies and Attribution
Python

Flask

Ngrok

##  Bugs and improvements

Payloads are capped at 25 MB. If your event generates a larger payload, a webhook will not be fired. This may happen, for example, on a create event if many branches or tags are pushed at once. We suggest monitoring your payload size to ensure delivery. See webhooks docs.

There is a 1 second Delay built in to the code which is NOT ideal. It seems the code is checking for the main branch before it is finished creating.

This could be done with AWS Lambda and an API Gateway.

This is a test.