# Healthcare Clinical Ontology

A formal OWL 2 DL ontology of the clinical healthcare domain, developed in Protégé as part of the Knowledge Representation course at the University of Verona, Computer Science Department.

---

## Domain

The ontology models the core entities and relationships of a clinical healthcare setting, including:

- Medical personnel (doctors, nurses)
- Patients and their conditions
- Treatments (pharmacological and surgical)
- Drugs
- Medical facilities (hospitals, clinics)

---

## File

| File | Description |
|------|-------------|
| `HealthcareOntology.owl` | OWL 2 DL ontology in RDF/XML format |

---

## How to Open

1. Download and install [Protégé 5.x](https://protege.stanford.edu/)
2. Open Protégé → File → Open → select `HealthcareOntology.owl`
3. Go to **Reasoner → HermiT → Start reasoner**
4. Inspect the inferred class hierarchy in the Classes tab

Alternatively, upload the file to [WebProtégé](https://webprotege.stanford.edu/) to open it directly in the browser without installation.

---

## Ontology Structure

### T-Box — Classes

| Class | Type | Description |
|-------|------|-------------|
| `HealthEntity` | Primitive | Top-level concept |
| `Person` | Primitive | A person in the domain |
| `Patient` | Defined | A Person with at least one Condition |
| `MedicalStaff` | Primitive | A Person who works at a facility |
| `Doctor` | Defined | A MedicalStaff who treats at least one Patient |
| `Nurse` | Defined | A MedicalStaff who assists only Doctors |
| `Condition` | Primitive | A medical condition |
| `AcuteCondition` | Primitive | A sudden-onset condition |
| `ChronicCondition` | Primitive | A long-term condition |
| `Treatment` | Primitive | A medical treatment |
| `PharmacologicalTreatment` | Defined | A Treatment using a Drug |
| `SurgicalTreatment` | Defined | A Treatment performed by a Doctor |
| `Drug` | Primitive | A pharmaceutical drug |
| `MedicalFacility` | Primitive | A medical facility |
| `Hospital` | Primitive | A full hospital |
| `Clinic` | Primitive | An outpatient clinic |
| `EmergencyPatient` | Defined | A Patient with at least one AcuteCondition |
| `ChronicCarePatient` | Defined | A Patient with at least one ChronicCondition |
| `InpatientDoctor` | Defined | A Doctor treating ≥3 Patients at a Hospital |
| `UnassignedPatient` | Defined | A Patient with no assigned Doctor |
| `AcuteOrChronicPatient` | Defined | A Patient with an acute or chronic condition |
| `NonMedicalPerson` | Defined | A Person who is not MedicalStaff |
| `SpecialistDoctor` | Defined | A Doctor who treats ChronicCarePatients |

### R-Box — Object Properties

| Property | Characteristics | Domain → Range |
|----------|----------------|----------------|
| `treats` | — | Doctor → Patient |
| `isTreatedBy` | Inverse of `treats` | Patient → Doctor |
| `hasCondition` | — | Patient → Condition |
| `worksAt` | Functional | MedicalStaff → MedicalFacility |
| `assists` | — | Nurse → Doctor |
| `assistsInTreatment` | Role chain: `assists ∘ treats` | — |
| `performedBy` | — | SurgicalTreatment → Doctor |
| `usesDrug` | Functional | PharmacologicalTreatment → Drug |
| `refersTo` | Functional | — |
| `isRelatedTo` | Symmetric | — |
| `isPartOf` | Transitive | — |

### A-Box — Individuals

| Individual | Type |
|------------|------|
| `drRossi` | Doctor |
| `drBianchi` | Doctor |
| `nurseConti` | Nurse |
| `marioB` | Patient |
| `luciaF` | Patient |
| `giovanniM` | Patient |
| `annaN` | Patient |
| `appendicitis` | AcuteCondition |
| `fracture` | AcuteCondition |
| `hypertension` | ChronicCondition |
| `diabetes` | ChronicCondition |
| `tx01` | PharmacologicalTreatment |
| `surgery01` | SurgicalTreatment |
| `amoxicillin` | Drug |
| `veronaCivile` | Hospital |
| `clinicaSud` | Clinic |

---

## Automatic Inferences

When the HermiT reasoner is started, the following classifications are inferred automatically:

| Individual | Inferred class |
|------------|---------------|
| `marioB` | `EmergencyPatient` (has appendicitis, an AcuteCondition) |
| `giovanniM` | `EmergencyPatient` (has fracture, an AcuteCondition) |
| `luciaF` | `ChronicCarePatient` (has hypertension, a ChronicCondition) |
| `annaN` | `ChronicCarePatient` (has diabetes, a ChronicCondition) |
| `drRossi` | `InpatientDoctor` (treats 3 patients, works at a Hospital) |
| `drBianchi` | `SpecialistDoctor` (treats annaN, a ChronicCarePatient) |

---

## OWL 2 DL Constructs Used

- Class inclusion axioms (`SubClassOf`)
- Class equivalence axioms (`EquivalentClasses`)
- Intersection (`ObjectIntersectionOf`)
- Union (`ObjectUnionOf`)
- Complement (`ObjectComplementOf`)
- Existential restriction (`ObjectSomeValuesFrom`)
- Universal restriction (`ObjectAllValuesFrom`)
- Qualified minimum cardinality (`ObjectMinCardinality`)
- Qualified maximum cardinality (`ObjectMaxCardinality`)
- Inverse object properties (`InverseObjectProperties`)
- Functional object property (`FunctionalObjectProperty`)
- Transitive object property (`TransitiveObjectProperty`)
- Symmetric object property (`SymmetricObjectProperty`)
- Role chain axiom (`SubObjectPropertyOf` with chain)
- Disjoint classes (`DisjointClasses`)
- Named individuals with concept and role assertions

---

## Course

Knowledge Representation — University of Verona, Computer Science Department
