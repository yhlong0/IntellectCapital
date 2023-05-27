# Graph Database

1. Relationships are first-class citizens of the graph data model. 
2. Relational db, where join intensive query performance deteriorates as the dataset gets bigger, with a graph database performance tends to remain relatively constant, even as the dataset grows. This is because queries are localized to a portion of the graph, you start with one or multiple nodes and traversed to satisfy that query, the "hops" define your execution time rather than the size of the overall graph.
3. "What products did a customer buy" is relatively cheap compared to "Which customers bought this product?", "Which customers buying this product also bought that product" quickly become prohibitively expensive as the degree of recursion increases. 
4. To figure out which system down(app, vm, server, db, load balancer) causing user not able to use the system. `MATCH (user:User)-[*1..5]-(asset:Asset) WHERE user.name = 'User 3' AND asset.status = 'down'` This will cover a lot of relationships, user->app, user->app->db, user->app->vm->server and etc.
5. MERGE, ensuring that if some of which already exist, avoid duplication. 
6. Labels are first class citizens of the property graph model, we can index nodes with a User label, or add constrain all nodes with a customer label have a unique email property value. 
7. 
