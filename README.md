## kubernetes_marketplus
The purpose of this repo is to decouple the frontend and backend functions of the Marketplus dapp [(see here)](https://github.com/snpsuen/Marketplus) into separate Kubernetes microservices. More specifcally, a backend K8s pod is dedicated to running the local Ganache blockchain to serve the smart contract at work. Menawhile, the webapp frontend is implemented by another K8s pod, which also provide a development environment for compiling and deploying the smart contract to the ganache pod.

