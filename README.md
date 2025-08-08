# 🚀 Fund-It-8 Subgraph

Welcome to the Fund-It-8 Subgraph! This project powers a next-generation, transparent fundraising platform on the blockchain, making charity smarter, fairer, and more data-driven. Built with The Graph, it transforms on-chain events into rich, queryable data for dApps, analytics, and AI.

## 🌐 What is The Graph?
The Graph is a decentralized protocol for indexing and querying blockchain data. Subgraphs like Fund-It-8 make it easy to build powerful dashboards, leaderboards, and chatbots by exposing blockchain events as GraphQL APIs.

## 🔗 Subgraph API Endpoint
**Subgraph URL:**  
[https://api.studio.thegraph.com/query/105145/fund-it-8/version/latest](https://api.studio.thegraph.com/query/105145/fund-it-8/version/latest)

Use this endpoint to run your GraphQL queries and power your applications!

## 🏗️ Core Entities

```
┌─────────────┐    ┌──────────────┐    ┌─────────────┐
│   Charity   │────│   Campaign   │────│  Milestone  │
│             │    │              │    │             │
│ • address   │    │ • name       │    │ • target    │
│ • name      │    │ • goal       │    │ • reached   │
│ • campaigns │    │ • state      │    │ • campaign  │
└─────────────┘    │ • donations  │    └─────────────┘
                   └──────────────┘           
                          │                   
                          ▼                   
                   ┌─────────────┐    ┌──────────────┐
                   │  Donation   │────│    Donor     │
                   │             │    │              │
                   │ • amount    │    │ • address    │
                   │ • timestamp │    │ • totalDon.  │
                   │ • campaign  │    │ • donations  │
                   └─────────────┘    └──────────────┘
```

This diagram shows the relationships between the main entities indexed by the Fund-It-8 subgraph. Each entity is linked as defined in the schema and supports rich queries for analytics, transparency, and AI.

## 📁 Key Files
- `schema.graphql`: Defines the subgraph's GraphQL schema and entities
- `subgraph.yaml`: Subgraph manifest, mapping events to handlers
- `src/`: Mapping handlers for smart contract events
- `abis/`: Smart contract ABIs for event decoding

## ⚡ Getting Started
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

## 💡 Development Tips
- Update `schema.graphql` to change or add entities
- Edit mapping logic in `src/` to handle new events or entity updates
- Use `graph codegen` after schema or ABI changes
- Test mapping logic with sample data in `tests/`

## 🔍 Example GraphQL Queries

### 1. AI Campaign Prediction Knowledge Base
```graphql
query GetCampaignTransactions($campaignId: ID!) {
  campaign(id: $campaignId) {
    name
    totalDonated
    goal
    milestones {
      target
    }
    charity {
      address
    }
    donations(orderBy: timestamp, orderDirection: desc) {
      amount
      timestamp
      donor {
        address
      }
    }
  }
}
```

### 2. Detailed Transactions & Timeline for Transparency
```graphql
query GetCampaignTransactions($campaignId: ID!) {
  campaign(id: $campaignId) {
    name
    totalDonated
    charity {
      address
    }
    donations(orderBy: timestamp, orderDirection: desc) {
      amount
      timestamp
      donor {
        address
      }
    }
    fundsReleased(orderBy: timestamp, orderDirection: desc) {
      amount
      recipient
      timestamp
      milestoneIndex
    }
  }
}
```

### 3. Donor Info & Active Campaigns for Personal Chatbot
```graphql
query GetDonorData($donorAddress: Bytes!) {
  donor(id: $donorAddress) {
    id
    totalDonated
    donations(first: 5, orderBy: timestamp, orderDirection: desc) {
      id
      amount
      timestamp
      campaign {
        id
        name
        charity {
          name
        }
      }
    }
  }
}

query GetActiveCampaigns($donorAddress: Bytes!) {
  campaigns(where: { state: "Active" }) {
    id
    name
    description
    goal
    totalDonated
    state
    charity {
      address
      name
    }
    donors(where: { donor: $donorAddress }) {
      totalDonated
    }
  }
}
```

### 4. Leaderboard Query
```graphql
query GlobalLeaderboard {
  donors(orderBy: totalDonated, orderDirection: desc, first: 100) {
    address
    totalDonated
  }
}
```

## 📚 Resources
- [The Graph Documentation](https://thegraph.com/docs/)
- [Subgraph Manifest Reference](https://thegraph.com/docs/en/developer/manifest/)
- [Graph CLI](https://thegraph.com/docs/en/developer/cli/)

## 📝 License
MIT
