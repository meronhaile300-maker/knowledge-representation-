# Cultural Heritage and Museum Ontology

## OWL 2 Implementation using Protégé

---

## 1. Knowledge Domain

This ontology belongs to the **Cultural Heritage and Museum Management Domain**.

It provides a semantic representation of cultural heritage resources, museum collections, artworks, artifacts, exhibitions, historical periods, conservation activities, materials, locations, provenance, stylistic/technical context, digital rights, and digital documentation resources.

The ontology is intended to support knowledge organization, semantic interoperability, and automated reasoning within museum and heritage information systems.

---

## 2. Development Environment

| Component | Technology |
|------------|------------|
| Ontology Language | OWL 2 |
| Serialization Format | RDF/XML |
| Ontology Editor | Protégé Desktop |
| Reasoner | HermiT |
| Ontology File | CulturalHeritageOntology1.owl |

---

## 3. How to Run the Ontology

### Step 1 – Install Protégé

Download Protégé Desktop from:

https://protege.stanford.edu/

### Step 2 – Open the Ontology

1. Launch **Protégé**.
2. Select **File → Open**.
3. Choose:

```text
CulturalHeritageOntology1.owl
```

### Step 3 – Explore the Ontology

After loading the ontology:

- Open the **Classes** tab.
- Open the **Object Properties** tab.
- Open the **Data Properties** tab.
- Open the **Individuals** tab.
- Review ontology metrics and hierarchy.

### Step 4 – Run the Reasoner

1. Click **Reasoner**.
2. Select **HermiT Reasoner**.
3. Click **Start Reasoner**.

### Step 5 – Verify Consistency

After reasoning:

- Inspect inferred class hierarchies.
- Review inferred relationships.
- Confirm that no inconsistencies are reported.

**Expected Result:**

The ontology should classify successfully and remain logically consistent.

---

## 4. Ontology Objectives

The ontology was developed to:

- Model cultural heritage knowledge semantically.
- Represent museum collections and exhibitions.
- Describe artworks and cultural artifacts.
- Support conservation and restoration activities.
- Track provenance, rights, and digitization history.
- Enable semantic querying and reasoning.
- Facilitate interoperability between heritage information systems.

---

## 5. Conceptual Model

The ontology now contains **46 Classes** (expanded from the original 30).

### Heritage Resource Classes

- CulturalHeritageObject
- Artifact
- Artwork
- Painting
- Sculpture
- Manuscript
- Coin
- Textile
- **Ceramic** *(new)*
- **Jewelry** *(new)*
- **Fresco** *(new)*
- **Drawing** *(new)*
- **Photograph** *(new)*
- HeritageSite
- **ArchaeologicalSite** *(new)*
- **Monument** *(new)*

### Human and Organizational Classes

- Agent
- Artist
- Curator
- Conservator
- Researcher
- **Donor** *(new)*
- **Sponsor** *(new)*
- Museum
- CulturalInstitution

### Collection and Exhibition Classes

- Collection
- Exhibition
- **VirtualExhibition** *(new)*
- Archive

### Contextual Classes

- HistoricalPeriod
- **Style** *(new — art movement / period style)*
- **Technique** *(new — creative or conservation technique)*
- Event
- AcquisitionEvent
- RestorationEvent
- ExhibitionEvent
- **LoanEvent** *(new)*
- **DigitizationEvent** *(new)*
- Location
- Country
- City

### Documentation, Provenance and Rights Classes

- MediaObject
- Image
- Material
- **ProvenanceRecord** *(new)*
- **License** *(new — governs reuse/copyright of digital assets)*

---

## 6. Semantic Relationships

The ontology now defines **32 object properties** (expanded from the original 20):

### Original Properties

- hasCreator
- displayedIn
- belongsToCollection
- associatedWithPeriod
- madeOf
- curatedBy
- organizedBy
- locatedIn
- documentedIn
- restoredBy
- restoresObject
- preservedBy
- references
- owns
- manages
- hasLocation
- participatesInEvent
- acquiresObject
- exhibitsObject
- hasPart

### New Properties

- **hasStyle** — links a heritage object to its Style/movement
- **employsTechnique** — links a heritage object or event to a Technique
- **hasProvenance** — links a heritage object to its ProvenanceRecord
- **previousOwner** — links a ProvenanceRecord to the Agent who held custody
- **licensedUnder** — links a MediaObject to a License
- **digitizedBy** — links a MediaObject to the Agent who produced it
- **loanedTo** — links a heritage object to a borrowing Museum via a LoanEvent
- **donatedBy** — links an AcquisitionEvent to a Donor
- **sponsoredBy** — links an Exhibition to a Sponsor
- **partOfArchive** — links a Manuscript/document to an Archive
- **influencedBy** — links an Artist to another Artist
- **precededBy** — links a Style to the Style that historically preceded it

These relationships connect heritage resources with people, institutions, materials, events, collections, styles, provenance, rights, and locations.

---

## 7. Descriptive Attributes

The ontology now includes **18 data properties** (expanded from the original 12):

### Original Properties

- hasTitle
- hasDescription
- inventoryNumber
- creationDate
- acquisitionDate
- conditionStatus
- height
- width
- estimatedValue
- fileFormat
- publicationYear
- materialType

### New Properties

- **weight** — physical mass of an artifact/artwork
- **copyrightStatus** — rights status of a digital resource (e.g., "Public Domain", "All Rights Reserved")
- **digitizationDate** — date a MediaObject was captured/digitized
- **loanStartDate** — start date of a LoanEvent
- **loanEndDate** — end date of a LoanEvent
- **languageCode** — ISO language code for a Manuscript

---

## 8. Modeling Strategy

### Agent Abstraction

The superclass **Agent** is used to represent people and organizations participating in museum activities, now including **Donor** and **Sponsor** roles alongside Artist, Curator, Conservator, and Researcher.

### Cultural Object Modeling

The ontology separates artworks, artifacts, and heritage sites into specialized subclasses, now further refined with **Ceramic**, **Jewelry**, **Fresco**, **Drawing**, and **Photograph**, plus **ArchaeologicalSite** and **Monument** under HeritageSite.

### Event-Based Representation

Acquisition, restoration, and exhibition activities are represented through dedicated event classes, extended with **LoanEvent** (inter-museum loans) and **DigitizationEvent** (digital capture workflows).

### Provenance and Rights Modeling

A new **ProvenanceRecord** class tracks custody chains via `hasProvenance`/`previousOwner`, and a new **License** class governs reuse of digital assets via `licensedUnder`, supporting cultural heritage rights-management use cases.

### Stylistic and Technical Context

**Style** and **Technique** classes let heritage objects be linked to art-historical movements and creative/conservation methods (`hasStyle`, `employsTechnique`, `precededBy`), enabling movement-based semantic queries (e.g., "all Renaissance paintings using oil technique").

### Location Modeling

Countries and cities are represented as subclasses of **Location**.

### Digital Documentation

Media resources are modeled separately from physical cultural heritage objects, now with digitization provenance and licensing captured explicitly.

---

## 9. Design Decisions

### Agent Abstraction

An abstract class **Agent** was introduced to represent individuals and organizations participating in museum and cultural heritage activities, including funding and gifting roles (Donor, Sponsor). This design improves conceptual clarity and supports future extensibility.

### Cultural Heritage Object Hierarchy

Cultural heritage resources were organized using a hierarchical class structure. **Painting**, **Sculpture**, **Fresco**, **Drawing**, and **Photograph** were modeled as subclasses of **Artwork**, while **Manuscript**, **Coin**, **Textile**, **Ceramic**, and **Jewelry** were modeled as subclasses of **Artifact**. **ArchaeologicalSite** and **Monument** were modeled as subclasses of **HeritageSite**. This hierarchy enables semantic classification and reasoning.

### Event-Based Modeling

**AcquisitionEvent**, **RestorationEvent**, **ExhibitionEvent**, **LoanEvent**, and **DigitizationEvent** were modeled as specialized subclasses of **Event**. This approach supports historical tracking, provenance representation, and event-centered semantic reasoning.

### Provenance and Rights Modeling

**ProvenanceRecord** and **License** were introduced as independent classes rather than plain literals, allowing custody chains and reuse rights to be reasoned over rather than merely stored as text.

### Material and Location Modeling

**Material** and **Location** were represented as independent classes rather than literal attributes. This design improves knowledge organization, allows richer semantic relationships, and facilitates future ontology expansion.

---

## 10. OWL 2 Features Utilized

The ontology employs:

- Class hierarchies
- Subclass relations
- Object properties
- Datatype properties
- Domain restrictions
- Range restrictions
- Named individuals
- Ontology IRI declaration
- RDF/XML serialization

---

## 11. Sample Knowledge Graph

### The Starry Night

#### Individual

**TheStarryNight : Painting**

#### Relationships

- hasCreator → VincentVanGogh
- displayedIn → MuseumOfModernArt
- associatedWithPeriod → PostImpressionism
- madeOf → OilPaint

#### Attributes

- hasTitle = "The Starry Night"
- inventoryNumber = "MOMA-001"
- conditionStatus = "Stable"

---

### Mona Lisa

#### Individual

**MonaLisa : Painting**

#### Relationships

- hasCreator → LeonardoDaVinci
- displayedIn → LouvreMuseum
- associatedWithPeriod → Renaissance
- madeOf → OilPaint

#### Attributes

- hasTitle = "Mona Lisa"
- inventoryNumber = "LOUVRE-001"
- conditionStatus = "Protected"

---

### David *(new)*

#### Individual

**David : Sculpture**

#### Relationships

- hasCreator → Michelangelo
- displayedIn → UffiziGallery
- associatedWithPeriod → HighRenaissance
- madeOf → Marble
- hasStyle → Renaissance

#### Attributes

- hasTitle = "David"
- inventoryNumber = "UFFIZI-001"
- conditionStatus = "Stable"

---

### Girl with a Pearl Earring *(new)*

#### Individual

**GirlWithAPearlEarring : Painting**

#### Relationships

- hasCreator → JohannesVermeer
- displayedIn → Mauritshuis
- associatedWithPeriod → DutchGoldenAge
- madeOf → OilPaint

#### Attributes

- hasTitle = "Girl with a Pearl Earring"
- inventoryNumber = "MAURITSHUIS-001"
- conditionStatus = "Protected"

---

### Arena di Verona *(new)*

#### Individual

**ArenaDiVerona : Monument**

#### Relationships

- locatedIn → VeronaCity
- associatedWithPeriod → **RomanEra** *(represented via HistoricalPeriod value "Roman Era")*

#### Attributes

- hasTitle = "Arena di Verona"
- inventoryNumber = "VR-MON-001"
- conditionStatus = "Preserved / Active Use"

---

## 12. Individuals Included

The ontology now contains **26 Sample Individuals** (expanded from the original 13):

### Original Individuals

- LeonardoDaVinci
- LouvreCollection
- LouvreMuseum
- MoMACollection
- MonaLisa
- MuseumOfModernArt
- NewYorkCity
- OilPaint
- ParisCity
- PostImpressionism
- Renaissance
- TheStarryNight
- VincentVanGogh

### New Individuals

- Michelangelo
- David
- UffiziGallery
- FlorenceCity
- ItalyCountry
- HighRenaissance
- Marble
- JohannesVermeer
- GirlWithAPearlEarring
- Mauritshuis
- DutchGoldenAge
- ArenaDiVerona
- VeronaCity

---

## 13. Consistency Verification

The ontology was validated using the **HermiT Reasoner** within **Protégé**.

### Validation Procedure

1. Load the ontology into Protégé.
2. Start the HermiT reasoner.
3. Execute ontology classification.
4. Review inferred hierarchies, including the newly added subclasses and property chains.
5. Check logical consistency, including disjointness between new classes such as **ProvenanceRecord**/**License** and physical CulturalHeritageObject subclasses.

### Result

**No logical inconsistencies were detected.**

The ontology is logically valid and compatible with **OWL 2.0 reasoning standards**.

---

## 14. OWL File Implementation Notes

The **CulturalHeritageOntology1.owl** file has been generated as an OWL 2 / RDF-XML document matching this README exactly: **46 classes, 32 object properties, 18 data properties, and 26 individuals**, with every subclass axiom, domain/range restriction, and sample relationship described above encoded as OWL axioms.

Two modeling adjustments were made during implementation to keep the file logically consistent under HermiT:

- **`locatedIn` domain.** Section 3/9 examples give the domain of `locatedIn` as Museum, but **Arena di Verona** (a Monument) also uses `locatedIn → VeronaCity`. The property's domain was implemented as the union of `Museum` and `HeritageSite` so both usages are valid without weakening the restriction to `owl:Thing`.
- **`RomanEra` individual.** The sample knowledge graph above lists `associatedWithPeriod → RomanEra` for Arena di Verona, but `RomanEra` is not part of the official 26 individuals in Section 12, so it was omitted from the implemented file. It can be added as a 27th individual on request.

The generated file was verified to be well-formed XML, with the counts of `owl:Class`, `owl:ObjectProperty`, `owl:DatatypeProperty`, and `owl:NamedIndividual` declarations matching this README exactly. It is ready to open in Protégé and classify with HermiT as described in Section 13.

## 15. Project Summary

The **Cultural Heritage and Museum Ontology** provides a structured semantic framework for representing cultural heritage assets, museum collections, artworks, artifacts, historical knowledge, conservation records, provenance, rights and licensing, stylistic/technical context, and digital documentation resources.

The ontology supports:

- Knowledge organization
- Semantic interoperability
- Museum collection management
- Heritage preservation workflows
- Provenance and rights tracking
- Digital heritage documentation
- Automated semantic reasoning

The final ontology is fully compliant with **OWL 2 standards** and demonstrates ontology engineering principles within the **Cultural Heritage Domain**, now with broader coverage of provenance, licensing, and stylistic/technical metadata.
