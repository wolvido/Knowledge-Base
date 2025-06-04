#### Context Driven Feature Sliced Design with Repository
###### Unidirectional Consumption Codebase
![[Pasted image 20250331003047.png]]
###### Based on the Feature Sliced Design Architecture but modified for **higher cohesion** and **lower coupling**
![[Pasted image 20250330164719.png]]
###### How does it achieve higher cohesion?
- By focusing on three main layers; Entities, Features, and Application layer. Removed unnecessary layers.
- By implementing unidirectional consumption/dependencies.
- By using service-contexts, which are context that combine business logic and data state into a logical and cohesive functionality.
	- Service-contexts are segments that can be bound to an entity or feature vertical slice.
###### How does it achieve lower coupling?
- by removing API calls on all the layers and implementing an Infrastructure layer dedicated to the API.
##### Layering, Slicing, and Segmenting
- members of a layer (also called a vertical slice) should not have dependencies on each other.
- slices should only depend on other layers as defined by the architecture. e.g. entities -> features -> application.
- slices contains parts called segments.
##### Segments
- members of a slice contains segments.
- segments are parts of a slice and can have dependencies on each other.
##### Context-Service
- In this architecture "Services" are react context, where business logic is contained within a service-context.
	- Why use context as a service?
	- It encapsulates feature specific business logic and its data states inside a single provider. Easy to trace and prevents unnecessary scattered logic.
		- But what if it becomes unwieldy?
		- As long as your feature scope is reasonable and has a single responsibility, then its context will also remain reasonable.
		- If your context becomes unreasonable, then your feature should be two features.
##### Features and Services
- Features can contain feature bound context-services, which contain feature specific business logic.
#### Shared
[Layers | Feature-Sliced Design](https://feature-sliced.github.io/documentation/docs/reference/layers#shared)