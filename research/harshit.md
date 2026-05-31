# Component

LLM Layer

# Proposed Technology

OpenAI GPT-5

# What does this component do?

The LLM Layer is the AI Reasoning Layer of the project. it receives enriched , retreived context from the hybrid retreival engine and generated answers to questions based on the knowledge graph and input data .The reasoning layer does NOT operate freely. It only works with verified retrieved context. This is extremely important,questions like :
"Why was this migration performed?"
"Which deployments caused incidents recently?"
the llm only SUMMARIZES inputed data like discussions , incident reports ,migration reasoning architectural tradeoffs and does not decide infrastructural relationships . The model is constrained to:
    retrieved evidence, 
    graph relationships, 
    extracted documents, 
    discussions,	
    timelines. 
The system explicitly prevents unsupported inference. 


# Why did you choose this technology?

- GPT-5 is the best-in-class model for Agentic/Tool Use — critical since the LLM layer must call vector search, graph DB, and hybrid retrieval simultaneously
- considering that the project would require a lot of input data , we need an llm which can allow processing multiple tokens .922k context window allows processing entire PRs, RFCs, Slack threads, and incident reports together in a single call
- Reason 3

# Advantages

- Massive 922k context window reduces need for excessive chunking of large engineering documents like RFCs and architecture docs
- Best-in-class agentic tool use for calling retrieval engine and graph layer and 45% fewer hallucinations than GPT-4o — critical since a hallucinated service dependency or fake incident summary can lead engineers to make wrong architectural decisions or miss real root causes

# Limitations

- Expensive at scale — querying across thousands of PRs, incidents, and Slack threads can make costs explode
- Closed source / proprietary — model weights are not publicly available, meaning the system cannot be self-hosted or audited
- Vendor lock-in — dependent on OpenAI's pricing and availability decisions
- Slight latency overhead compared to smaller models


# Would you use it in Company Brain?

Yes , this would be a perfect llm layer for the project because of its reduced hallucination rate , massive context windows(tokens large dataset) and agentic capabilities. the llm only summarizes verified, machine-grounded data it never
invents infrastructure relationshipswhich is a primary rule .
if cost comes out to be a problem , we can use GPT -4o as it has significantly lesser cost but greater hallucination rate or we can use gemini.

# References

-https://youtu.be/n4NokjyAklg?si=mxKrqxOP4w_IKHrw
-https://youtu.be/pYax2rupKEY?si=afSXsIjwpX8GizyC
-https://artificialanalysis.ai/leaderboards/models
-https://openai.com/index/introducing-gpt-5/
-https://www.geeksforgeeks.org/machine-learning/top-20-llm-models/

