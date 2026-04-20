First retrieves relavant information from your own data

Then uses that information to generate the answer

## Process

1. **Data Ingestion** - load and process raw data include cleaning the text.
2. **Chunking** - split long documents into smaller chunks and attach metadata to each chunk.
3. **Embedding** - convert each text chunk into a vector representation using embedding model.
4. **Vector Index Instruction** - store the embeddings in a vector index(such as FAISS, Milvus, Qdrant, or Pinecone) to enable efficient similarity-based retrieval.
5. **Retrieval** - when user submit a query, embed the query using the same embedding model and retrieve the top-k most relevant chunks from the vector based on similarity.
6. **Prompt Construction** - assemble a prompt by injecting the retrieve context into a predefined template, then pass it to the LLM to generate an answer.
7. **Generation** - the LLM generate a response using the retrieved context, producing an answer grounded in the source documents.
8. **Evaluation and Optimization** - evaluate retrieval quality and answer accuracy, then iteratively improve the system by tuning parameters, such as chunk size, overlap, top-k value, reranking strategies, and prompt design.

## Evaluate

### Measure Retrieval

#### MMR(Mean Reciprocal Rank)

> Important for QA-style systems
>
> $$
> MRR=1/rankoffirstrelevantdocument
> $$

## Advanced

1. **Chunking R&D**: experiment with chunking strategy
2. **Encoder R&D**: select the best Encoder model based on a test set
3. **Improve Prompts**: generate content, the current date, relevant context and history
4. **Document pre-processing**: use an LLM to make the chunks and/or text for encoding
5. **Query rewriting**: use an LLM to convert the user's question to a RAG query
6. **Query expansion**: use an LLM to turn the question into multiple RAG queries
7. **Re-ranking**: use an LLM to sub-select from RAG results
8. **Hierarchical**: use an LLM to summarize at multiple levels
9. **Graph RAG**: retrieve content closely related to similar documents
10. **Agentic RAG**: use Agents for retrieval, combining with Memory and Tools such as SQL
