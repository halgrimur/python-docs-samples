# Wikibot example that can be run on Google Compute Engine

This sample shows how to use the [SleekXMPP](http://sleekxmpp.com/index.html)
client and [Flask](http://flask.pocoo.org/) to build a simple chatbot that can
be run on [Google Compute Engine](https://cloud.google.com/compute/). The
chatbot does two things:
	
1. Sends messages to XMPP users via http get:
	* The server is running on port 5000
	* if running on virtual machine use: http://<MACHINE IP>:5000/send_message?recipient=<RECIPIENT ADDRESS>&message=<MSG>
	* If running locally use: http://localhost:5000/send_message?recipient=<RECIPIENT ADDRESS>&message=<MSG>

2. Responds to incoming messages with a Wikipedia page on the topic:
	* Send a message with a topic (e.g., 'Hawaii') to the XMPP account the server is using
	* It should respond with a Wikipedia page (when one exists)

## Setup

Download the [Google Cloud SDK](https://cloud.google.com/sdk/) to your local machine.
It will allow you to access many of the features of Google Compute Engine via
your local machine.

Clone this project to your local machine.

Follow the instructions at the 
[Compute Engine Quickstart Guide](https://cloud.google.com/compute/docs/quickstart-linux)
on how to create a project, create a virtual machine, and connect to your
instance via SSH. 

Copy the `wikibot.py` and `requirements.txt` files from this sample to your remote 
instance running in Compute Engine. See
[Transferring Files](https://cloud.google.com/compute/docs/instances/transfer-files)
for more information.

Install the dependencies using [pip](http://pip.readthedocs.io/en/stable/):

    pip install -r requirements.txt


Enable tcp traffic on port 5000 to send messages to the XMPP server, by running the following SDK commands:
    
    gcloud config set project <YOUR PROJECT NAME>

    gcloud compute firewall-rules create wikibot-server-rule --allow tcp:5000 --source-ranges=0.0.0.0/0

Alternatively to enabling `tcp` traffic on port 5000,  you can create a new firewall rule via the UI in the 
[Networks](https://console.cloud.google.com/networking/networks/list) section of
the Google Cloud Console.

## Running the sample

You'll need to have an XMPP account prior to actually running the sample.
If you do not have one, you can easily create an account at one of the many
XMPP servers such as [Jabber.at](https://jabber.at/account/register/).
Once you have an account, run the following command:

    python wikibot.py -j '<YOUR XMPP USERNAME>' -p '<PASSWORD>'

Where the username (e.g., 'bob@jabber.at') and password for the account that
you'd like to use for your chatbot are passed in as arguments.

Enter control-Z to stop the server


### Running on your local machine

You may also run the sample locally by simply copying `wikibot.py` to a project
directory and installing all python dependencies there.
