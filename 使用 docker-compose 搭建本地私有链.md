



## 使用 docker-compose 启动容器

### 第一步：下载仓库，进入项目目录，启动容器

git clone https://github.com/chunqizhi/go-ethereum.git

cd chaojigongshi-miners

docker-compose up -d

### 第二步：进入 myEthNode 容器，启动挖矿

docker exec -it myEthNode /bin/sh

geth attach ~/data/geth.ipc

miner.start(1)

admin.nodeInfo.enode

eth.sendTransaction({from:eth.accounts[0],to:eth.accounts[1],value:1000000000000000000})

docker logs -f myEthNode

### 第三步：进入其他容器，连接 myEthNode 容器节点

#### 操作 myEthOtherNode 容器

docker exec -it myEthOtherNode /bin/sh

geth attach ~/data/geth.ipc

admin.addPeer("enode://093e51559d86166edb07f3bb815367bb51898ad61d93d37752fe5f3324f9299d7fb02906b6de66dcfe97cba1d8ca02a30310abf77baf1d121beb6cc09ec59028@myEthNode:30303")

personal.newAccount()

123456

miner.start(2)

docker logs -f myEthOtherNode 

#### 操作 myBtcpoolOtherNode 容器

docker exec -it myBtcpoolOtherNode /bin/sh

geth attach ~/data/geth.ipc

admin.addPeer("enode://093e51559d86166edb07f3bb815367bb51898ad61d93d37752fe5f3324f9299d7fb02906b6de66dcfe97cba1d8ca02a30310abf77baf1d121beb6cc09ec59028@myEthNode:30303")

personal.newAccount()

123456

miner.start(2)

### 其他节点以容器方式加入联盟链

docker run -d --network chaojigongshi-miners_ethnet --name joinEthNode zfq17876911936/chaojigongshi-ethereum-client-go:eth-1.0

docker exec -it joinEthNode  /bin/sh

geth attach geth.ipc

admin.addPeer("enode://093e51559d86166edb07f3bb815367bb51898ad61d93d37752fe5f3324f9299d7fb02906b6de66dcfe97cba1d8ca02a30310abf77baf1d121beb6cc09ec59028@myEthNode:30303")

## 其他节点以进程方式加入联盟链，以来持久化数据

cd otherMiner

cat REEADME.md

admin.addPeer("enode://093e51559d86166edb07f3bb815367bb51898ad61d93d37752fe5f3324f9299d7fb02906b6de66dcfe97cba1d8ca02a30310abf77baf1d121beb6cc09ec59028@127.0.0.1:30303")
