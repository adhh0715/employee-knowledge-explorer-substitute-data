# Employee Knowledge Explorer — Substitute Data

Prepared for Aditya Siddaarth, 2 November 2026.

**Dataset disclosure:** this project uses six AI-authored fictional policy files, explicitly authorized by the student after the instructor dataset could not be obtained. These are **not** the instructor-supplied Northstar policies. The original assignment asks for the supplied data; evaluator acceptance of the substitution is unconfirmed. No official grade or exact-dataset compliance is claimed.

## Run

Open [the executed notebook](Employee_Knowledge_Explorer_Substitute_Data.ipynb) using its Colab badge, or use [the editable Colab copy](https://colab.research.google.com/drive/13gKPcYkj9BTzntM_LlKBrP5xcLXB-opq). Run the setup, substitute-data creation, twelve required functions, integration harness, comparison cell and supplementary probes in order. Skip the explicitly optional DeepSeek extension; no API key is required. The package/model downloads require internet access.

The notebook contains the complete substitute corpus and recreates it automatically at /content/northstar_substitute_knowledge_base. The same six documents are also included in [data/](data/). It creates Northstar_Substitute_Employee_Knowledge_Base.zip with a provenance notice. No manual upload of the unavailable instructor ZIP is needed for this version.

## Implementation

All twelve required functions are implemented: loading stable document IDs and metadata; TF-IDF ranking and budgeted source-labeled context; normalized BAAI/bge-small-en-v1.5 embeddings; FAISS IndexFlatIP with IndexIDMap; LlamaIndex Documents and Nodes; persistent Chroma upsert/query/filtering; and metadata updates. The original integration assertions and seven reference cases are preserved.

## Actual validation

- Six documents (1001–1006), seven LlamaIndex Nodes, seven persistent Chroma records.
- The original harness printed **All structural checks passed.** IT filtering and review_status update succeeded.
- TF-IDF, FAISS and Chroma each ranked the expected source first for **6/6 in-scope reference questions**. This purpose-written corpus was created with the visible test topics in mind; these are development results, not held-out evaluation or answer correctness scores.
- Re-upsert did not duplicate records; a reopened persistent client saw seven records. Context-budget, zero lexical signal and missing-ID checks passed.
- Cafeteria query: TF-IDF retrieved Benefits; FAISS/Chroma retrieved HR. Neither contains a menu, so all results are insufficient evidence.
- Extra workstation/temporary-machine paraphrase: TF-IDF found no match; FAISS and Chroma retrieved IT.
- Extra bereavement/absence query: all methods incorrectly retrieved Benefits for the manually intended HR topic. The notebook documents this ambiguity rather than claiming semantic search always wins.

FAISS searches whole files and returns larger-is-better similarity; Chroma searches Nodes and returns smaller-is-better default L2 distance. Do not compare raw values directly. Deterministic node IDs here depend on fixed input order and are not a general version-management strategy.

The executed outputs and Step 15 reflection are visible in the notebook. No API keys, model caches or Chroma database folders are included.
