এটা কোনো TODO list হবে না। এটা হবে Architectural Change Log।

Structure হবে এরকম:

Refactor ID: REF-0001

Status:
Proposed | Approved | Implemented | Rejected

Affected Documents:
- 02-project-scope.md
- 04-core-domain-model.md

Reason:
কেন পরিবর্তন প্রয়োজন?

Current Design:
বর্তমান design কী?

Proposed Design:
নতুন design কী?

Impact:
- Database
- API
- Code
- UI
- Documentation

Migration Strategy:
কীভাবে change apply হবে?

Decision Date:

Implemented Version:

Documentation Hierarchy

এখন থেকে আমি documentation-কে এই hierarchy-তে organize করতে চাই।

docs/

├── constitution/
│   ├── 00-project-principles.md
│   ├── 01-project-vision.md
│   ├── 02-project-goals.md
│   ├── 03-platform-architecture-principles.md
│   ├── 04-core-domain-model.md
│   └── 05-ubiquitous-language.md
│
├── architecture/
│   ├── 00-refactor-log.md
│   ├── 01-adr/
│   ├── 02-rfc/
│   ├── 03-diagrams/
│   └── 04-decisions/
│
├── design/
│
├── database/
│
├── api/
│
├── agents/
│
├── workflows/
│
└── deployment/

এভাবে Constitution, Design, Architecture Decisions এবং বাস্তব Implementation Specification আলাদা থাকবে।

