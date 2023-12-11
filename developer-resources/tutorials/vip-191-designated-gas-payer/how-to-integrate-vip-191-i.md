# How to Integrate VIP-191 (I)

Hi guys, welcome to this section of the tutorials. I am very excited about the new features that vechain has introduced recently, for example, the VIP-191 fee delegation. I will quickly walk you through what it is and how to use it in the following tutorials.

### What is VIP-191? <a href="#what-is-vip-191" id="what-is-vip-191"></a>

In short, VIP-191 is a fee delegation proposal that gets realized on vechain that enables the end-user to use blockchain without paying native tokens/cryptocurrencies. The fee is paid by a sponsor. To make a metaphor in real life, it is like a father as a primary credit cardholder giving his kid a secondary credit card to go shopping. All the fees incurred are paid by the father in the end.

<figure><img src="https://cdn-images-1.medium.com/max/2152/1*-vWHlvBFcxlm3D_XeF6AlA.png" alt=""><figcaption><p><em>Father pays for his son’s shopping cart.</em></p></figcaption></figure>

### Why is VIP-191 Important? <a href="#why-is-vip-191-important" id="why-is-vip-191-important"></a>

Just as Ethereum has introduced **CREATE2** opcode to solve (in a weird way) the “user-onboarding” issue described in [this article](https://medium.com/coinmonks/user-on-boarding-and-create2-a67a185fd149), vechain also realized the friction (huge obstacle, to be honest) for new users to adopt the blockchain system. For example, wallet setup, private key safekeeping, buying cryptocurrencies on exchanges, calculating transaction fees and so on.

On the developer’s side, it’s difficult to attract new users _**outside**_ the crypto community to try out the app even if it is awesome.

On the users’ side, the high setup knowledge of crypto will render them helpless before they get a taste of the awesome new app.

If the above practice continues, any blockchain will soon find the user-base is not expanding but shrinking. Only “savvy” tech users are in this game but inexperienced users are excluded outside. It’s against the “stupid and simple” norm we’ve been used to today since the Web2.0 and mobile-dominant era where apps are easy to use day by day.

This _death spiral_ needs to be stopped and replaced by an easy-to-go approach:

> How about the users don’t worry about the fees/crypto and just go using the dApps directly?

Here comes the VIP-191 fee delegation protocol on vechain. 😃

### Where does VIP-191 Come to Play? <a href="#where-does-vip-191-come-to-play" id="where-does-vip-191-come-to-play"></a>

Quite a few scenarios as I have observed.

I give three examples that can benefit from the fee delegation of VIP-191.

**1) A Standalone Web App Game.**

So suppose you have a web game that uses vechain as a “points storing” database. Whenever the end-user calls your smart contract to upgrade their game hero, normally, they should pay for the transaction fee in VTHO (a gas token like ETH). However, now you have launched a “promotion” where newly registered users are allowed to try out your game 3 days free, all the transaction fees are covered by you — the developer’s big wallet.

<figure><img src="https://cdn-images-1.medium.com/max/2832/1*0r9a_RmPNJqKYrWSiA6ZTA.png" alt=""><figcaption><p><em>Games use VIP-191 for promotion</em></p></figcaption></figure>

This will improve your exposure to non-tech users without knowing vechain at all. And once they get addicted to the game, you can charge them a subscription fee in fiat ($5/month?) and keep sponsoring the game operation by your wallet. Win-Win.

**2) Shipping & Logistics company**

Suppose a shipping company is using the vechain as its blockchain backbone for tracking cargos. Employees on the positions, eg. custom clearing, shipping, and inspecting need to write to the blockchain. All those operations need VTHO to fuel them. Sometimes each shipment involves up to 20–30 middlemen.

Instead of charging each account the employee holds with the minimum tokens they need and keeping an eye on the balance of each account, the management team can “sponsor” their employees’ actions and all the fees are deducted directly from a big wallet — the company’s operation wallet.

This improves security by eliminating the possible theft of wallets and ease the burden of balance tracking. The management team can also dynamically choose for whom and for what actions they would like to sponsor.

<figure><img src="https://cdn-images-1.medium.com/max/3252/1*yMF-aQQtSHU1PfIlKOd2mA.png" alt=""><figcaption><p><em>Shipping Company uses VIP-191</em></p></figcaption></figure>

**3) The Crypto Exchanges**

Nowadays crypto exchanges use simple logic to collect ERC20/VIP-180 tokens from the end-users: It gives end-user a temp “deposit address” to transfer to. Once the user has done deposition, the exchange then fuels the account with some ETH/VTHO and then “withdraw” further to the exchange’s cold wallet for safekeeping (by initiating another transaction).

This 2-step process can be largely improved by the VIP-191 fee delegation protocol.

Suppose the exchange has a hefty wallet that can sponsor the withdraw action, then the exchange can eliminate the 1st step of transferring fuel money to the deposit address (which involves a careful calculation of the fee and one online transaction which takes minutes). It can simply initiate the 2nd step withdraw immediately and let the fee be deducted from the hefty wallet, simple and elegant.

### How does VIP-191 Work? <a href="#how-does-vip-191-work" id="how-does-vip-191-work"></a>

It is very simple.

As a developer, you probably already understood a normal valid transaction request is a transaction object with the sender’s signature.

VIP-191 is using a specially formed signature composed by the user and the sponsor together.

Just as the picture below has depicted, once the transaction is forged, the user extracts the hash (information digest) and signs it as normal. At the same time, the sponsor also signs the hash but with additional information “for whom”. Then we concatenate the two signatures together, then send the final composed signature along with the transaction itself, to the vechain network.

<figure><img src="https://cdn-images-1.medium.com/max/3412/1*EqQX-xtv6RLNb0t1nUQCdQ.png" alt=""><figcaption><p><em>Concatenate Signatures to forge a VIP-191 signature</em></p></figcaption></figure>

### What’s next: <a href="#what-s-on-next" id="what-s-on-next"></a>

Thanks for reading this article.

After solving the problem of “why and how”, I will set up a small example to show off how to integrate the VIP-191 to your dApp workflow. Keep reading!
