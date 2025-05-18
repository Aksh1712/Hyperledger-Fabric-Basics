# Hyperledger Fabric Basics

This repository provides a beginner-friendly guide to set up Hyperledger Fabric, deploy a basic network, and run a simple chaincode (smart contract) for a permissioned blockchain. It’s designed for developers exploring enterprise blockchain solutions.

## Prerequisites
- **OS**: Linux (Ubuntu 20.04+ recommended) or MacOS
- **Tools**: Docker, Docker Compose, Git, Go (1.18+), Node.js (16+), curl
- **Hardware**: 4GB RAM minimum, 8GB recommended
- **Internet**: Required for downloading binaries and images

## Installation
1. Clone this repository:
```bash
git clone https://github.com/username/Hyperledger-Fabric-Basics.git
cd Hyperledger-Fabric-Basics
```

2. Run the installation script:
```bash
chmod +x install_fabric.sh
./install_fabric.sh
```

3. Start the test network and deploy the chaincode:
```bash
cd fabric-samples/test-network
./network.sh up
./network.sh createChannel
cd ../../chaincode
./deploy_chaincode.sh
```

## Usage
1. Interact with the chaincode (example: asset transfer):
```bash
# Set environment variables for peer
export PATH=${PWD}/../bin:$PATH
export FABRIC_CFG_PATH=${PWD}/../config/

# Invoke chaincode to create an asset
peer chaincode invoke -o localhost:7050 --ordererTLSHostnameOverride orderer.example.com --tls --cafile "${PWD}/organizations/ordererOrganizations/example.com/orderers/orderer.example.com/msp/tlscacerts/tlsca.example.com-cert.pem" -C mychannel -n basic --peerAddresses localhost:7051 --tlsRootCertFiles "${PWD}/organizations/peerOrganizations/org1.example.com/peers/peer0.org1.example.com/tls/ca.crt" --peerAddresses localhost:9051 --tlsRootCertFiles "${PWD}/organizations/peerOrganizations/org2.example.com/peers/peer0.org2.example.com/tls/ca.crt" -c '{"function":"CreateAsset","Args":["asset1","blue","10","Alice","1000"]}'
```

2. Query the chaincode:
```bash
peer chaincode query -C mychannel -n basic -c '{"Args":["ReadAsset","asset1"]}'
```

3. Shut down the network:
```bash
cd fabric-samples/test-network
./network.sh down
```

## Repository Structure
- `install_fabric.sh`: Script to install Fabric binaries and samples
- `chaincode/`: Contains a basic Go chaincode for asset transfer
- `deploy_chaincode.sh`: Script to package and deploy the chaincode
- `.gitignore`: Comprehensive ignore patterns for Fabric projects
- `LICENSE`: MIT License

## Contributing
1. Fork the repository
2. Create a feature branch (`git checkout -b feature/xyz`)
3. Commit changes (`git commit -m "Add feature xyz"`)
4. Push to the branch (`git push origin feature/xyz`)
5. Create a Pull Request

## Resources
- [Hyperledger Fabric Documentation](https://hyperledger-fabric.readthedocs.io/)
- [Fabric Samples](https://github.com/hyperledger/fabric-samples)

## License
MIT License