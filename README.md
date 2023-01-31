# Buidl the contract

cargo concordium build --out dist/smart-contract-multi/module.wasm.v1 --schema-out dist/smart-contract-multi/schema.bin

# Deploy the contract

concordium-client module deploy dist/smart-contract-multi/module.wasm.v1 --sender <YOUR-ACCOUNT> --name cis2_multi --grpc-port 10001

# Initialize the contract

concordium-client contract init <MODULE-HASH> --sender <YOUR-ACCOUNT> --energy 30000 --contract cis2-multi --grpc-port 10001

# Mint Semi-Fungible Tokens

concordium-client contract update <YOUR-CONTRACT-INSTANCE> --entrypoint mint --parameter-json nft-artifacts/mint-params.json --schema dist/smart-contract-multi/schema.bin --sender <YOUR-ACCOUNT> --energy 6000 --grpc-port 10001

# View Contract State

concordium-client contract invoke <YOUR-CONTRACT-INSTANCE> --entrypoint view --schema dist/smart-contract-multi/schema.bin --grpc-port 10001

# Check Metadata

concordium-client contract invoke <YOUR-INDEX> --entrypoint tokenMetadata --parameter-json nft-artifacts/ids.json --schema dist/smart-contract-multi/schema.bin --grpc-port 10001

# Transfer

concordium-client contract update <YOUR-INDEX> --entrypoint transfer --parameter-json nft-artifacts/transfer.json --schema dist/smart-contract-multi/schema.bin --sender <YOUR-ACCOUNT> --energy 6000 --grpc-port 10001
