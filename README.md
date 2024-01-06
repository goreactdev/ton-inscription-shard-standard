- **title**: Shard Protocol
- **status**: Active
- **type**: Transaction Interface
- **created**: 24.12.2023

# Summary
A standard interface for Item inscription in TON.

## Motivation

The development and adoption of the Item Inscription Standard for the TON blockchain is driven by several key motivations:

1. **Interoperability and Standardization:** In the rapidly evolving world of blockchain and items, the lack of a unified standard for item inscription can lead to fragmentation and inefficiencies. By establishing a common protocol ("Shard"), we aim to facilitate interoperability among different entities and platforms within the TON ecosystem. This standardization will simplify the processes of minting, transferring, and managing digital assets.

2. **Enhanced Security and Reliability:** The standard introduces a robust structure for data handling, particularly focusing on the integrity of transaction hashes and metadata. By enforcing strict guidelines and formats, it reduces the risk of errors and security vulnerabilities, ensuring that digital assets are securely managed and transferred.

3. **Ease of Adoption for Developers and Users:** The clear and precise specifications outlined in this standard provide a straightforward blueprint for developers to implement. This ease of adoption not only accelerates the development of new applications and services on the TON blockchain but also enhances the user experience by providing a consistent and predictable framework for asset management.

4. **Facilitating Digital Ownership and Provenance:** At the heart of items and digital collections is the notion of ownership and provenance. This standard ensures that ownership rights are clearly defined and transferable in a transparent manner. The use of internal collection and item hashes as unique identifiers plays a crucial role in tracing the lineage and ownership history of digital assets.

5. **Future-Proofing and Scalability:** The Item Inscription Standard is designed with future developments in mind. It accommodates potential expansions and adaptations, allowing for scalability and evolution as the blockchain technology and digital asset landscape continue to grow and change.

6. **Cultivating a Vibrant Ecosystem:** By providing a common foundation for item inscription, this standard encourages innovation and creativity within the TON blockchain community. It opens up new possibilities for artists, collectors, and entrepreneurs to explore and create value in the digital asset space.

In conclusion, the Item Inscription Standard is a critical step towards a more unified, secure, and user-friendly environment for the TON blockchain. It lays the groundwork for a thriving ecosystem where digital assets can be created, traded, and enjoyed with confidence and ease.

## Deployment
Deployment involves initializing **Items** or **Сollections** on the blockchain. It requires legally compliant JSON formatting. 

The initial step is to deploy the collection to the owner address. You must send a transaction from your (owner) address to your (owner) address to deploy the **Collection**. So the creator of the collection will be the address. You will then need to get a unique hash of the transaction (**collection_hash**) that you can use to deploy the **Item**. 

**Item** for a certain collection can be created only on the address of the **collection's** owner. The mechanism is exactly the same - you need to send transactions from your address to your address with an **Item**. In this way, it is possible to trace the entire chain of a collection or items and ensure that the data is intact and cannot be compromised. 

#### WARNING
**The external hash for transactions is not unique and you should not use it to bind items or collection. If indexed incorrectly, items and collections may be compromised. Always verify a collection and item by internal hash.**

# Specification
1. **Protocol Definition**
   - **Protocol Name:** "Shard."
   - **Operations:** Supports "mint" and "transfer" operations for both collections and items.
   - **Type of item:** Supports "item" and "collection" types.

2. **Data Structure for Deployments**
   - **Collection Deployment:**
     - JSON structure:
       ```
       data:application/json,
       {
         "p": "shard",
         "op": "mint",
         "t": "collection",
         "max": [maximum supply number],
         "royalty": [royalty percentage],
         "metadata": {
           "key": "value"
         }
       }
       ```
   - **Item Deployment:**
     - JSON structure:
       ```
       data:application/json,
       {
         "p": "shard",
         "op": "mint",
         "t": "item",
         "collection_hash": "[transaction hash]",
         "metadata": {
           "key": "value"
         }
       }
       ```

3. **Data Structure for Transferring**
   - **Collection Transfer:**
     - JSON structure:
       ```
       data:application/json,
       {
         "p": "shard",
         "op": "transfer",
         "t": "collection",
         "hash": "[collection hash]"
       }
       ```
   - **Item Transfer:**
     - JSON structure:
       ```
       data:application/json,
       {
         "p": "shard",
         "op": "transfer",
         "t": "item",
         "hash": "[item hash]"
       }
       ```

4. **Metadata Standards**
   - **Collection Metadata:**
     - Example:
       ```
       {
         "image": ""[gzipped and then base64-encoded image]"",
         "name": "Collection name",
         "description": "Description",
         "social_links": []
       }
       ```
   - **Item Metadata:**
     - Example:
       ```
       {
         "name": "Item name",
         "description": "Description",
         "image": ""[gzipped and then base64-encoded image]"",
         "attributes": []
       }
       ```
   - **Size Limitations:** Metadata should not exceed ~50 kilobytes.
#### Use Cases

1. **Deploying a Collection**
   - **Scenario:** A user initiates a collection on the TON blockchain.
   - **Process:** The user sends a transaction from their address to their address with the specified JSON structure for collection deployment.
   - **Example:**
     ```
     data:application/json,
       {
         "p": "shard",
         "op": "mint",
         "t": "collection",
         "max": 10000,
         "royalty": 0.5,
         "metadata": {
            "image": ""[gzipped and then base64-encoded image]"",
            "name": "Collection name",
            "description": "Description",
            "social_links": []
         }
       }
     ```
   - **Collection Hash:** Upon deployment, a unique `collection_hash` is generated.

2. **Minting an Item**
   - **Scenario:** A user wants to create an item within a deployed collection.
   - **Process:** The user sends a transaction from their address to their address with the item JSON structure, referencing the `collection_hash`.
   - **Example:**
   ```
   data:application/json,
          {
            "p": "shard",
            "op": "mint",
            "t": "item",
            "collection_hash": "[transaction hash]",
            "metadata": {
               "name": "Item name",
               "description": "Description",
               "image": ""[gzipped and then base64-encoded image]"",
               "attributes": []
            }
          }
    ```
   - **Item Hash:** Each item receives a unique hash upon creation.

3. **Transferring an Item**
   - **Scenario:** An item owner wishes to transfer ownership to another user.
   - **Process:** The owner sends a transfer transaction using the item transfer JSON structure, specifying the `item hash`.

This specification outlines the technical details and provides real-world examples for using the Item Inscription Standard in the TON blockchain environment. It includes the necessary structures for deployment and transfer of collections and items, along with metadata standards and size limitations.

# Future Possibilities

The implementation of the Item Inscription Standard in the TON blockchain lays the groundwork for numerous exciting possibilities in the future. As the technology evolves and the community grows, we anticipate several developments:

1. **Advanced Metadata Management:** Future iterations of the standard could introduce more complex metadata structures. This would allow for richer descriptions of items and collections, including interactive or dynamic elements, enhancing the user experience and value of digital assets.

2. **Integration with Other Blockchain Systems:** While initially focused on the TON blockchain, the standard could be adapted for compatibility with other blockchain networks. This cross-chain interoperability would significantly expand the market and utility of digital assets.

3. **Automated Royalty Distribution:** The standard could evolve to include smart contract functionalities for automated royalty distributions. This would ensure fair compensation for creators whenever their digital assets are sold or transferred, enhancing the sustainability of the digital art ecosystem.

4. **Enhanced Security Features:** As security threats evolve, so will the countermeasures. Future versions of the standard may incorporate advanced security protocols to protect against fraud, theft, and other vulnerabilities, ensuring the integrity and trustworthiness of the blockchain ecosystem.

5. **Expansion into Virtual and Augmented Reality:** The standard could extend to encompass assets in virtual and augmented reality spaces. This would open up new avenues for creating and interacting with digital content, potentially revolutionizing the fields of gaming, education, and virtual experiences.

6. **Decentralized Finance (DeFi) Applications:** The integration of this standard with DeFi applications could lead to innovative financial products based on NFTs, such as collateralized loans or asset-backed tokens, offering new financial opportunities and greater liquidity in the digital asset market.

7. **Community Governance Models:** Future development could include mechanisms for community governance, allowing users and stakeholders to have a say in the evolution of the standard. This could lead to a more democratic and user-centric evolution of the ecosystem.

8. **Environmental Sustainability Initiatives:** As environmental concerns become increasingly important, future adaptations may focus on minimizing the ecological footprint of NFT transactions and digital asset management, aligning with broader sustainability goals.

By laying a robust foundation today, the Item Inscription Standard is not just a solution for the present but a stepping stone towards an innovative and dynamic future in the blockchain space.
