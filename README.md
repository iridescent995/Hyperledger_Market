# Hyperledger_Market
stop and remove running docker container
```
docker stop $(docker ps -aq)
docker rm $(docker ps -aq)
```
run
```
docker-compose -f docker-compose.yml up -d
```

edit 3 files.
create cryptoconfig files.

create channel
```
docker exec -e "CORE_PEER_LOCALMSPID=SellerMSP" -e "CORE_PEER_MSPCONFIGPATH=/opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/peerOrganizations/Seller.market.com/users/Admin@Seller.market.com/msp" cli peer channel create -o orderer.market.com:7050 -c channel -f /etc/hyperledger/configtx/channel.tx
```


join peer to channel
```
docker exec -e "CORE_PEER_LOCALMSPID=SellerMSP" -e "CORE_PEER_MSPCONFIGPATH=/opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/peerOrganizations/Seller.market.com/users/Admin@Seller.market.com/msp" -e "CORE_PEER_ADDRESS=peer0.Seller.market.com:7051" -e "CORE_PEER_ID=cli" cli peer channel join -b channel.block
```

install cc
```
docker exec -e "CORE_PEER_LOCALMSPID=SellerMSP" -e "CORE_PEER_MSPCONFIGPATH=/opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/peerOrganizations/Seller.market.com/users/Admin@Seller.market.com/msp" -e "CORE_PEER_ADDRESS=peer0.Seller.market.com:7051" -e "CORE_PEER_ID=cli" cli peer chaincode install -n market-network -v 1.0 -l golang -p github.com/basic-marketplace-cc/go
```

attach cc to peer and compile it
```
docker exec -e "CORE_PEER_LOCALMSPID=SellerMSP" -e "CORE_PEER_MSPCONFIGPATH=/opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/peerOrganizations/Seller.market.com/users/Admin@Seller.market.com/msp" -e "CORE_PEER_ADDRESS=peer0.Seller.market.com:7051" -e "CORE_PEER_ID=cli" cli peer chaincode install -n market-network -v 1.0 -l golang -p github.com/basic-marketplace-cc/go
```
