# v0.0.1 -> Britishslavetraders
Tastade started with the data model from the Britishslavetraders project as a basis. The data models/profiles are integrated in a data entry Editor, and can be seen in XML in [this release](https://github.com/knaw-huc/iisg-tastade-editor/releases/tag/v0.1.0) Editor's Github repository.

# v0.1.0 until v0.4.0 -> Conceptual sketches
These were the initial conceptual sketches by the researchers about the main classes and relations between them.

# v0.2.0 -> CMDI XML profiles
This version lives in the data entry Editor only in the form of XML profiles, it corresponds to [this Editor's release](https://github.com/knaw-huc/iisg-tastade-editor/releases/tag/v1.0.0).

# v1.0.0 (2026-08-29) -> CIDOC CRM based ontology in RDFS 
- First version of the ontology in RDFS, built on the basis of [CIDOC CRM v7.1.3](https://cidoc-crm.org/Version/version-7.1.3).
- Built with Protégé.
- From this version the TASTADE ontology is implemented in different versions of the data entry [Editor](https://github.com/knaw-huc/iisg-tastade-editor).
- It includes the main classes from the previous versions of the ontology, but aligned with CIDOC.
- This version extends CIDOC in this way:
    - It reuses the main CIDOC classes, among others:
        - Source (E31)
        - Actor (E39)
        - Place (E53)
        - Time-Span (E52)
        - Type (E55)
        - Legal Object (E72)
        - Currency (E98)
    - It defines the main specific TASTADE subclasses:
        - "Outfitting Partnership", "Polity", "Trading Company" as subclasses of Group (E74)
        - "Financial Instrument" (which includes "Share" and "Loan") as subclasses of Legal Object (E72)
        - "Financial Event" and "Actor Event" as subclasses of Activity (E7)
    - It adds a reified "Binary Relationship" as a subclass of Temporal Entity (E2) for representing binary relationships (personal relationships, group, intergroup and ownership and place ruling relationships) (See Clarifications below (*)).
      In the implementation of this approach, the relationship is typed in a Relation Type subclass (under Type, E55), and via a skos:Concept relation to a relationships controlled vocabulary.
    - It reuses two classes from the SeaLit ontology (https://zenodo.org/records/5964240; see also [this presentation](https://cidoc-crm.org/sites/default/files/The%20SeaLiT%20Ontology%20-%2052nd%20CIDOC%20CRM%20SIG%20-%20FEB%202022.pdf)):
        - Ship as a subclass of Human-Made Object (E22)
        - "Voyage" as a subclass of Activity (E7), but it is called "Crossing" in TASTADE.
- It adds an "Epistemic Status" class with "Observation" and "Reconstruction" as subclasses, although this is not always consistently added to the instances in this version.
- It adds several TASTADE own properties, one of the most important is the property hierarchy for binary relationships: The relationFrom/relationTo parent properties with subclasses (hasOwner, hasMember, hasEmployee, isAssociatedWithGroup, hasRulingPolity, etc.)
- Known limitations in this version:
    - It doesn't fully adopt CIDOC CRM in some cases, for example: TASTADE uses direct properties for common events: birthPlace, birthDate on Person (rather than requiring full E67_Birth events).
    - Epistemic Status (Observation/Reconstruction) are not consistently applied to all instances yet
    - Some places lack full falls_within chains
    - Some polities lack Wikidata sameAs links
- Clarifications:
  - Notes (e.g., extra comments or notes) are not part of the Ontology, they are only added to the Editor's metadata profiles.
  - (*) This approach is inspired in other projects which also needed native support for time-spans, source attribution, and typed relationships. Those projects are: BIO-CRM (https://seco.cs.aalto.fi/projects/biographies/biocrm-2026-02-11.pdf) and AAAO (https://www.sari.uzh.ch/en/ordea/aaao.html). The TASTADE ontology doesn't reuse those models directly, but it adapts their principles and some of their concepts.
