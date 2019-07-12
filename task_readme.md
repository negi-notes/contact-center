# Ubuntu Conversation Challenge

Welcome to the EdgeTier NLP and data science code challenge.

You are required to read the scenario below, and submit a Jupyter notebook (or similar) with your analysis and output in answer to both parts of the challenge.

# Scenario

Ubuntu is a linux-based operating system that has millions of users globally. You have been tasked with setting up a contact centre that will service queries from Ubuntu users in English from around the globe, covering all types of issues. The contact centre will work across chat-based channels.

To help you, the zip file in the data directory of this repository contains the details of 362,200 conversations that have occurred between volunteer technical advisors and Ubuntu users between January 2010 and December 2011. Conversations were completed with a chat-based tool and each is a 1-1 interaction consisting of multiple messages over and back.

# Data Download

There is an example Jupyter notebook in the repository that will download the data for this task, and unzip it in your local machine.

You can run the notebook using (assuming you have Python installed):

```
git clone https://bitbucket.org/killbiller/ubuntu-conversation-challenge/src/master/
cd ubuntu-conversation-challenge
pip install -r requirements.txt
jupyter notebook
```

The data in the zip file will unzip to create a comma-separate-value file with one row per message sent, and the following columns:

* conversation_id: an ID that indicates the conversation that this message belongs to.
* datetime: the time and date that the message was sent / received.
* to: username of the user that this message was sent to. This field is left blank at the start of a conversation, before someone responds.
* from: the user who sent this message.
* text: the text contents of the message

# Challenge

There are two parts of this challenge. Feel free to create the solutions in the language or tool of your choice.

## 1: Choose your agents

You have been tasked with the selection of 15 users from the dataset to form the customer service agents for a new professional contact centre for Ubuntu support. 

Using the data provided, select 15 users that you see in the dataset, and please provide validation with workings, summary statistics, and any visualisations to help motivate your selection. 

To limit time, we would recommend generating appoximately 3 simple visualisations that you think would assist your choice and explaining how and why you used those.

## 2: Phatic-chat detector

Efficiency is key in any customer contact centre. Agents are expensive, and priced per minute. 

For this challenge, you are tasked with building a phatic expression classifier. Phatic conversation is language used for general purposes of social interaction, rather than to convey information or ask questions. Utterances such as "hello, how are you?" and "nice morning, isn't it?" are phatic. 

You need to design a classification model that can accurately detect the messages and sentences that add no significant information in the message data provided.

Examples of phatic conversation that we'd like to include:
 
* Greetings: hello, hi, hi there, good morning, good evening, etc.
* Farewells: bye, adios, see you later, good bye, etc.
* Pleasantries: thanks, cheers, thank you, please, etc.

You are required to detect full messages that are made up of niceties, or sentences within longer messages that are niceties. You are not required to detect niceties within longer sentences. e.g. "Hey, I need help with my password."

With the classifier you design and build, the contact centre will build an automated system to remove niceties from messages, and reduce reading time for agents to operate more effectively.

Feel free to use any model paradigm, libraries, technologies, or external data, that you please. As a submission, please provide workings and some measure of model accuracy.

# Submission

Please submit workings as a git repository that we can clone, with results embedded, or with code that we can run locally to generate the required output.

To get started, there is a sample Jupyter notebook provided in "initial_data_load.ipynb" that demonstrates how you can access the raw Ubuntu data from our file store.

Please note that there is a vast number of messages in this dataset, if processing time becomes an issue, feel free to use a subset of the data to reduce the time required.