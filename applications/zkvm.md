# W3F Grant Proposal

- **Project Name:** zkVM
- **Team Name:** ALPHA LABS FZCO
- **Payment Address:** 
- **[Level](https://github.com/w3f/Grants-Program/tree/master#level_slider-levels):** 2

## Project Overview :page_facing_up:

### Overview

zkVM aims to bring an easily programmable general purpose STARK based virtual machine to substrate.  We believe that zero-knowledge technology is posed
to usher in the next wave of innovation in decentralised systems.  However, most zero-knowledge libraries require highly specialised expertise 
to construct zero-knowledge circuits that represent a specific computation.  If we intend to realise the full potential of zero-knowledge technology
we must reduce the barrier to entry and increase accessibility for developers.  This goal can be achieved via the application of zero-knowledge virtual 
machines that can be programmed using languages and constructs that are familiar to developers.  We believe that there is a huge (largely untapped) potential 
for the application of zero-knowledge technology within the substrate ecosystem.  We hope that by providing a zkVM we can help realise this potential.

### Project Details

This project will leverage [`Miden VM`](https://github.com/maticnetwork/miden), a STARK based zero-knowledge virtual machine built on the
[`Winterfell`](https://github.com/novifinancial/winterfell) proof system.  We will provide a pallet implementation that allows for *creation*, *execution* and 
*verification* of programs on the VM.  We will also expose verification via rpc such that client side applications can perform verification of proofs.  

#### API

```rust
pub fn create(origin: OriginFor<T>, init: Script, num_output: u32) { ... }

pub fn call(origin: OriginFor<T>, target: Address, input: Vec<u32>) { ... }

pub fn verify(origin: OriginFor<T>, target: Address, input: Vec<u32>, output: Vec<u32>, proof: StarkProof) { ... }
```

#### Data Model

```rust 
pub struct Program {
    pub code_hash: Digest,
    pub output: Vec<u32>,
    pub proof: StarkProof
}

pub struct Codes {
    pub code_hash: Digest,
    pub code: Script
}
```

*The API and Data Model may be subject to change 

### Ecosystem Fit

The deliverables described above are intended to be used by any substrate based project that would like to leverage an easily programmable and performant STARK 
based zkVM.  This project makes zero-knowledge technology more accessible to developers within the substrate ecosystem.  The table below describes
the similarities / differences of other zero-knowledge projects in the substrate ecosystem.

|                                                                                      Project | Similarities                                                      | Differences                                                                                              |
|---------------------------------------------------------------------------------------------:|-------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------|
|                                       [Astar - Plonk](https://github.com/AstarNetwork/plonk) | On-chain proof verification                         | Uses plonk proof system. <br/>Off-chain proof generation.  <br/>Doesn't provide a VM (uses raw circuits) |
|                                     [Starks Network](https://github.com/gbctech/starks-node) | Uses STARKS. <br/>Provides a VM. <br/>On-chain proof verification. | Uses less feature rich and less efficient Distaff VM.                                                    |
|                                              [zkMega](https://github.com/patractlabs/zkmega) | On-chain proof verification.             | Uses SNARKS. <br/>Off-chain proof generation. <br/>Rollup focussed. <br/>Doesn't provide a VM.                |

## Team :busts_in_silhouette:

### Team members

- Francesco Risitano - Project Lead

### Advisors

- [Zero Network](https://github.com/zero-network)

### Contact

- **Contact Name:** Francesco Risitano
- **Contact Email:** francesco.risitano95@gmail.com
- **Website:** N/A

### Legal Structure

- **Registered Address:** Dubai Silicon Oasis, DDP, Building A2, Dubai, United Arab Emirates
- **Registered Legal Entity:** ALPHA LABS FZCO

### Team's experience

#### Francesco Risitano
Francesco found his passion for complex systems and programming during his particle physics research at CERN where he developed 
a machine learning algorithm concerned with particle identification at the ATLAS detector.  He then transitioned to industry where he
worked at a telecommunications company applying machine learning models at scale for broadband network assurance and recommendation engines. 
Following this he worked at a consultancy where he was the technical lead responsible for architecting and engineering a highly scalable event streaming solution 
for government. In this role he was responsible for managing a technical team of 12 members.  He gained significant experience across
architecture, engineering, devops, testing and project management.  He then started contributing to open source blockchain projects and found himself
a part-time (evenings / weekends) role building a data oracle.  Following this he transitioned full time to blockchain development where he built reef chain, 
an EVM compatible substrate based chain.  He is also a Mina genesis founding member and participated in Mina's builders program to develop a POC layer 2 rollup based DEX.  His
experience at Mina and REEF has fuelled his desire to bring more zero-knowledge technology to the substrate ecosystem and has now left his role at REEF
to focus on achieving this goal.

#### Zero Network
Zero Network have been working on implementing zero knowledge libraries and pallet. We have already delivered several grants
such as `plonk` and `zk rollups`. And now working on implementing privacy-preserving transactions blockchain.

- [plonk](https://github.com/w3f/Grants-Program/blob/master/applications/zk-plonk.md)
- [zk rollups](https://github.com/w3f/Grants-Program/blob/master/applications/zk-rollups.md)
- [zero network](https://github.com/w3f/Grants-Program/blob/master/applications/zero-network.md)

We can contribute this project as we have already experienced implementing `pallet` which is compatible with `Substrate` and we have a lot of knowledge about
optimization using parallelize, algorithm and architecture. We are also working on zk-SNARKs friendly `VM` so we would be happy to collaborate.

### Team Code Repos

- https://github.com/frisitano

### Team LinkedIn Profiles

- https://www.linkedin.com/in/francescorisitano/

## Development Status :open_book:

Development has not started yet.

### References

- https://github.com/maticnetwork/miden/issues/201
- https://eprint.iacr.org/2018/046.pdf
- https://nakamoto.com/cambrian-explosion-of-crypto-proofs/

## Development Roadmap :nut_and_bolt:

### Overview

- **Total Estimated Duration:** Duration of the whole project (e.g. 2 months)
- **Full-Time Equivalent (FTE):**  Average number of full-time employees working on the project throughout its duration (see [Wikipedia](https://en.wikipedia.org/wiki/Full-time_equivalent), e.g. 2 FTE)
- **Total Costs:** Requested amount in USD for the whole project (e.g. 12,000 USD). Note that the acceptance criteria and additional benefits vary depending on the [level](../README.md#level_slider-levels) of funding requested. This and the costs for each milestone need to be provided in USD; if the grant is paid out in Bitcoin, the amount will be calculated according to the exchange rate at the time of payment.

### Milestone 1 — Implement zkVM Substrate Module

- **Estimated duration:** 2 month
- **FTE:**  2
- **Costs:** $50,000 USD

| Number | Deliverable            | Specification                                                                                                                                          |
| -----: |------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| 0a. | License                | MIT                                                                                                                                                    |
| 0b. | Documentation          | We will provide both **inline documentation** of the code and a basic **tutorial** that explains how a user can register, execute and verify programs. |
| 0c. | Testing Guide          | Core functions will be fully covered by unit tests to ensure functionality and robustness. In the guide, we will describe how to run these tests.      |
| 0d. | Docker                 | We will provide a Dockerfile(s) that can be used to test all the functionality delivered with this milestone.                                          |
| 0e. | Article                | We will publish an **article** that explains how we were able to build out our deliverables and how substrate projects can leverage the zkVM module.   
| 1. | Substrate module: zkVM | We will create a Substrate module that will enable a user to register, execute and verify a program using miden VM with winterfell backend.            |

## Future Plans

- We will promote the module to substrate developers via discord, telegram and element.
- We are committed to maintaining the module as `Miden VM` is upgraded.
- We plan to leverage this module to develop zero-knowledge infrastructure and applications within the substrate ecosystem.


## Additional Information :heavy_plus_sign:

**How did you hear about the Grants Program?** Web3 Foundation Website
