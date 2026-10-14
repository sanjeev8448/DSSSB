## 1. What is NLP?

Natural Language Processing (NLP) is a branch of Artificial Intelligence that enables computers to process, analyze, understand, and generate human language, such as English and Hindi.

NLP works with both:

- Text: Emails, documents, messages, and search queries.
    
- Speech: Spoken commands, conversations, and voice recordings, often combined with speech recognition and speech synthesis.
    

### Examples

- Google Translate translates text between languages.
    
- Spam filters identify unwanted emails.
    
- Chatbots answer questions in natural language.
    
- Speech assistants interpret spoken commands.
    
- Sentiment analysis identifies positive, negative, or neutral opinions in text.
    

## 2. Applications of NLP

|Application|Purpose|Example|
|---|---|---|
|Machine translation|Converts text between languages|English to Hindi translation|
|Sentiment analysis|Identifies opinions or emotions in text|Classifying a review as positive or negative|
|Spam detection|Identifies unwanted messages|Email spam filters|
|Text summarization|Produces a shorter version of text|Summarizing a long article|
|Speech recognition|Converts spoken language into text|Voice typing|
|Question answering|Answers questions written in natural language|A customer support assistant|
|Information extraction|Extracts important details from text|Identifying dates, names, and locations|
|Text generation|Produces human-readable text|Drafting an email|
|Search and information retrieval|Helps match a query with relevant information|Searching documents using natural-language queries|

Exam tip: Speech recognition and NLP are related but not identical. Speech recognition converts speech into text; NLP can then analyze or interpret that text.

## 3. Chatbots

A chatbot is a software application that interacts with users through text or voice. It may answer questions, provide information, or perform tasks.

Many chatbots use NLP to interpret user messages and generate relevant responses.

### Types of chatbots

A. Rule-based chatbot

Uses predefined rules, keywords, decision trees, or scripted responses.

Example: A college chatbot responds to “admission fees” with a predefined fee-information message.

Limitation: It may struggle with unexpected wording or questions outside its rules.

B. AI-powered chatbot

Uses techniques such as NLP and sometimes Machine Learning to interpret messages and generate or select responses.

Example: A support chatbot that understands differently worded questions about refunds.

Limitation: It may misunderstand questions or generate incorrect information.

### How a basic chatbot works

User input

“Where is my order?”

Language processing

Interpret the request and identify its intent

Response generation

Retrieve order information or ask for an order ID

Response to user

“Please provide your order ID.”

### Important chatbot terms

- Intent: What the user wants to accomplish, such as tracking an order.
    
- Entity: A relevant piece of information, such as an order number or date.
    
- Dialogue management: Controls the flow of the conversation and determines what to ask or do next.
    
- Response generation: Produces or selects the chatbot's reply.
    

## 4. Basic language processing

NLP systems often perform several stages to process text. These are useful fundamentals for exam questions.

### A. Tokenization

Splits text into smaller units called tokens, such as words, subwords, or punctuation.

Example:

`I love computers!`

Possible tokens: `I`, `love`, `computers`, `!`

### B. Stop-word removal

Removes common words that may contribute little to a particular analysis, such as “the,” “is,” and “a.”

Example:

`The computer is fast.` → `computer`, `fast`

Stop-word removal is task-dependent; these words are not always removed.

### C. Stemming

Reduces a word to a simplified stem, which may not be a valid dictionary word.

Example:

`playing`, `played`, `plays` → `play`

The actual result depends on the stemming algorithm.

### D. Lemmatization

Reduces a word to its dictionary base form, called a lemma, using linguistic information.

Example:

`am`, `is`, `are` → `be`

Stemming vs lemmatization: Stemming typically applies simpler word-reduction rules; lemmatization aims to return a valid base word.

### E. Part-of-speech tagging (POS tagging)

Identifies grammatical roles such as noun, verb, adjective, and adverb.

Example:

In “The student reads quickly”:

- student — noun
    
- reads — verb
    
- quickly — adverb
    

### F. Named Entity Recognition (NER)

Identifies named entities such as people, organizations, locations, and dates.

Example:

`Ravi lives in Delhi.`

- Ravi — person
    
- Delhi — location
    

### G. Sentiment analysis

Determines the sentiment or opinion expressed in a text.

Example:

`The service was excellent.` → Positive sentiment.

### H. Parsing

Analyzes the grammatical structure of a sentence and the relationships between its words.

Example: Identifying which noun is the subject and which verb describes its action.

These stages are not always performed in a fixed sequence, and an NLP application may use only the stages relevant to its task.

## 5. Important NLP terms at a glance

| Term               | Remember                                      |
| ------------------ | --------------------------------------------- |
| NLP                | Processes and generates human language        |
| Tokenization       | Splits text into tokens                       |
| Stop-word removal  | Removes selected common words                 |
| Stemming           | Reduces words to approximate stems            |
| Lemmatization      | Finds dictionary base forms                   |
| POS tagging        | Identifies grammatical roles                  |
| NER                | Identifies names, places, organizations, etc. |
| Sentiment analysis | Detects opinions or sentiment                 |
| Parsing            | Analyzes grammatical structure                |
| Chatbot intent     | What the user wants                           |
| Chatbot entity     | Important information in the message          |
### Last-minute revision

- NLP: Enables computers to process human language.
    
- Chatbots: Interact with users through text or voice.
    
- Tokenization: Splits text into tokens.
    
- Stemming: Produces simplified word stems.
    
- Lemmatization: Finds dictionary base forms.
    
- POS tagging: Identifies grammatical roles.
    
- NER: Identifies people, places, and organizations.
    
- Sentiment analysis: Detects positive, negative, or neutral sentiment.