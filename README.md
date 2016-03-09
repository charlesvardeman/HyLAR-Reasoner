# HyLAR-Reasoner #

HyLAR-Reasoner is an OWL 2 RL reasoner that uses JSW and OWLReasoner (https://code.google.com/p/owlreasoner/) as a triplestore and provides an additional incremental reasoning engine. The framework implementation of HyLAR is available at https://github.com/ucbl/HyLAR.

## Getting started ##

### Use HyLAR's reasoner module locally ###

1) Install locally

`npm install --save hylar`

2) Import HyLAR, then classify your ontology and query it

(currently accepts OWL 2 XML serialization only)

```
var Hylar = require('hylar');
var classifiedOntology, queryResults;

classifiedOntology = Hylar.classify('./fipa.owl'));

queryResults = Hylar.query('PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#> ' +
                            'PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#> ' +
                            'SELECT ?a ?b { ?a rdfs:subClassOf ?b }');
```

### Use HyLAR as a server ###

1) Install HyLAR globally:
`npm install -g hylar`

2) Use CLI to run HyLAR as a server:
`hylar --port 3123`

`--port <port_number>` or `-p <port_number>` is optional. HyLAR runs at port 3000 by default.

It then outputs:
```
[HyLAR] Setting up routes...
[HyLAR] Done.
[HyLAR] Exposing server to port 3003...
[HyLAR] Done.
[HyLAR] HyLAR is running.
```

3) Once HyLAR is launched, it can be requested as follows:

(GET) `/classify`
> Parameters
`filename` (the absolute path of the ontology file to be processed)
Parses and classify an ontology (OWL 2 XML serialization). Supports Classes, ObjectProperties and DatatypeProperties. This step has to be done before sending any SPARQL query (but only once, as the reasoner instance is kept in-memory).

(GET) `/query`
> Parameters
`query` (the SPARQL query string)