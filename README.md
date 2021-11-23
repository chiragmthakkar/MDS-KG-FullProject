# MDS-BIMKG
This repository is for Masters of Data Science project for Chirag M Thakkar (a1806400)

```bash
pip install requirements.txt
```


## Installing Stanza

There are two ways of installing/using OpenIE Stanza:
1. Using pip install [stanza](https://stanfordnlp.github.io/stanza/)

2. Using [coreNLP Client](https://stanfordnlp.github.io/stanza/corenlp_client.html) and then Stanza.
   Example:
   
   ```python
   
   from stanza.server import CoreNLPClient

   text = "I miss Mox Opal"

   #with CoreNLPClient(annotators=["tokenize","ssplit","pos","lemma","depparse","natlog","openie"], be_quiet=False) as client:
   with CoreNLPClient(annotators=["openie"], be_quiet=False) as client:
       ann = client.annotate(text)
       #print(ann)
       for sentence in ann.sentence:
           for triple in sentence.openieTriple:
               print(triple)
   
   ```
   

## Steps involved

1. Extracting data from the 20 journals in the [20journalDataExtraction](https://github.cs.adelaide.edu.au/a1806400/MDS-BIMKG/tree/master/20journalDataExtraction)

```bash
├── 20journalDataExtraction
│   ├── **/*.ipynb
├── 20journalAfterClusterErData.ipynb
├── final20JOurnalFullData.csv
├── neo4jUI.html
├── requirements.txt
├── README.md
└── .gitignore
```


2. Concatinating data from 20 journals
3. Word2vec, dictionary creation and similarity mapping [here](https://github.cs.adelaide.edu.au/a1806400/MDS-BIMKG/blob/master/21journalAfterClusterErData.ipynb)
4. Neo4j user interface 
   1. Import the ['final20JOurnalFullData.csv'](https://github.cs.adelaide.edu.au/a1806400/MDS-BIMKG/blob/master/final20JOurnalFullData.csv) data in the import folder in Neo4j Desktop version. Run the following query in the Desktop version.
   
       Cypher Query

       ```python
       LOAD CSV FROM 'file:///final20JOurnalFullData.csv' AS line  
       MERGE (n:Entity {name : line[1]})  
       WITH line, n  
       MERGE (m:Entity {name : line[2]})  
       WITH m,n,line[3] as relName, line[4] as urlName, line[5] as jName  
       MERGE (m)-[rel1:RELATED{name:relName,url:urlName, journal: jName}]->(n); 
       ```
       
     2. Run the [neo4j UI](https://github.cs.adelaide.edu.au/a1806400/MDS-BIMKG/blob/master/neo4jUI.html)
        The UI uses the [Neovis.js](https://github.com/neo4j-contrib/neovis.js) used for displaying the cypher query results on the web application.
        


![alt text](https://github.cs.adelaide.edu.au/a1806400/MDS-BIMKG/blob/master/wholeUI.png)



In case of any queries, please feel free to reach out at 1806400@student.adelaide.edu.au









