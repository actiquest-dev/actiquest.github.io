---
icon: versions
label: AI Live Pod

---

# Decentralized Storage and Governance Over On-Device AI

----------
## 1. Abstract

**Actiquest On-Device AI**  (running in the AI Live Pod) is the complex of Vision/LMM and NLP neural models brings next-generation edge intelligence to users’ devices by combining efficient local inference with a robust  **Compute-to-Data**  paradigm. Rather than pulling massive datasets into centralized servers for training,  Actiquest stores and governs these datasets on the **Internet Computer (ICP)**—enabling a decentralized, community-driven approach to data handling. This litepaper outlines how these components integrate to deliver private, up-to-date, and decentralized AI solutions,  **including the process of delivering the best pre-trained models to end-user devices.**


## 1. Introduction & Motivation

### 1.1 Background

The rapid ascent of  **artificial intelligence**  (AI) in domains such as computer vision, natural language processing, and personalized recommendations has often hinged on  **centralized**  data pipelines. Traditional AI workflows store large volumes of data in monolithic data centers, train models on powerful, centralized compute clusters, and then deliver these models to end users—often via cloud APIs. However, this model presents several  **shortcomings**:

-   **Privacy Concerns**: Centralized datasets can be vulnerable to leaks or unauthorized usage.
-   **Single Points of Failure**: A single entity controlling data and model access can impose censorship, raise fees, or unilaterally change usage terms.
-   **Limited Community Involvement**: Contributors (e.g., data owners, labelers, or subject-matter experts) typically have little direct input into model curation or governance.
-   **Scalability & Latency**: Constantly streaming data to and from the cloud can be costly and introduce performance bottlenecks, especially for real-time or sensor-based applications.

### 1.2 Vision for a Decentralized On-Device AI Ecosystem

Instead, a  **decentralized architecture**  can address many of these concerns by distributing data storage, governance, and inference. We propose the Internet Computer (ICP) as the  **trustless backbone**  to store and manage data, while allowing:

1.  **On-Device Local Inference**
    -   Models run locally on user devices or edge hardware, ensuring low-latency, privacy-preserving AI.
2.  **Community Governance**
    -   A decentralized autonomous organization (DAO) or Service Nervous System (SNS) on ICP oversees dataset curation, usage terms, and revenue distributions—enabling transparent decision-making.
3.  **Compute-to-Data**
    -   Data remains encrypted and within canisters; compute providers request access to train or fine-tune models. Once approved, the data is decrypted for that specific job (off-chain or on specialized subnets).
4.  **Immutable Logs & Versioning**
    -   All changes to datasets, model checkpoints, and governance parameters are recorded on the ICP, guaranteeing tamper-proof auditability.

----------

## 2. The Role of the Internet Computer (ICP)

### 2.1 Core ICP Design

1.  **Canisters**
    -   Smart contracts on ICP, hosting both code (WebAssembly) and data (stable memory). They can hold structured data, files, and application logic.
    -   Canisters are powered by “cycles,” ensuring a predictable cost model.
2.  **Boundary Nodes**
    -   Edge gateways that serve user-facing requests (e.g., HTTP calls) and route them to the correct canister. They can also cache static content, partially acting like a lightweight CDN.
3.  **Subnet Architecture**
    -   The Internet Computer network is composed of subnets (groups of replica nodes) which can collectively run canisters. This design ensures redundancy and decentralization.
4.  **Service Nervous System (SNS)**
    -   A framework that transforms a canister-based application into a community-governed DAO. Token holders can propose and vote on code updates, data changes, fees, or rewards distribution.

### 2.2 Advantages for AI Data Storage and Governance

1.  **Low On-Chain Storage Cost**
    -   The ICP’s model, while not as inexpensive as traditional cloud storage, is comparatively cost-effective versus other blockchains that might charge significant gas fees for data.
2.  **DAO Governance Out-of-the-Box**
    -   Using SNS, developers can quickly set up a governance token, proposal system, and treasury logic—ideal for datasets that require curation, licensing, or community-based moderation.
3.  **Stable Memory for Large Data**
    -   Each canister can store up to 4GB of stable memory (with possible future increases), enabling direct storage for moderate-sized models or datasets. For larger ones, chunked approaches or multi-canister architectures are used.
4.  **Global Accessibility**
    -   The Internet Computer is designed to be globally accessible, with boundary nodes offering near-universal coverage for data retrieval and dApp access.

----------

## 3. Architectural Overview

### 3.1 Storage Layer

#### 3.1.1 Chunked Data Canisters
-   **File-Style Canisters**: For vision datasets (images, videos), large text corpora, or sensor logs, developers can implement chunked storage. Each chunk is typically <1MB, stored in stable memory.
-   **Metadata Registry**: A separate canister that maps dataset IDs to chunk references (hashes), file sizes, and optional encryption keys or IPFS-like references.

#### 3.1.2 Off-Chain Hybrids
-   Some cases may be more effective a hybrid approach, where large or infrequently accessed data is stored using centralized cloud services. The ICP canister then holds references, licensing info, and verifies data integrity with stored hashes.

### 3.2 Governance Layer
#### 3.2.1 DAO (SNS) or Custom Governance

-   **SNS**: A built-in approach where the Internet Computer automatically sets up a governance token, neuron-based staking, and proposal logic. The dApp’s community can decide on data updates, usage fees, or distribution of revenues.
-   **Custom DAO**: Developers can also code a custom governance canister in Rust or Motoko, giving them more tailored logic (e.g., specialized curation markets, nested proposals, or fine-grained permission controls).

#### 3.2.2 Proposal Lifecycle
1.  **Proposal Creation**: A user or recognized contributor adds a proposal to ingest a new dataset, change a licensing fee, or incorporate a new model checkpoint.
2.  **Voting**: Token holders cast votes. If the proposal meets quorum and passes, the canister logic automatically executes the changes.
3.  **Actions**: Approved proposals might add new chunk references, pay contributors, or update a model’s version in a specialized canister.

### 3.3 Compute-to-Data Flow
1.  **Data Remains in Canisters**
    -   Images, videos, bounding boxes, masks (Vision models data) plus text corpora, embeddings, tokenized references (LLM data); stored in chunked file canisters or off-chain data storage, with the ICP canister tracking hashes and metadata.
2.  **Off-Chain Training Request**
    -   A GPU/ or decentralized CPU node on Bittensor training subnet/ or any other external HPC training environment requests access to the dataset (depends on situation).
    -   The DAO or data owner grants a decryption key if the proposal is passed or the entity meets certain criteria (e.g., paid a licensing fee).
3.  **Secure Training**
    -   The HPC training environment decrypts and processes the data locally.
    -   Zero-knowledge proofs or secure enclaves may be used to reduce data exposure risks.
4.  **Model Checkpoint Upload**
    -   After training, the HPC training environment returns a new model checkpoint, which is stored in a “Model Registry Canister” on the ICP, ensuring an immutable record of model evolution.
    -   The DAO votes again to accept or reject the checkpoint, ensuring community trust.

### 3.4 On-Device AI Delivery
1.  **Running Models on-Device**
    -   Local Inference devices like **AI Live Pod** are capable of loading model weights, verifying their authenticity, and running real-time inference with a lightweight model.
2.  **Fetching Checkpoints**
    -   Device queries the Model Registry Canister for the latest verified checkpoint.
    -   A cryptographic signature check ensures the model is genuine.
3.  **Private Computation**
    -   Personal data of AI users (e.g., health metrics, camera images) remains on the device, never shipped to a central server.
    -   This fosters privacy, reduces latency, and saves network costs.

----------

## 4. Technical Details & Implementation Considerations

### 4.1 Cryptographic Signatures & Hashing

1.  **Data Upload**
    -   Contributors sign the data with their private key, ensuring authenticity.
    -   The canister verifies the signature with the contributor’s public key.
2.  **Model Checkpoints**
    -   Post-training, an aggregator or HPC node signs the final weights. The DAO can verify it was indeed produced by the correct aggregator.
3.  **Integrity Hashes**
    -   Each chunk or file is hashed (e.g., SHA-256) to detect any tampering. The canister stores these hashes, and any mismatch on retrieval flags an error.

### 4.2 Access Control & Encryption

1.  **Encryption Keys**
    -   The data owner or the DAO can store encryption keys in a canister, releasing them only when an approved training request is made.
2.  **Compute Nodes**
    -   They decrypt data locally, train the model, and discard it after the job to minimize leakage.
3.  **Zero-Knowledge Proofs (Optional)**
    -   To prove certain properties (e.g., “this data meets size or content requirements”) without exposing the underlying content.

### 4.3 Pricing & Monetization

1.  **Cycles & ICP**
    -   Storing metadata in canisters requires cycles. The DAO might maintain a treasury of cycles to fund ongoing storage.
2.  **Licensing Fees**
    -   External compute providers or organizations wanting to train with certain datasets may pay fees to the DAO, which then rewards data owners or labelers.
3.  **Token Incentives**
    -   If the system is governed by an SNS, the governance token can be used to reward contributions, stake in proposals, or trade on open markets.

----------

## 5. Example Use Case: Athlete Performance Data

1.  **Dataset Capture**
    -   Athletes record heart rate, motion, or video data using special training wizard app. Finally data is labeled and prepared for training routine using this app.
    -   The athlete’s training wizard app signs and encrypts the data, uploading it to an ICP canister.
2.  **DAO Proposal**
    -   The athlete proposes that this new dataset be included in next round of training. DAO token holders vote, evaluating data authenticity and potential value for improving the AI model.
3.  **Training on External Training Nodes**
    -   Once approved, an external training node obtains the decryption key, trains or fine-tunes the relevant model.
    -  Once training yields a strong or improved checkpoint, participants (or the training orchestrator) propose this checkpoint as an “official update.”
    -   The HPC environment uploads the new weights to the Model Registry Canister.
4.  **On-Device AI Model Activation**
    -   The new checkpoint is loaded into memory on the on-device AI, replacing or augmenting older models.
    - If the model is encrypted, the On-device AI obtains an access key from the DAO or canister, decrypting it locally.
   5.  **Benefits to On-Device AI users** 
		-   Users seamlessly benefit from updated AI capabilities (e.g., improved video recognition accuracy or reasoning).
		- All model versions are tied to immutable references on the IC, preventing unauthorized or malicious model updates.
		- If the community finds a checkpoint suboptimal, they can propose rolling back or adopting a different checkpoint—ensuring user devices always get **trusted, high-quality** models.
----------


## 6. Future Enhancements

### 6.1 Specialized ICP Subnets

-   **High-Compute Subnets**: Future ICP subnets might integrate CPU/GPU resources. This would enable direct on-chain training, reducing reliance on external HPC.
-   **Large Stable Memory**: Ongoing research might push stable memory limits beyond 4GB, simplifying chunking or multi-canister strategies.
- 

### 6.2 Improved DAO Modules

-   **Curation Markets**: Weighted voting or bonding curves for data quality can systematically reward high-value data.
-   **Automated Label Bounties**: Users can earn tokens for labeling unlabeled data, fostering continuous improvement.

### 6.3 Integration with Other Protocols

-   **Cross-Chain Bridges**: Linking ICP canisters to Ethereum, Polkadot, or Bittensor (for decentralized AI training) can broaden the ecosystem.

### 6.4 Secure Enclaves & ZK Computation

-   **Hardware Enclaves**: Potential future subnets or off-chain nodes could offer Intel SGX/TEE-based computation for advanced privacy.
-   **Zero-Knowledge Training**: Methods like fully homomorphic encryption or secure multi-party computation might eventually allow partial training on encrypted data without decryption.

### 6.4 Edge-Level Model Customization
- **Future enhancements** to the AI Live Pod could allow partial fine-tuning directly on the device (for small personal datasets), then contributing insights or differential privacy gradients back to the decentralized model storage.

----------

## 7. Security & Integrity Analysis

1.  **Data Authenticity**
    -   Mandatory cryptographic signatures for data uploads.
    -   DAO can slash or penalize malicious data contributors if proven fraudulent.
2.  **Immutable Logging**  
    -   Any change in the canisters’ state (addition/removal of data, model checkpoint updates) is permanently recorded and visible, preventing unilateral tampering.
3.  **Resilience & Redundancy**
    -   ICP replicates canisters across nodes in a subnet. Even if some nodes fail, the data remains intact.
4.  **DAO Governance Risks**
    -   As with any token-based governance, whales or large stakeholders could exert heavy influence. Mechanisms like decentralized distribution, reputation scoring, or delegated voting can mitigate plutocratic control.

----------

## 8. Ecosystem Benefits

1.  **Scalable & Decentralized** 
-   Scalable models, seamless training routine, decentralized backend, and on-device AI ecosystem, that contains from local AI inference sources can all interoperate without a single point of failure and be more effective in general.
 
2.  **User & Data Owner Trust**
- The community (via DAO) collectively audits updates and usage.
-   Data owners see a clear trail of where and how their data is used.
3.  **High-Quality Model Training**
-   Bittensor/GPU/HPC AI training ecosystems provides a robust, incentivized environment, attracting resources from around the globe.
-   Continual improvements keep models fresh and competitive.
4.  **Monetization & Rewards**
-   Dataset owners, model contributors, and compute providers can earn tokens or revenue shares, making the ecosystem self-sustaining.
5.  **On-Device Privacy & Performance**
-   AI Live Pods run models directly on the user device, ensuring minimal latency and protecting sensitive user data from leaving the device.
6.  **Seamless Model Delivery**
-   End users automatically get updated model checkpoints verified by the DAO, removing friction and ensuring trust in each new release.

## 8. Conclusion

**Decentralized storage and governance**  on the  **Internet Computer**  presents a powerful alternative to traditional, centralized AI pipelines.

The  **Actiquest On-Device AI**  platform merges the best of decentralized technology—**immutable data storage, community governance, scalable training,**  and  **privacy-preserving inference**—all while simplifying  **model delivery**  to end-user devices. By adopting a  **Compute-to-Data**  approach on the  **Internet Computer**  for robust AI development:

1.  **Data owners retain control**  of their valuable datasets.
2.  **Developers and participants**  are fairly rewarded through DAO-based monetization.
3.  **Users**  benefit from  **on-device AI**  with minimal latency and maximum privacy.
4.  **Model updates**  are frictionless and tamper-proof, strengthening user trust and system resilience.

The result is a novel AI ecosystem that meets modern demands for  **transparency, decentralization, performance,**  and  **easy model delivery**, fostering a more open, trustable, and dynamic future for vision and language AI applications at the edge.

-   **Data Integrity & Transparency**: Immutable canisters ensure that datasets and model checkpoints can be audited and are safe from covert manipulation.
-   **Community-Driven Governance**: SNS or custom DAO logic empowers data owners, labelers, and compute providers to shape the platform’s evolution, aligning incentives for high-quality data and model improvements.
-   **Compute-to-Data Privacy**: By encrypting data on the IC, then selectively granting access for off-chain or specialized on-chain compute, sensitive information is protected while still feeding robust training workflows.
-   **On-Device AI**: Delivering newly approved models directly to user devices reduces latency, preserves privacy, and unlocks real-time or offline use cases, especially relevant for wearables, smart home devices, or remote sensors.

In sum, this  **document**  underscores the viability of building a  **trustless, decentralized AI ecosystem**  that harnesses the Internet Computer’s technical capabilities to store, govern, and continually update AI models—paving the way for more equitable, privacy-respecting, and community-centered AI solutions at scale.
