## Dapp Segmentation Into Kubernetes Pods
The purpose of this repo is to decouple the frontend and backend functions of the Marketplus dapp [(see here)](https://github.com/snpsuen/Marketplus) into separate Kubernetes microservices. 

More specifcally, a backend K8s pod is dedicated to running the local Ganache blockchain to serve the smart contract at work. Meanwhile, the webapp frontend is implemented by another K8s pod to invoke the smart contract remotely on the Ganache pod. It also provides a development environment for compiling and deploying the smart contract to Ganache.

### Workload demarcation between decoupled pods
<table>
	<thead>
		<tr>
			<th scope="col">K8s Pod</th>
			<th scope="col">Workload</th>
			<th scope="col">Process/Command</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td>marketfront</td>
			<td aligh="left">ReactJS Webapp <br> Truffle Development</td>
			<td aligh="left">
			<pre>npm run start<br>truffle compile<br>truffle migrate</pre>
			</td>
		</tr>
		<tr>
			<td>ganache</td>
			<td aligh="left">Ganache blockchain</td>
			<td aligh="left"><pre>ganache -h 0.0.0.0</pre></td>
		</tr>
	</tbody>
</table>

Here are the steps to take in a nutshell in order to deploy the Marketplus dapp in a Kubernetes cluster.

### 0. Prerequisites

In our example, a Kind Kubernetes cluster is set up on an Ubuntu Virtualbox VM hosted in a Windows laptop. The VM is assigned a static IP 10.0.2.55 on a NAT network.

Both the webapp and Ganache pods are exposed as K8s services and handled by a MetalLB load balancer via the VIPs 172.18.0.10 and 172.18.0.11 respectively. the following SSH tunneling rules are added to the putty terminal of the VM to redirect the webapp traffic (port 3000) and Ganache traffic (port 8545) from the local host (10.0.2.55) to the corresponding VIPs.
* L3000 ---> 172.18.0.10:3000
* L8545 ---> 172.18.0.11:8545

the following port forwarding rules are added to Virtualbox to redirect the webapp traffic (port 3000) and Ganache traffic (port 8545) from the local desktop to the VM (10.0.2.55).
* Host port:3000 ---> 10.0.2.55:3000
* Nost port:8545 ---> 10.0.2.55:8545





