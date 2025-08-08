# Fund-It-8 Subgraph

This repository contains the subgraph for Fund-It-8, a decentralized fundraising platform. The subgraph indexes and exposes blockchain data for charities, campaigns, donors, donations, milestones, and fund releases using The Graph protocol.

## About The Graph
The Graph is a decentralized protocol for indexing and querying blockchain data. Subgraphs define how to transform and serve on-chain data via GraphQL APIs, enabling efficient and flexible access for dApps and analytics.

## Subgraph Entities
- **Charity**: Registered organizations with campaigns
- **Campaign**: Fundraising events with milestones
- **Milestone**: Goals within campaigns
- **Donor**: Users who donate to campaigns
- **CampaignDonor**: Donor-campaign relationship, tracks donations and ranking
- **Donation**: Individual donation records
- **FundRelease**: Records of released funds for milestones

## Key Files
- `schema.graphql`: Defines the subgraph's GraphQL schema and entities
- `subgraph.yaml`: Subgraph manifest, mapping events to handlers
- `src/`: Mapping handlers for smart contract events
- `abis/`: Smart contract ABIs for event decoding

## Getting Started
1. Install dependencies:
   ```powershell
   npm install
   ```
2. Generate types from the schema and ABIs:
   ```powershell
   graph codegen
   ```
3. Build the subgraph:
   ```powershell
   graph build
   ```
4. Deploy the subgraph:
   ```powershell
   graph deploy fund-it-8
   ```

## Development Tips
- Update `schema.graphql` to change or add entities
- Edit mapping logic in `src/` to handle new events or entity updates
- Use `graph codegen` after schema or ABI changes
- Test mapping logic with sample data in `tests/`

## Resources
- [The Graph Documentation](https://thegraph.com/docs/)
- [Subgraph Manifest Reference](https://thegraph.com/docs/en/developer/manifest/)
- [Graph CLI](https://thegraph.com/docs/en/developer/cli/)

## License
MIT
