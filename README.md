# Chain-of-agents
An experimental implementation of Google's "Chain of Agents: Large Language Models Collaborating on Long-Context Tasks" paper. It's far from production-ready, but I get very good results with it even with relatively weak models. The main use case would be very large documents (100-200K tokens) where the user query needs multi-hop reasoning so a basic RAG would fall short there.

## Key Enhancements from Original Paper
- **Enhanced prompt engineering**: Implemented sophisticated prompting strategies for both worker and manager agents, optimized for small model limitations (8B/3B) and capabilities.
- **Dynamic Context-Aware Chunking**: Incorporates TF-IDF analysis and cosine similarity metrics; prioritizes contextually relevant document segments; adaptive document splitting algorithms.
- **Entropy-Based Prioritization**: Use Shannon entropy calculations for content diversity assessment; intelligent document subdivision decisions
- **Hierarchical Processing Structure**: Implements a depth-limited binary tree architecture; systematic processing of complex content.

The PDF processing is quite basic, using PyMuPDF and a few regex to filter things we don't want (references, citations, whitespaces...). 

I tested the framework on Google's paper using vLLM backend, with a quantized llama3.1-8B-AWQ model. By using ngram prompt lookup decoding, the chain of reasoning can be done in ~45 seconds on Kaggle using a single T4.

I also tested the framework using a llama3.2 3B AWQ quantized model, it still works somehow with a bit of degradation compared to the 8B.

## Citation
```bibtex
@misc{zhang2024chainagentslargelanguage,
      title={Chain of Agents: Large Language Models Collaborating on Long-Context Tasks}, 
      author={Yusen Zhang and Ruoxi Sun and Yanfei Chen and Tomas Pfister and Rui Zhang and Sercan Ö. Arik},
      year={2024},
      eprint={2406.02818},
      archivePrefix={arXiv},
      primaryClass={cs.CL},
      url={https://arxiv.org/abs/2406.02818}, 
}
