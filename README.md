# NP-Guard Demo

### 1) Connectivity visualization before adding network policies
Clone the microservices demo repo, install and run network-config-analyzer (https://github.com/np-guard/network-config-analyzer). \
Make sure you have Python 3.8 or above on your platform.

```
cd $HOME
git clone git@github.com:GoogleCloudPlatform/microservices-demo.git
pip install network-config-analyzer
nca --connectivity -r $HOME/microservices-demo/release/ 
```

Consider various formats of connectivity reports:

```commandline
nca --connectivity -r $HOME/microservices-demo/release/ -o dot -f demo-connectivity-1.dot
```

```commandline
nca --connectivity -r $HOME/microservices-demo/release/ -o csv -f demo-connectivity-1.csv
```

```commandline
nca --connectivity -r $HOME/microservices-demo/release/ -o md -f demo-connectivity-1.md
```

```commandline
nca --connectivity -r $HOME/microservices-demo/release/ -o txt -f demo-connectivity-1.txt
```
Check the [connectivity report files](analysis_before_netpols_added).

### 2) Synthesis of network policies
Build and run cluster topology analyzer (https://github.com/np-guard/cluster-topology-analyzer). \
Make sure you have golang 1.13+ on your platform.


```
git clone git@github.com:np-guard/cluster-topology-analyzer.git
cd cluster-topology-analyzer
go mod download
make

$HOME/cluster-topology-analyzer/bin/net-top -dirpath $HOME/microservices-demo -commitid c04cf77a7550d932821f5a5c5c6936ab02402fea -giturl https://github.com/GoogleCloudPlatform/microservices-demo -gitbranch main -netpols -outputfile $HOME/microservices-demo/release/netpols.yaml 
```
Check the [synthesized network policies yaml file](synthesis/netpols.yaml).
### 3) Connectivity visualization after adding network policies

```commandline
nca --connectivity -r $HOME/microservices-demo/release/ 
```
Check the [connectivity report files](analysis_after_netpols_added).




