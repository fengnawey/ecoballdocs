# Staking Special Topic

## Skaking system

The staking system rewards all validators essentially equally, regardless of the number of staking. Having a larger share of the pledge on a validator does not affect the amount of block rewords it receives. However, there is a probability component in the reward calculation, so the rewards may not be exactly the same for all validators at a given time.

After deducting the validator's payment, the award is distributed pro rata to all nominators. In this way, the network encourages the nomination of low-risk validators in order to create an equally risky set of validators.

The whole process of staking involves several important topics:

1. Determine the identity

You can be either the nominator or the validator when staking.

As a nominator, you may nominate one or more (up to 16) validated candidates that you trust in order to help you earn your token rewards. You can refer to the [Nominating Wizard] (# Nominating Wizard) to find out what you need to do.

The validator is required to respond 24/7, to perform the expected duties in a timely manner and to avoid any disciplinary actions.

2. Nomination period

Any potential validator can indicate their intention to become a validation candidate. Their candidacy is open to all nominator.The nominator then submits a list of any number of candidates he supports. During the next period (which lasts approximately a few hours), a certain number of validators with the most ECO support are selected and activated. There are no special requirements for an ECO holder to be a nominator, although it is expected that each nominator will carefully track the performance and reputation of the validator.

Once the nomination period is over, the XPOS election mechanism takes the nominators and their associated votes as input and outputs a set of validators of the required size in order to maximize the staking support of any validator and to distribute the staking of the supporting validators as evenly as possible. The goal of the system is to maximize online security and achieve fair representation of nominators.

3. Staking reward distribution

To explain how rewards are paid to validators and nominators, we need to consider the validator pool, where the validator pool consists of an elected validator and the nominators who support it. (Note: If a nominator N who holds a staking S supports several elected validators, such as K, the XPOS election mechanism will divide its shares into S_1, S_2,... , s_k, so that it supports validator i that holds shares s_i. In this case, nominator n will receive the same reward as if there were k nominators in a different pool, each nominator supporting a validator i with an equity s_i.) For each validator pool, we keep a list of nominators for the associated staking.

The general rule for rewards across validator pools is that two validator pools receive substantially the same ECO reward for equal work, i.e., they receive a reward that is not proportional to the staking in each pool. Staking rewards in the form of points and tips is a probabilistic factor that should become averaged over time. In the validator pool, a fixed percentage of the reward (configurable) is used to pay the validator's commission, and the rest is paid pro rata (the staking ratio) to the nominator and the validator. In particular, validators are rewarded twice: once for validation (if their commission rate is higher than 0%) and once for nominating their own staking shares.

4. Reward mechanism

Let's focus on two features of this incentive scheme. The first is that because validation pools get the same benefits, regardless of the number of staking, pools with fewer staking will typically pay more per nominator than pools with more staking. Thus, we provide financial incentives for nominators to gradually shift their preferences to lower-risk validators with sufficient reputations. The reason for this is that we want the rights to be distributed as evenly as possible across the validation pool to avoid the concentration of power among a few validators. In the long run, we expect all validation pools to have similar staking levels, with higher reputations leading to higher staking (meaning that nominators willing to take more risks by supporting less creditworthy validators will be paid more).

There is an additional factor to consider when it comes to rewards. While there is no limit to how many nominators a validator can have, there is a limit to how many nominators a validator can pay rewards. This parameter can be changed when the system is upgraded.

Another point to note is that each validation candidate is free to specify as much commission (as a percentage of the award) as they want to cover operating costs. Because validation pools pay the same amount, pools with lower commissions pay more to nominators than pools with higher commissions. Therefore, each validator can choose whether to increase their commission to earn more ECO, or reduce their commission to attract more nominators and increase their chances of being elected. We have to let the market regulate itself. In the long run, we expect that all validators will need to be cost effective to remain competitive, and that validators with a higher reputation will be able to charge slightly higher commissions (which is fair).


5. slashing

If the validator behaves strangely on the network (for example, going offline, attacking the network, or running modified software), they and their nominator will be penalized and lose a certain percentage of the money slashed. Any forfeited slashing are transferred to a temporary warehouse, and the reason for doing so (rather than directly destroying the forfeited funds or releasing them as incentives) is that the forfeited funds can be paid directly from the temporary warehouse later, as appropriate, thereby reducing losses. Because in many cases, the abnormal behavior may not be caused by the subjective error of the validator, but due to reasons such as network error or system error. At this time, the slashed money that was confiscated before should be returned. If it turns out to be the validator's fault, then the confiscated funds should be rewarded to those validators who have made contributions to ecological development.

A pool of validators with a larger total staking will be penalized more than a pool of less favored validators, so we encourage nominators to move their nominations to a less favored validator to reduce possible losses.

