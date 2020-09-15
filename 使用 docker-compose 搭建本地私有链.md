## 使用 docker-compose 启动容器

### 第一步：下载仓库，进入项目目录，启动容器

git clone https://github.com/chunqizhi/chaojigongshi-miners.git

cat README.md

### 第二步：进入 myEthNode 容器，启动挖矿

docker exec -it myEthNode bash

geth attach geth.ipc

miner.start(1)

admin.nodeInfo.enode

eth.sendTransaction({from:eth.accounts[0],to:eth.accounts[1],value:1000000000000000000})

docker logs -f myEthNode

### 第三步：进入其他容器，连接 myEthNode 容器节点

#### 操作 myEthOtherNode 容器

docker exec -it myEthOtherNode bash

geth attach geth.ipc

admin.addPeer("enode://45385c99ac12952ef0a84a7333b5258885a13036767fa381737ad5a1143b4430d36925abee752e8d445e0fe4d0927e1d02cbf03bd2706c8a5927a55b4d5c8559@myEthNode:30303")

personal.newAccount()

123456

miner.start(2)

docker logs -f myEthOtherNode

#### 操作 myBtcpoolOtherNode 容器

docker exec -it myBtcpoolOtherNode bash

geth attach geth.ipc

admin.addPeer("enode://45385c99ac12952ef0a84a7333b5258885a13036767fa381737ad5a1143b4430d36925abee752e8d445e0fe4d0927e1d02cbf03bd2706c8a5927a55b4d5c8559@myEthNode:30303")

personal.newAccount()

123456

miner.start(2)

### 其他节点以容器方式加入联盟链

docker run -d --network chaojigongshi-miners_ethnet --name joinEthNode zfq17876911936/chaojigongshi-ethereum-client-go:eth-miningPool-1.0

docker exec -it joinEthNode bash

geth attach geth.ipc

admin.addPeer("enode://45385c99ac12952ef0a84a7333b5258885a13036767fa381737ad5a1143b4430d36925abee752e8d445e0fe4d0927e1d02cbf03bd2706c8a5927a55b4d5c8559@myEthNode:30303")

## 其他节点以进程方式加入联盟链，以来持久化数据

cd backup

cat REEADME.md

admin.addPeer("enode://45385c99ac12952ef0a84a7333b5258885a13036767fa381737ad5a1143b4430d36925abee752e8d445e0fe4d0927e1d02cbf03bd2706c8a5927a55b4d5c8559@127.0.0.1:30301")