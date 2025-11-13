---
description: Economic and X-Node interactions with the official node rewards dApp.
---

# Node Rewards Programme

{% hint style="info" %}
The official node rewards dApp is available at [app.rewards.vechain.org](https://app.rewards.vechain.org)
{% endhint %}

In blockchain ecosystems the word node is a reserved word which is used to refer to a computer system which stores a copy of the blockchain transactions. In the vechain ecosystem the word node can also be used to refer to a non-contractual address that holds, soft stakes, a certain amount of VET. These reward nodes are more accurately called Economic or X-Nodes, but they are often referred just referred to as nodes. Accounts which hold an Economic or X-Node are identifiable by ownership of a non-fungible token (NFT). Additional privileges are provided to Economic and X-Node holders. Both Economic and X-Node holders having voting rights on vechain governance proposals. Additionally, X-Node holders are entitled to additional VTHO rewards from the VechainThor X-Node bonus pool, which are VTHO rewards on top of the basic generation formula.

{% hint style="warning" %}
To maintain node ownership, it is crucial to retain a specified amount of VET in your wallet; failure to do so may result in node downgrading or destruction.
{% endhint %}

Both Economic and X-Nodes have distinctive tiers which are determined by the following criteria:

* **Balance Requirement:** The quantity of VET to be held in your wallet for the acquisition, generation, and sustenance of your node.
* **Voting Tier:** Indicates the weight of your vote within vechain's voting ecosystem, determined by the type of node you own.
* **Maturity Period:** The duration of time required for your node to upgrade from the current level to the next level.
* **Generation Ratio (Applicable exclusively to X-Nodes):** Represents the percentage of additional VTHO rewards generated in comparison to the basic generation formula.

### Economic Nodes

Users can apply for an Economic Node if they meet the required balance of VET in their address. Additionally, they are available for purchase on the secondary market. Owning an Economic Node provides you with the right to participate in vechain's governance process.

### X-Nodes

These nodes are exclusively available for purchase on the secondary market. They generate additional VTHO rewards derived from a 5 billion VET locked by the vechain foundation to generate VTHO for the VechainThor X-node bonus pool.\* Owning an X-Node provides you the right to participate in vechain's governance process.

{% hint style="info" %}
The VechainThor X-Node bonus pool size is 5bln VET. This allocated VET is locked and produces 0.000432 VTHO per VET per day. The daily generated VTHO rewards of 2.16mln VTHO are rewarded to all eligible VechainThor X-Node token holders.
{% endhint %}

{% hint style="info" %}
[vevote.vechain.org](https://vevote.vechain.org) vechain governance proposal website.
{% endhint %}

### X-Node Bonus VTHO Reward Claiming

An X-Node owner can claim their bonus VTHO reward at any time by claiming from the smart contract. VTHO bonus reward claims are disbursed hourly through multi-task transfers (MTT). Claiming rewards costs 40 VTHO from the claimed reward to cover transfer costs. VTHO claims are processed and credited within an hour. If you were an X-Node holder who disposed of the node, you still have the option to claim any unclaimed VTHO. The calculation for VTHO staking rewards is available [here](https://vechainstats.com/vtho-calculator/).

### Node Upgrades and Downgrades

Users have the option to apply for a node upgrade when their address satisfies the minimum VET holding requirement of the next Economic or X-Node level. Upon doing so, the node will undergo an upgrade to the next level following the maturity period. It's important to note that your node cannot be transferred or placed in auction during this maturity period. The remaining time for your upgrade can always be monitored, and you retain the ability to cancel the upgrade while it is in progress.

Downgrades, on the other hand, do not incur a maturity period and occur within a few minutes. The main cause of node level downgrades is due to the required VET balance no longer being meet.

If you own an Economic Node and face a downgrade, you will be demoted to the Economic Node corresponding to your VET balance or to no node if the VET balance falls below the minimum requirement for the initial node level.

For X-Node owners undergoing a downgrade, the X-Node status will be lost, and you will be allocated an Economic Node in accordance with your VET balance or no node if the VET balance is insufficient for any node.

It is essential to note that the VeThorX Node is an exception among X-nodes; if downgraded, it will be destroyed, and you will be left with no node entitlement.

### Node Instant Transfer and Direct Sale

Users can either transfer their Economic or X-Node to another address instantly or create a direct sale to a specific address. Instant transfer facilitates the swift relocation of the node to a different address, while direct sale allows the user to sell the node to a specific address, establishing both a price and duration for the sale.

In both scenarios, the node holder is required to maintain the minimum VET corresponding to the node tier until the node ownership is successfully transferred. It is essential for the recipient to ensure that their address meets the minimum VET holding requirement. It is worth noting that nodes cannot be transferred or placed on direct sale during the maturity period, and upgrades are not available during the transfer or sale process.

If the recipient address currently possesses a VechainThor Node, they will not be eligible to receive an additional node. Following the successful transfer or sale of node ownership to a new address, a 24-hour cooldown period will ensue before another transfer or sale can take place.

### Node marketplace

Node holders have the option to list their node on the market for a public auction. There are two types of auction available; Fixed Price and Dutch Auction.

In the Fixed Price Auction, the node holder, when initiating the order, must specify a sales price greater than 0 and a valid order duration ranging from 1 to 7 days.

For those opting for a Dutch Auction, the node holder needs to set a starting price, the lowest price, and a valid order period between 1 and 7 days. During a Dutch Auction, the price gradually decreases every 5 minutes in a linear manner until it reaches the lowest price.

Nodes available for purchase can be viewed by users in the marketplace section of the [official vechain rewards dApp](https://app.rewards.vechain.org). If the node is on Dutch Auction, the current price will be displayed.

In both auction types, the principle of first come, first served applies. Once a user successfully purchases the node, ownership is transferred, and it will no longer be visible on the trading market. If no one purchases the node, the auction will be automatically cancelled after the valid period.

After the successful sale of node ownership to a new address, a 24-hour cooldown period will take effect before another transfer or sale for that specific node can occur.
