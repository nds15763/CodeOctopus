# Node Design Document

## Core Concepts

### Node Base

A Node is a fundamental unit in the MCP system that processes and manages specific types of content (code, documents, etc.). Each node type inherits from the base node implementation and includes three essential components:

1. **VectorDB Component**
   - Purpose: Deep content storage and similarity search
   - Function: Stores detailed information and enables semantic search
   - Key Features:
     - Content vectorization
     - Semantic similarity search
     - Relevance ranking
     - Linked to Memory Graph nodes via unique IDs

2. **Memory Graph Component**
   - Purpose: Knowledge relationship management
   - Function: Maintains high-level understanding and relationships
   - Key Features:
     - Core concept storage
     - Relationship mapping
     - Quick navigation
     - Bi-directional links with VectorDB entries

3. **Cursor Component**
   - Purpose: Content location and navigation
   - Function: Provides precise positioning within files
   - Key Features:
     - Position tracking
     - Content boundary marking
     - Change monitoring
     - Quick jumps

## Node Types

### Project Node

Manages project-level information and coordinates between different nodes.

- **VectorDB Usage**
  - Project configurations
  - Build specifications
  - Dependency information
  - Project-wide settings

- **Memory Graph Usage**
  - Project structure
  - Module relationships
  - Component dependencies
  - Architecture overview

- **Multi Doc Cursor Usage**
  - Cross-file navigation
  - Project-wide locating
  - Multi-file coordination
  - Change tracking across files

### Code Node

Handles code-related content and structure.

- **VectorDB Usage**
  - Function implementations
  - Class definitions
  - API specifications
  - Code comments and documentation

- **Memory Graph Usage**
  - Code architecture
  - Function relationships
  - Call hierarchies
  - Module interfaces

- **Doc Cursor Usage**
  - Code block positioning
  - Function navigation
  - Definition location
  - Reference tracking

### Design Node

Manages design documents and their relationships.

- **VectorDB Usage**
  - Detailed design specifications
  - Architecture decisions
  - Component designs
  - Interface definitions

- **Memory Graph Usage**
  - Design patterns
  - System architecture
  - Component relationships
  - Design principles

- **Code Cursor Usage**
  - Design-code mapping
  - Implementation tracking
  - Specification location
  - Change impact analysis

## Data Relationships

### Inter-Node Communication

```
[Project Node] ←→ [Code Node]
       ↕            ↕
[Design Node] ←→ [Doc Node]
```

### Data Flow

1. Memory Graph provides high-level navigation
2. VectorDB enables detailed content search
3. Cursor facilitates precise positioning

## Implementation Guidelines

### Data Consistency

- **Unique Identifiers**
  - Each node has a unique ID
  - All components within a node share reference IDs
  - Cross-node references use consistent ID system

- **Change Propagation**
  - File changes trigger Cursor updates
  - Cursor updates notify VectorDB
  - VectorDB changes reflect in Memory Graph

### Search Process

1. **Top-down Search**
   - Start from Memory Graph concepts
   - Follow relationships to VectorDB details
   - Use Cursor for precise location

2. **Bottom-up Search**
   - Begin with VectorDB content search
   - Link to Memory Graph for context
   - Navigate related concepts

### Extension Points

- **New Node Types**
  - Inherit from Node Base
  - Implement required components
  - Define specialized behaviors

- **Custom Components**
  - Extend base components
  - Maintain core interfaces
  - Add specialized features

## Usage Examples

### Code Understanding

1. User queries about a feature
2. Memory Graph identifies relevant modules
3. VectorDB provides implementation details
4. Cursor locates exact code position

### Design Evolution

1. Design changes in documents
2. Memory Graph updates relationships
3. VectorDB stores new specifications
4. Cursor tracks impacted code areas

## Best Practices

1. **Memory Graph Management**
   - Keep concepts atomic
   - Maintain clear relationships
   - Regular graph optimization

2. **VectorDB Organization**
   - Proper content segmentation
   - Regular vector updates
   - Efficient index maintenance

3. **Cursor Implementation**
   - Real-time position tracking
   - Efficient boundary marking
   - Robust change detection