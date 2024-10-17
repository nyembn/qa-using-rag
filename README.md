# A QA notebook over text data using LangChain and OpenAI
This notebook implements QA over a blog post. RAG is implemented.

## Indexing
- WebBaseLoader is used to load contents of a blog post to list of Document.
- RecursiveCharacterTextSplitter is used to split the loaded document into chunk size of 1000 chracters with chunk overlap of 200 chracters.
- Stored and embedded all document splits using Chroma and OpenAIEmbedding model.
## Retrieval and Generation
- The VectorStore is turned into a Retriever.
- The rag_chain components retriever, prompt and llm are instances of Runnable. They implement the same methods such as sync and async .stream, .invoke or .batch. It makes them easier to connect together. The chain retriever | format_docs passes the question through the retriever which generates Document objects. format_docs generate strings. The last two components of the chain are llm that runs the inference and StrOutputParser() which plucks the string content out of the LLM's output message.