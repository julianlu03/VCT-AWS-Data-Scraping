# VCT-AWS-Data-Scraping
Python notebook used for scraping, chunking, and embedding XML files in order to improve Large Language Model performance by providing domain specific knowledge.

## Background
For a Valorant X AWS Hackathon https://vcthackathon.devpost.com/ our team had to fine-tune a large language model to be able to answer questions regarding Valorant Esports. To achieve this, it was necessary to feed the model domain specific information, such as general game information or pro player statistics, to enhance it's performance in answering these questions. In this case, we are extracting general game knowledge from Valorant's fandom wiki, in hopes for our LLM to gain a deeper understanding of the game. 

## Features
This Python Notebook utlizes the Element Tree library to clean and parse through XML files, chunk the text data, and then uses a Hugging Face text embedding model to transform the chunks into vectors for optimal storage inside of a Knowledge Base.

## 1. Parsing and Cleaning

The notebook parses the XML file titled "valorant_pages.xml", which is a file containing all the text data from the Valorant fandom wiki. The code specifically searches for snippets of text, usually following instances of "== ==" containing a header of sorts, in order to only extract the relevant pieces of information from the wiki (weapon info, agent background, official/community terminology). Once retrieved, the text data was also cleaned up to remove unwanted tags and symbols to improve our later steps. The final output of this step is found in "scrapingoutput.txt". 

## 2. Chunking

This step simply looped through the "scrapingouput.txt" and split the data every 300 characters. This process, called chunking, is necessary for efficiency, maintaining context, and taking in account of model input limitations for our embedding step.

## 3. Vector Embedding

We use Hugging Face's all-MiniLM-L12-v2 model in order to transform our chunks into vector embeddings. This step is important for efficient storage and retrieval of this data when inside our LLM's Knowledge base. 
