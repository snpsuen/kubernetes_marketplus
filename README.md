## kubernetes_marketplus
The purpose of this repo is to decouple the frontend and backend functions of the Marketplus dapp [(see here)](https://github.com/snpsuen/Marketplus) into separate Kubernetes microservices. More specifcally, a backend K8s pod is dedicated to running the local Ganache blockchain to serve the smart contract at work. Meanwhile, the webapp frontend is implemented by another K8s pod to invoke the smart contract remotely on the Ganache pod. It also provide a development environment for compiling and deploying the smart contract to Ganache.

### Demarcation of workloads between decoupled pods
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
			<pre>npm run start<br>Truffle compile<br>Truffle migrate</pre>
			</td>
		</tr>
		<tr>
			<td>ganache</td>
			<td aligh="left">Ganache blockchain</td>
			<td aligh="left"><pre>ganache -h 0.0.0.0</pre></td>
		</tr>
	</tbody>
</table>


