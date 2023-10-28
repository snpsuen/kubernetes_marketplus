## kubernetes_marketplus
The purpose of this repo is to decouple the frontend and backend functions of the Marketplus dapp [(see here)](https://github.com/snpsuen/Marketplus) into separate Kubernetes microservices. More specifcally, a backend K8s pod is dedicated to running the local Ganache blockchain to serve the smart contract at work. Meanwhile, the webapp frontend is implemented by another K8s pod to invoke the smart contract remotely on the Ganache pod. It also provide a development environment for compiling and deploying the smart contract to Ganache.

### Demarcation of workloads between decoupled pods

| K8s pod       | Type          | Process/command     |
| ------------- |:-------------:| -------------------:|
| marketfront   | right-aligned | npm run start       |
|               |               | truffle compile     |
|               |               | truffle migrate     |
| ganache       | centered      | ganache -h 0.0.0.0  |


