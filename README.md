Hey Hi,

I have been recently experimenting with lots of different RAG mechanisms like there was a paper relased by Jina AI which inroduced Late chunking for RAG retrival. Uniquely uses Large context modles for generating a Embeddings of the whole docuement and does some mean pooling with the user querry and the documents. Promisses that it performs better then any other RAG approach. ![late-chunking](https://github.com/jina-ai/late-chunking)


and then we also had Supperposition Prompting from Apple that focuses on parallel processing. 
[Apple SupperPosition Prompting](https://arxiv.org/pdf/2404.06910)



# But These are Better RAG approaches that i have put in practice from past :-

# 1.BM25 retriver 
(pure NLP based Techinque with statical formula highlisghting occurence of a word/ phrase in a chunk/document)

# 2. Processed RAG 

(A approach i came up with personally)

## Chunking
-> A seperate LLm layer dedictaed to consume information from the internet and provide processed chunks which are more search able when user query is in pure natural language.

data(companyinfo)-->chunks--->LLM(chunks info into n number if QnA pairs)

the chunks are in a form of QnA Pairs

question: what is the most selling product
answer: xyz.. is the most selling

The chunking layer is prompted in a way that it 1st
creates a Pobable set of questions a user could ask for given set of information available on the website. 

-> Embeding creation for all Chunks

## Querrying 
-> Preprocesisng of user querry to write better search terms rather then user current user message we also use previous context of user to make the search more effecient
-> Current query and context is sent to GPT4o mini instance to come up with top related 5 questions.

{key word 1, keyword 2, search phrase 1 , search phrase 2, search phrase 3}


# 3. Microsoft GraphRag
Its is by far the best graph rag approach i have ever seen. 
The prompts written for creating entiities and communities along with their Summeries is just so good, With amazing features like local search and global search.


The core idea of GraphRAG can be likened to 'finding a book in a library':

1. Book Classification (Indexing Phase)
 - Breaking a book into paragraphs (Text Chunks): 
 600 token size, 100 token overlap
 Example: 1 book = [1-600], [501-1100], [1001-1600] tokens

- Extract key concepts (Element Instances):
 The LLM extracts the entity, relationship, and claim from each chunk
 In code:
 ```python
 for chunk in book_chunks:
 entities = LLM.extract_entities(chunk)
 relationships = LLM.extract_relationships(chunk)
 claims = LLM.extract_claims(chunk)
 ```

- Concept Summary (Element Summaries):
 Group and summarize extracted concepts
 
- Grouping related concepts (Graph Communities):
 Using the Leiden Algorithm to Detect Graph Communities
 Mathematically: G = (V, E), where V is a node (concept), where E is an edge (relation)
 
- Community Summaries:
 Generate a summary in the form of a report for each community

2. Question Answering (Query Stage)
 - Find Related Groups (Community Answers):
 Select a community summary related to your question
 
- Generate a full answer (Global Answer):
 Aggregate selected summaries to generate a final answer

Performance Evaluation:
- Dataset: about 1 million tokens (enough for 10 novels) 
- Evaluation metrics: Inclusivity, Diversity, Usefulness (0-100 points)
- Results: GraphRAGs score 10-20% higher than baseline RAGs

As an analogy, a GraphRAG is "a student who reads an entire book, summarizes it, and then answers questions." 
A traditional RAG is like a student who only looks at the table of contents and finds and answers related chapters.

This approach is especially useful when you need to have a general understanding of a large document corpus.


### Similarly the due deligence task involves lots of paper work and data rooms can be intergartion, collected documents has lot of interconnected realtions and a normal RAG couldnt have done a good job here, but by establishing Graph like network which hold all the relationships well will really will enhance the search quality. 
 

