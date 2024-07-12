# Inspecting-On-Chain-Functions-Involving-Calls
### Introduction

**Protocol Name:** Centrifuge  
**Category:** RWA Tokenization  
**Smart Contract:** Tinlake Pool  

### Function Analysis

**Function Name:** applyJuniorRatio  
**Block Explorer Link:** [Etherscan - Tinlake Pool](https://etherscan.io/address/0xaFB2f3c7bDb97F3e0ED3A81d52093FfC6c989Eef#code)  
**Function Code:**
```solidity
function applyJuniorRatio(uint256 amount, address user, bytes32 deal) internal {
    bytes32[] memory params = new bytes32[](2);
    params[0] = bytes32(uint256(uint160(user)));
    params[1] = deal;
    triggerSeniorSupplyOrder(
        deal,
        amount,
        abi.encode(address(juniorMemberlist), "triggerEvent(bytes32,bytes32[])"),
        params
    );
}
```
**Used Encoding/Decoding or Call Method:** `abi.encode`

# Explanation
Purpose: The `applyJuniorRatio` function facilitates applying a junior ratio for a user in a Tinlake Pool, part of Centrifuge's RWA tokenization protocol.

Detailed Usage: In this smart contract, `applyJuniorRatio` constructs an array `params` containing the user's address and a deal identifier. It then uses `abi.encode` to encode a function call to `triggerEvent` on the `juniorMemberlist` contract, passing the `params` array as an argument. This encoded data is used as a parameter when triggering a senior supply order (`triggerSeniorSupplyOrder`).

The use of `abi.encode` here allows the smart contract to dynamically encode the parameters for a function call, which is essential for interacting with other contracts in a structured manner. By encoding the parameters (`params`) into a byte array, the function ensures that the data passed to `triggerEvent` is correctly formatted and can be interpreted by the receiving contract (`juniorMemberlist`), maintaining consistency and integrity in data communication.

Impact: The `applyJuniorRatio` function enhances the Tinlake Pool's functionality by enabling the application of junior ratios based on encoded user and deal data. This contributes to the protocol's overall capability to manage and adjust junior participation in financing pools backed by real-world assets. The use of `abi.encode` ensures that interactions between different components of the Centrifuge ecosystem are efficient and secure, leveraging blockchain's transparency and automation benefits in RWA tokenization.
