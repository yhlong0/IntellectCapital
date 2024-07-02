# Docker Deep Dive

1. Low to high: Runtime[runc(short live, start the container), contained(long-running process,pulling images, managing runc instances, life cycle management)] -> Engine/daemon[CLI, API, image mgt, Networking, Volumes] -> Orchestration(swarm, manages clusters)
2. 
