# Basic long tail example: Bean Finance

[Beanstalk](https://bean.money/docs/beanstalk.pdf) is a stablecoin protocol that uses a decentralized credit facility, variable supply and self-adjusting interest rate, to regularly cross the stablecoin price over its value peg without affecting users.

To stabilize the value of the peg and ensure 'protocol native time-keeping', there is a function `sunrise()` that can be called once a 'season' (every hour). The award for calling it starts at 100 Beans and compounds 1% every additional second that elapses past the beginning of the season for up to 300 seconds. 

This leads to a maximum extraction per hour of $1978 - gas + swap fees (if no one else calls the function for 5 minutes). 

# Strategy: Battering Ram

Send FB request to call the function every 5 seconds with high enough gas bid outprice everyone else - this requires you to be willing to burn capital up front; after denying all other bots from enough seasons, they will eventually be turned off (which you can test by delaying the call for a single block) due to node running costs. Then, wait 300 seconds before calling to maximize the `sunrise()` reward for as many blocks until the competitors return, and then repeat the Battering Ram.*

## How is this basic?

### Simple RPC
You are only interacting with Flashbots' [MEV-Relay](https://docs.flashbots.net/flashbots-auction/searchers/quick-start/). This is not a latency dependant strategy, you do not need to establish a strong node peer network. 
### No Graph Theory
You don't have to worry about any pair scanning (you do not need to fetch state of AMMs), due to the length of the rebalance period (spans over ~ 240 blocks). 
### Low Competition
This is not a highly capital intesive strategy, it does not require much modality, and you don't end up with 99% profit going to the miner. The game theory is quite clear. This op is below the caliber of interest of most bots. 
