# Neural Language Models for the Multilingual, Transcultural, and Multimodal Semantic Web

http://www.semantic-web-journal.net/content/neural-language-models-multilingual-transcultural-and-multimodal-semantic-web

### Dagmar Gromann

-----------

- A vision of a truly multilingual Semantic Web has found strong support with the Linguistic Linked Open  Data community.
- Standards, such as Onto Lex-Lemon, highlight the importance of explicit linguistic modelling in relation to ontologies and knowledge graphs.
- Nevertheless, there is room for improvement in terms of automation, usability, and interoperability.
- Neural Language Models have achieved several breakthroughs and successes considerably beyond Natural Language Processing (NLP) tasks and recently also in terms of multimodal representations.
- Several paths naturally open up to port these successes to the Semantic Web, from automatically translating linguistic information associated with structured knowledge resources to multimodal question-answering with machine translation.
- Language is also an important vehicle for culture, an aspect that deserves considerably more attention.
- This article envisions joint forces between Neural Language Models and Semantic Web technologies for multilingual, transcultural, and multimodal information access and presents open challenges and opportunities in this direction.

#### Multilingual SW

- A true semantic web must be language independent. For this several mediation mechanisms to translate between abstract layers and lexical manifestations are required. NLMs are a useful tool that can contribute to multilingual SW tasks and technologies.
- NLMs can be used for- 
  1. Machine translating the SW -

     - Automatic translation of natural languages on the SW
     - [Translate ontology labels using NMT and SMT](https://arxiv.org/abs/1709.02184)
     - Domain specific terminological knowledge could be injected in NMT and SMT to improve performance. For example - domain adaptation of a trained model with terminological expressions to [translate ontology labels](https://doi.org/10.1016/j.websem.2015.12.001)
  - Some preliminary evaluations, such as the impact of linguistic processing results injected into a neural question-answering system [are available](https://www.aclweb.org/anthology/W19-5806/)
     - Knowledge injection or augmentation holds the potential to help bridge the [neural-symbolic gap](http://www.semantic-web-journal.net/system/files/swj2188.pdf) and support [Explainable AI](http://www.semantic-web-journal.net/content/role-knowledge-graphs-explainable-ai-0)

     - Combination of SW technologies and NMTs can be used to produce multilingual domain-specific ontology description.
     - Unfortunately, Current popular semantic representations such as RDF and OWL might require an adaptation towards the more lightweight end in order to be readily adopted by the NLP community
     
  2. Machine translating to structured languages - 

     - NMT can be used to create a structured knowledge base from free text. 
     - Early neural approaches utilised [joint knowledge base and language embeddings to extract relations](https://www.aclweb.org/anthology/D13-1136/)
     - [Multi-lingual natural language patterns can be utilised to learn RDF predicates](https://www.researchgate.net/publication/262273462_Extracting_Multilingual_Natural-Language_Patterns_for_RDF_Predicates) which are then refined using feed-forward neural nets.
     - Recent approaches treat the entire problem of [structure learning as a machine translation task using NMT to learn a specific subset of Description Logic Formulas](https://www.sciencedirect.com/science/article/abs/pii/S1570826818300507)
     - NMTs could also be used to translate natural language queries to SPARQL. A broad test such models has been proposed [here](https://arxiv.org/abs/1806.07941)

     - Automating the process of extracting structured knowledge from natural language holds the promise of obtaining conceptualisation specific to language and culture.
     - Joining both technologies could create the ability to adapt training models to new domains and languages.

  3. Machine translation for reasoning -
     - A very recent approach is to tailor embeddings to [accommodate RDFS reasoning in and NMT task](https://content.iospress.com/articles/semantic-web/sw190363)
     - Encoding information as input to NLM- based reasoning engines is an open research topic.
     - If embeddings learned for the purpose of reasoning in one formalism might allow for transitioning to or similarity measures of elements or statements in different representation languages, it could be a potential approach for [tackling diversity of ontology languages](https://www.researchgate.net/publication/319395285_The_Distributed_Ontology_Modeling_and_Specification_Language)
     - The challenge in combining machine learning and logic lies in conciliating advantages of both without aggravating their limitations.
     - An additional opportunity here is a hybrid interaction of both methodologies, as [proposed
       for image segmentation](https://content.iospress.com/articles/semantic-web/sw190362)
     - A discussion for a truly hybrid neural-symbolic systems can be found [here](http://www.semantic-web-journal.net/system/files/swj2188.pdf)

  4. NLM based ontology alignment - 
     - NLM-based alignment strategies could benefit from the previous tasks in form of using neural-symbolic reasoning to align large multilingual, transcultural, and multimodal ontologies
     - The substantial surge of knowledge graph embedding approaches could be joint with the multitude of word embedding models, building on and contributing to the tradition of modelling at the ontology-natural language interface of the SW community
     - Joint NLM- and SW-based alignment approaches can potentially also foster the transitioning from knowledge represented in one cultural context to another.
     - Pretrained multilingual word embeddings have been compared for [ontology alignment](https://www.aclweb.org/anthology/L18-1034/)
     - [Large scale ontology alignment](http://ceur-ws.org/Vol-2180/paper-28.pdf) has been divided into smaller, manageable tasks using lexical indexing and neural embeddings.

#### Multimodal SW

- NLMs promise to boost not only the SW’s multilinguality but are capable of contributing to its multimodality.
- NLMs can be used for -
  1. Semantic Speech Technologies -
     - Speech technologies building on SW resources and NLM systems promise to support important present-day applications, such as assisted living.
     - Google registered a [patent](https://patents.google.com/patent/US9478145) on utilising language models for understanding conversations based on SW resource.
     - A speech interface for question-answering systems has been [proposed](https://www.sciencedirect.com/science/article/abs/pii/S0167639316301443), which, in combination with the above multilingual strategies for NLM-based question answering, could provide broad access to SW resources
- Another Google patent for reformulations of speech queries has been [registered](https://patents.google.com/patent/US8521526), providing alternative queries if the submitted one returns no results
      - Building on neural-symbolic reasoning, such systems could enable a multilingual, multimodal query-answering system on formally structured resources.
      - But Local contexts and linguistic variations need to be taken into account to grant broad information access and a high usability.
  2. Semantic Video Technologies - 
     - In order to include the visual-manual modality to convey meaning in form of sign language, knowledge needs to be conveyed by video.
     - An approach to combine speech synthesis, machine translation, and SW technologies to create a machine-readable knowledge representation for the Turkish sign language can be found [here](https://www.sciencedirect.com/science/article/abs/pii/S0950705116300557)
     - Therefore translation between natural language and sign language using NMT has also been [suggested](https://aircconline.com/ijnlc/V6N3/6317ijnlc03.pdf)
     - Unfortunately, semantic video technologies still suffer from a lack of broad coverage in terms of language and visual-manual modality
     - But a video-enabled NLM-based SW can strongly support barrier-free online communication, especially if transformations between different modalities are provided.
  3. Semantic Sensor Web - 
     - Building on SW enablement sensor data is linked and annotated. This allows [SW queries to be applied to sensor data](https://dl.acm.org/doi/10.4018/jswis.2012010103) 
     - Its link to NLMs comes from the necessity of connecting sensor data to human communication means, the human-robot interface, such as [natural language understanding of robot instructions](http://arxiv.org/abs/1903.09243) 
     - Sensory representations, their semantic representations and neural-symbolic reasoning could be highly beneficial to the tasks of [explainable AI](http://www-sop.inria.fr/members/Freddy.Lecue/presentation/ISWC2019-FreddyLecue-Thales-OnTheRoleOfKnowledgeGraphsInExplainableAI.pdf) 
     - NLMs and sensor data both suffer from biases and hence there is a risk of multiplying and intensifying biases across modalities.

#### Transcultural SW

- Transcultural refers to a social concept that denotes a joint shared culture irrespective of origin.

- For a semantic web the capacity to move between and within cultural and social identity is foreseen.

- Cultural Evolution -

  - A theory and experiments for the cultural evolution of human language has been thoroughly investigated
  - It also studies how linguistic variants are generated in a population and on which basis some variants survive and become dominant
  - As a social feature, language consists of cooperative interaction patterns such as open-ended questions.
  - While many of these phenomena are language-specific, it is highly unlikely that vocabularies and grammars are stored as different language systems by users. 
  - Instead, a widely accepted theory is that of storing such knowledge in form of constructions, associating meaning with form. One construction stores many constraints for efficient parsing and is presumed to incorporate several different language systems
  - Various grammars have been proposed to capture such linguistic constructions. NLMs potentially complement tested construction grammar approaches, increasing the level of automation and potentially domain coverage by means of transfer learning. 
  - NLM-based multi-agent system negotiations of meaning could foster transcultural modelling of cultural evolution.

- Cultural Heritage - 

  - The range of possible joint approaches of NLM and SW technologies to model cultural heritage includes the multilingual and most of the multimodal approaches presented here.

  - For instance, based on knowledge graphs, NLMs can be utilised to analyse similarities and differences across cultural heritages as well as refine technologies to share and analyse cultural data.
  - One of the most central challenges in terms of cultural heritage is the linking and representing of
    cultural data in a harmonised way across individual data collections. Here symbolic ontology-based integration methods could strongly benefit from NLMs and their ability to detect similarities even with noisy data.

- Culture-Specific Modelling -

  - Another important transcultural SW connection is that of utilising ontologies for culture-specific modelling
  - But when utilising SW technologies for cross-cultural modelling, lexical gaps rapidly become unavoidable
  - Cross-language information retrieval (CLIR) tasks equally encounter this problem, and have come up with NLM-based methods to bridge such lexical gaps [54]
  - Going from modelling individual culture-specific knowledge representations to a transcultural one is a big challenge.
  - Domain ontologies potentially provide a language-independent anchor for transcultural knowledge modelling, joint with NLM-based cross-language information retrieval and analysis approaches.  
  - Bringing both together enables transcultural question-answering and potentially automated localisation approaches.
  - A strong cognitive framework could be used to analyse and model cultural differences on a cognitive-conceptual basis rather than a primarily data-driven approach.



