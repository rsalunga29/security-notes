Zeek has two primary layers; "Event Engine" and "Policy Script Interpreter".
![[zeek-architecture.png]]
## Event Engine
The Event Engine layer is where the packets are processed. It is responsible for describing the events and where packages are divided into parts such as source and destination addresses, protocol identification, session analysis and file extraction.
## Policy Script Interpreter
This layer is where semantic analysis is conducted. It is responsible for describing the event correlations by using Zeek scripts.