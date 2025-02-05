# Emergency Shutdown

## What is an Emergency Shutdown?

One important security feature of Dai is called Emergency Shutdown, formerly known as Global Settlement. This crucial security feature allows the system to shut down and make underlying collateral available for redemption by [Dai](dai.md) holders and CDP owners.

## What happens during an Emergency Shutdown?

1. Emergency Shutdown is activated:
   If MKR voters believe that the system is subject to a serious attack, or if an Emergency Shutdown is scheduled as part of a technical upgrade, they can activate an Emergency Shutdown. This stops CDP creation and freezes the Price Feed.
2. Collateral Claims are processed:
   After Emergency Shutdown is activated, a time period is needed to allow the processing of the proportional collateral claims of all CDP owners. After this processing is done, all CDP owners will be able to claim a fixed amount of ETH with their CDPs. Dai holders can access their collateral claims immediately.
3. Dai and CDP owners claim collateral:
   Each Dai holder and CDP owner can exchange their Dai and CDPs directly for a fixed amount of ETH that corresponds to the calculated value of their assets.

## Who can Trigger an Emergency Shutdown?

The only way to trigger Emergency Shutdown in Single Collateral Dai is for MKR voters to pass an [Executive Vote](governance.md#is-there-more-than-one-type-of-vote).

## When should Emergency Shutdown be used?

Emergency Shutdown may be used in the cases of attacks on the system, significant economic issues, and for major upgrades.

Examples of attacks on the system include hacking or security breaches of the smart contracts and manipulation of the Oracles.

Examples of significant economic issues include the scenario of a severely broken peg (as decided by MKR voters), and other market conditions if they pose a significant and real threat to a majority of users.

An example of a major technical upgrade that will warrant an Emergency Shutdown is the upgrade to Multi Collateral Dai, as a method to shut down Single Collateral Dai after the transition period.

## Does hitting the Debt Ceiling warrant an Emergency Shutdown?

Hitting the Debt Ceiling marks the moment where new Dai cannot be generated by CDP owners. This is not an immediate threat to the stability of the system. However, if the ceiling is not lifted it may cause a supply and demand imbalance of Dai by allowing demand to outpace the limited supply. This problem can be fixed by raising the debt ceiling, therefore it is not necessary to perform an Emergency Shutdown on the system. Emergency Shutdown is a very disruptive process and should only be used in cases of last resort and planned upgrades.

## Will the redemption of collateral for CDPs and Dai be immediate and automatic, or a manual process?

The redemption of collateral claims will occur manually.

Dai holders will be able to redeem collateral immediately after the Emergency Shutdown. CDP owners need to wait for a 6 hour time period while their claims are processed before they can redeem their collateral.

## Why is there a time period before CDP owners can redeem collateral?

Calculating CDP claims involves on-chain calculation and movement of funds. Processing may take a long time depending on the congestion on the network, therefore the default time period is set to 6 hours. This delay period is also a precaution for unknown circumstances that may arise.

## Can MKR voters set the collateral claim processing time period to 0?

Setting a shorter time period will expose CDP owners to the risk of incorrect collateral claim amounts. CDP owners who try to close their CDPs and exit from PETH to WETH before the processing is finished will likely penalize themselves, the delay period is intended to protect them.

When Emergency Shutdown happens WETH is taken from collection of WETH that is pooled into PETH, to cover Dai holders. This lowers the PETH ratio. If a user tries to convert their PETH into WETH during the Emergency Shutdown's 6 hour delay period they may be subject to an artificially low PETH ratio.

## Do Dai holders need to redeem collateral, or is it just CDP owners?

Both CDP owners and Dai holders need to redeem collateral. However, only Dai holders can redeem ETH immediately after the Emergency Shutdown is triggered. CDP owners need to wait the 6 hour time period.

## What do I do in the case of an Emergency Shutdown if I'm a PETH holder who does not own a CDP?

The PETH ratio drops instantaneously when an Emergency Shutdown is triggered and comes back up as CDPs are processed. PETH holders should wait the 6 hour delay period like CDP owners.

## If the prices keep falling after the price feeds are frozen, doesn't this mean that people redeeming Dai and CDPs may get less than \$1 of collateral?

Yes, it is possible for users to get less than a dollar worth of collateral. Dai holders are able to immediately redeem their Dai for collateral and may experience some slippage. CDP owners must wait the 6 hour delay period for claims to be calculated and are therefore exposed to the risk of the underlying collateral price moving during these 6 hours.

## How quickly can an Emergency Shutdown be performed?

To trigger an Emergency Shutdown, an Executive Vote needs to be voted on by MKR voters. The proposal needs to garner enough MKR until it beats the previous proposal, in line with [continuous approval voting](governance.md#what-is-continuous-approval-voting). Therefore, it depends on how quickly MKR voters can act to beat the previous winning proposal.

## What happens to MakerDAO after an Emergency Shutdown?

After Emergency Shutdown is triggered, the collateral redemption process takes place. In the meantime, it is up to anyone whether they want to redeploy the system or not, and how they would deploy it.

## Who can redeploy the system?

Anyone can redeploy the system since it is open source software.

## What if multiple redeployments happen, who decides which one is legitimate?

Depending on the details of each redeployment, the market, along with various system participants will have to choose the one with the most appropriate changes. Some factors include:

- No unwarranted code changes
- Changes in the distribution of the MKR token
- Changes in the Risk Parameters

## Who decides how the system should be redeployed?

Since it is open source software, anyone can decide. Ideally, the parameters of redeployment should depend on the reason for the Emergency Shutdown, and should not be altered unilaterally and arbitrarily. Here is a rough example of a framework for making changes on redeployment:

| Reason            | Solution                                                                                                                                                                      |
| ----------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Governance attack | Fork out malicious MKR holders in new redistribution, redeploy system with everything else as-is                                                                              |
| Oracle Attack     | Fork out Oracle module for a new one with a vulnerability fix, redeploy system with everything else as-is                                                                     |
| Market Black Swan | Redeploy system with everything as-is, allow MKR voters to decide how best to address this event through new or improved system mechanics that can be added post-redeployment |

## During Emergency Shutdown, will CDP owner's collateral be given away to other people?

During Emergency Shutdown, collateral is immediately made available for redemption by Dai holders. This means that someone may receive a part of your original collateral. However, after the time period where CDP collateral claims are processed, any CDP owner will be able to withdraw collateral that represents the full net value of their CDP.

Example:

> If you have a CDP with 1 ETH that's worth 300 USD, and 100 debt, you will be left with 0.6666 ETH and no debt.
> The Net Value of the CDP is made available for redemption, which is 300 USD value of the collateral, minus 100 USD of debt.
> Therefore, you will be able to claim 0.6666 ETH after the 6 hour delay period.

## Is there anything preventing MKR holders from triggering an Emergency Shutdown in order to avoid MKR dilution due to poor management?

MKR holders, especially large ones, are incentivized to preserve the value of their MKR. Voting to perform an Emergency Shutdown on the system because of the fear of imminent dilution may harm the value of their MKR. It also puts their MKR ownership at risk, as anyone can redeploy the system and change the token distribution of MKR. Therefore, this is a very risky attack vector.

## Can I create a CDP during an Emergency Shutdown?

No.

## What happens to inaccessible CDPs and Dai that has been lost, stuck or is dust?

Any Dai or CDPs that have been stuck or lost will remain so afterward, they will effectively be stuck or lost ETH instead.

## Are Stability Fees waived in the event of an Emergency Shutdown?

Stability Fees are not paid in an Emergency Shutdown, but governance can enact an "Emergency Shutdown Penalty" that will ensure that anyone who holds their CDP through Emergency Shutdown rather than migrating it to MCD will have to pay a higher penalty, meaning that it is always cheaper to migrate your CDP and pay the stability fee.

## Has an Emergency Shutdown ever been performed in the past?

Yes, an Emergency Shutdown has been [performed](https://www.reddit.com/r/MakerDAO/comments/7lhbmx/psa_sai_now_globally_settled/) on the Sai system, before Single Collateral Dai.

## How was testing for Emergency Shutdown done?

Emergency Shutdown was originally introduced and tested with the Sai prototype deployments. Besides the tests in [the code](https://github.com/makerdao/sai/blob/master/src/sai.t.sol) itself, there were three live runs, all of which happened on deployments of the Sai prototype on the Ethereum Mainnet.

## How will CDP users and Dai holders be notified of Emergency Shutdown?

There will be notices within all official Maker front-ends, as well as announcements on our blog and on all our official communication channels like Twitter, Reddit, Medium, Rocketchat, Telegram, WeChat, and Kakaotalk.
