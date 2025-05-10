> building a product from requirements is system design 

### Set of requirements
* decide architecture (database, cdn, api's)
* decide components (auth = > (webserver, db, cache))
* decide modules (auth)

> system design is about how these modules, architecture and components will come together, interact with each other and build a complete solution, a functional solution ~~ Product Development 

## How to approach System Design?
* understand the problem statement
* break it down into components
    ex: Designing facebook : Auth, Notification, Feed, Gamification
* Split into features
    for ex Feed: Webserver, DB <= Generator, Aggregator
* For each sub-component look into
    * DB and Caching
    * Scaling and Fault Tolerance
    * Async processing (Delegation)
    * Communication (repeat all those points for each component)
* split components into sub-components if required

## Evaluate a System
1. You have broken your system into components
2. Every component has a clear set of responsibilities
    * feed webserver - server feed over http
    * feed generator - pulls data from multiple services and puts them in DB (candidate feed items)
    * Feed Aggregator - filters data and creates a final consumable feed
3. For each component, you've slight technical details figured out
    * DB and Caching
    * Scaling and Fault Tolerance
    * Async processing (Delegation)
    * Communication (repeat all those points for each component)
4. Each component (in isolation)
    * fault tolerant - plan for recovery in case of a failure
    * scalable
    * available - solve for complete outage