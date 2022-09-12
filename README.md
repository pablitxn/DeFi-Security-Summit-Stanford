# **Secureum A-MAZE-X Stanford**
## **A Smart Contract Security *Capture the Flag* Workshop**

![A-MAZE-X-Stanford-LOGO](https://github.com/eugenioclrc/DeFi-Security-Summit-Stanford/blob/master/img/A-MAZE-X-Stanford.png)
*hosted by the Stanford University as part of **[Defi Security 101](https://defisecuritysummit.org/defi-security-101/)***\
*built by [eugenioclrc](https://github.com/eugenioclrc) and [luksgrin](https://github.com/luksgrin)*\
*special thanks to [patrickd](https://github.com/patrickd-), [StErMi](https://github.com/StErMi), [tinchoabbate](https://github.com/tinchoabbate) and [Rajeev](https://twitter.com/0xrajeev) for reviewing, commenting and helping during the elaboration and design of this CTF Workshop*

-----------------------------

# **Instructions** 🕹️

This Workshop consists in a series of challenges, of increasing difficulty, targetting different **concepts** and common **vulnerabilities** found in **DeFi**. The CTF is designed in different flavors for all kinds of users.

-----------------------------

## **This is the A-MAZE-X `Foundry` flavor**

Best suited for users who are very familiar with `Solidity` and do not want to use additional languages.
The following setup tutorial will guide you through the installation of `Foundry` and its setup.

### **Clone this repository**

Run the command below to clone this repository into your local machine

``` bash
git clone git@github.com:eugenioclrc/DeFi-Security-Summit-Stanford.git
cd DeFi-Security-Summit-Stanford
git checkout foundry
```

### **Install `Foundry`** *(if you don't have `Foundry` already installed)*

Run the command below to get `foundryup` the `Foundry` toolchain installer:

``` bash
curl -L https://foundry.paradigm.xyz | bash
```

Then, in a new terminal session (or after reloading your `PATH` environmental variable), run `foundryup` to get the latest `forge` and `cast` binaries:

``` console
foundryup
```

And finally, install the repository's dependencies by entering it and running:

``` console
forge install
```

Note that you might have to restart your terminal for the `forge` command to become available.

At this point you should be all set. If not, check [`Foundry`'s installation troubleshooting](https://github.com/foundry-rs/foundry#troubleshooting-installation).

### **Solving a challenge**

Challenge contracts are located under the `foundry_flavor/src/` directory. **Do not** modify them, as it may lead to unexpected behaviors within the challenges.

To solve a challenge, you must open the corresponding `foundry_flavor/test/ChallengeX.t.sol` *(where X is a number)* and add your exploit code in the signalized areas within said file.

Then, to check if the challenge has been solved, execute the following command

``` bash
forge test --match-path test/ChallengeX.t.sol
```

If the solution criteria have been reached, it shall display the following message

``` bash
Running 1 test for test/ChallengeX.t.sol:ChallengeXTest
[PASS] testChallenge() (gas: XXXX)
Test result: ok. 1 passed; 0 failed; finished in XXXms
```

Alternatively, to check if all challenges have been solved, execute the following command:

``` bash
bash isSolved.sh
```

which will return the test results for all challenges in order.

----------

## Important note

This set of challenges aren't set for competitive purposes. Their main objective is to showcase scenarios involving DeFi, `Solidity` concepts and common vulnerabilities.

Focus on **learning** and having **fun**! 😊

------------------------------

🔗 [Access the repository's main `README` file containing the challenges' descriptions](https://github.com/eugenioclrc/DeFi-Security-Summit-Stanford/tree/master/).

## Solution

Let's begin with a simple warm up.
Our beloved Vitalik is the proud owner of **100 $VTLK**, which is a token that follows the ERC20 token standard. Or at least that is what it seems... 😉😉😉

📌 Upon deployment, the `VToken` contract mints **100 $VTLK** to Vitalik's address.

Is there a way for you to **steal** those tokens from him? 😈😈😈

<details>
<summary>🗒️ <i>Concepts you should be familiar with (spoilers!)</i></summary>
    <ul>
    <li><i><a href=https://ethereum.org/en/developers/docs/standards/tokens/erc-20>The ERC20 token standard</a>, especially the meaning of approving funds.</i></li>
    </ul>
</details>

-----------
**The contracts that you will hack are**:

-  **[VToken](https://github.com/eugenioclrc/DeFi-Security-Summit-Stanford/blob/master/challenges_sources/Challenge0.VToken.sol)**

-----------
## **Challenge 1: What a nice Lender Pool!**

Secureum has raised a lot of Ether and decided to buy a bunch of
`InSecureumToken`s (**$ISEC**) in order to make them available to the community
via flash loans. This is made possible by means of the `InSecureumLenderPool` contract.

📌 Upon deployment, the `InSecureumToken` contract mints an initial supply of 10 **$ISEC** to the contract deployer.

📌 The `InSecureumLenderPool` contract operates with **$ISEC**.

📌 The contract deployer transfers all of their **$ISEC** to the `InSecureumLenderPool` contract.

📌 The idea is that anyone can deposit **$ISEC**s to enlarge the pool's resources.

Will you be able to **steal** the **$ISEC**s from the `InSecureumLenderPool`? 😈😈😈

<details>
<summary>🗒️ <i>Concepts you should be familiar with (spoilers!)</i></summary>
    <ul>
    <li><i>The concept of <a href=https://blog.chain.link/flash-loans>flashloans</a>. Focus on the definition, how they work and what's their original purpose.</i></li>
    <li><i>Solidity's <a href=https://medium.com/coinmonks/delegatecall-calling-another-contract-function-in-solidity-b579f804178c>delegatecall</a>.</i></li>
    </ul>
</details>

-----------
**The contracts that you will hack are**:

- **[InSecureumLenderPool](https://github.com/eugenioclrc/DeFi-Security-Summit-Stanford/blob/master/challenges_sources/Challenge1.lenderpool.sol)**

**Which have interactions with the following contracts:**

- **[InSecureumToken](https://github.com/eugenioclrc/DeFi-Security-Summit-Stanford/blob/master/challenges_sources/tokens/tokenInsecureum.sol)**

-----------

## **Challenge 2: it's always sunny in decentralized exchanges**

I bet you are familiar with **decentralized exchanges**: a magical place where one can exchange different tokens.\
`InsecureDexLP` is exactly that: a <s>very insecure</s> Uniswap-kind-of decentralized exchange.\
Recently, the **$ISEC** token got listed in this dex and can be traded against a *not-so-popular* token called **$SET**.

📌 Upon deployment, the `InSecureumToken` and `SimpleERC223Token` contracts mint an initial supply of tokens 10 **$ISEC** and 10 **$SET** to the contract deployer.

📌 The `InsecureDexLP` operates with **$ISEC** and **$SET**.

📌 The dex has an initial liquidity of 9 **$ISEC** and 9 **$SET**, provided by the contract deployer. This quantity can be increased by anyone through token deposits.

📌 Adding liquidity to the dex rewards liquidity pool tokens (LP tokens), which can be redeemed in any moment for the original funds.

📌 In the `foundry` implementation, the deployer graciously airdrops the challenger (*you!*) 1 **$ISEC** and 1 **$SET**. In the `TenderlySandbox` implementation, the challenger must call the exclusive `claimAirdrop()` functions of each of the token contracts, obtaining this way 1 **$ISEC** and 1 **$SET**.

Will you be able to **drain** most of `InsecureDexLP`'s **$ISEC**/**$SET** liquidity? 😈😈😈

<details>
<summary>🗒️ <i>Concepts you should be familiar with (spoilers!)</i></summary>
    <ul>
    <li><i>The concept of <a href=https://research.paradigm.xyz/amm-price-impact>Automatic Market Makers (AMMs)</a>. Focus on the constant-product formula.</i></li>
    <li><i><a href=https://www.blockchain-council.org/ethereum/ethereum-tokens-erc-20-vs-erc-223-vs-erc-777>Other token standards</a> such as ERC223. Focus on the fallback function provided in ERC223.</i></li>
    <li><i>The concept of <a href=https://www.certik.com/resources/blog/3K7ZUAKpOr1GW75J2i0VHh-what-is-a-reentracy-attack>reentrancy attack</a>.</i></li>
    </ul>
</details>

-----------
**The contracts that you will hack are**:

- **[InsecureDexLP](https://github.com/eugenioclrc/DeFi-Security-Summit-Stanford/blob/master/challenges_sources/Challenge2.DEX.sol)**

**Which have interactions with the following contracts:**

- **[InSecureumToken](https://github.com/eugenioclrc/DeFi-Security-Summit-Stanford/blob/master/challenges_sources/tokens/tokenInsecureum.sol)**
- **[SimpleERC223Token](https://github.com/eugenioclrc/DeFi-Security-Summit-Stanford/blob/master/challenges_sources/tokens/tokenERC223.sol)**

----------------
## **Challenge 3: borrow, hide and seek**

Finally, as a conclusion to this <s>not-so-secure</s> ecosystem, the Secureum team built the `BorrowSystemInsecureOracle` lending platform where one can borrow and loan **$ISEC** and `BoringToken` (**$BOR**). Both tokens can be borrowed by either providing themselves or the other token as collateral.

📌 Upon deployment, the `InSecureumToken` and `BoringToken` contracts mint an initial supply of 30000 **$ISEC** and 20000 **$BOR** to the contract deployer.

📌 `BorrowSystemInsecureOracle` uses the `InsecureDexLP` to compute the **$ISEC**/**$BOR** price.

📌 The deployer adds an initial liquidity of 100 **$ISEC** and 100 **$BOR** to the `InsecureDexLP`.

📌 Similarly, `InSecureumLenderPool` contract is funded with 10000 **$ISEC** by the deployer.

📌 The `BorrowSystemInsecureOracle` contract has an initial amount of 10000 **$ISEC** and 10000 **$BOR** provided by the deployer.

📌 Users can add collateral and take loans from `BorrowSystemInsecureOracle`.

📌 Users may also get liquidated.



Will you be able to **drain** all the **$ISEC** from `BorrowSystemInsecureOracle`? 😈😈😈

<details>
<summary>🗒️ <i>Concepts you should be familiar with (spoilers!)</i></summary>
    <ul>
    <li><i><a href=https://blog.yield.app/post/defi-lending-and-borrowing-guide>How DeFi lending works</a>.</i></li>
    <li><i>The concept of <a href=https://blog.chain.link/flash-loans>price oracle attack</a>. Notice that this concept is very related to flashloans.</i></li>
    </ul>
</details>

-----------
**The contracts that you will hack are**:

- **[BorrowSystemInsecureOracle](https://github.com/eugenioclrc/DeFi-Security-Summit-Stanford/blob/master/challenges_sources/Challenge3.borrow_system.sol)**

**Which have interactions with the following contracts:**

- **[InSecureumLenderPool](https://github.com/eugenioclrc/DeFi-Security-Summit-Stanford/blob/master/challenges_sources/Challenge1.lenderpool.sol)** *(this contract should be used by the attacker as part of the attack)*
- **[InsecureDexLP](https://github.com/eugenioclrc/DeFi-Security-Summit-Stanford/blob/master/challenges_sources/Challenge2.DEX.sol)**
- **[InSecureumToken](https://github.com/eugenioclrc/DeFi-Security-Summit-Stanford/blob/master/challenges_sources/tokens/tokenInsecureum.sol)**
- **[BoringToken](https://github.com/eugenioclrc/DeFi-Security-Summit-Stanford/blob/master/challenges_sources/tokens/tokenBoring.sol)**

-----------

## CTF Writeup 🗒️🗒️🗒️

Follow [this link](https://ventral.digital/posts/2022/8/27/secureum-a-maze-x-stanford-ctf) to access this CTF's writeup by [patrickd](https://github.com/patrickd-).

-----------
