# Routers Evaluation-Demo
On-chain routers Evaluation Algorithm deployed on NEAR.

* **Attention**: the testnet and mainnet of NEAR cannot be accessed in some areas.
* For convenience, we are building a version that can be accessed from **discord**. It's coming soon.  

## Prepare
### NEAR cli

* Installation: [Tutorials](https://docs.near.org/docs/tools/near-cli#installation)

### Account on NEAR testnet

* Create account on testnet: [wallet testnet](https://wallet.testnet.near.org/)
* Use the account in near cli:
```sh
near login 
```

### Contract on NEAR testnet

Contract id:

`Testnet`: ec.d-hub.testnet

## Test increase credibility
The following line simulates a router performing `10` honest jobs in a row. It will show the credibility of the router after the honest work. 
```sh
near call ec.d-hub.testnet do_honest '{"times": 10}' --accountId CALL_ACCOUNT
```

## Test decrease credibility
The following line simulates a router performing `10` malicious jobs in a row. It will show the credibility of the router after the malicious work.
```sh
near call ec.d-hub.testnet do_evil '{"times": 10}' --accountId CALL_ACCOUNT
```

## Get credibility

1、get all validators credibility

```sh
near view ec.d-hub.testnet get_credibility '{"validators": []}'
```

2、get designated validators credibility

```sh
near view ec.d-hub.testnet get_credibility '{"validators": ["ACCOUTN_1", "ACCOUNT_2"]}'
```

## Example
* Execute `near call ec.d-hub.testnet do_honest '{"times": 50}' --accountId CALL_ACCOUNT` in a row, we can get the following credibility series, the curve of which is:

![1651914035(1)](https://user-images.githubusercontent.com/83746881/167247276-a2b82eaa-8010-401b-8e27-538781016c33.png)

It's similar to the `growth trend` in the [technical white paper](https://github.com/dantenetwork/Pitch-Deck/blob/main/Dante%20Network%EF%BC%9AThe%20_Internet%20protocol%20stack_%20of%20Web3.pdf), chapter 3.2, pic-4.

* Execute `near call ec.d-hub.testnet do_evil '{"times": 50}' --accountId CALL_ACCOUNT` in a row, we can get the following credibility series, the curve of which is:

![1651914073(1)](https://user-images.githubusercontent.com/83746881/167247295-434c95f5-d421-48ec-8127-de9406f2dab1.png)

It's similar to the `reduction trend` in the [technical white paper](https://github.com/dantenetwork/Pitch-Deck/blob/main/Dante%20Network%EF%BC%9AThe%20_Internet%20protocol%20stack_%20of%20Web3.pdf), chapter 3.2, pic-4.

* Besides, we can conclude from the two series that, with a high credibility, `do_evil` will loss more than `do_honest` can earn with the same credibility.

![1651914175(1)](https://user-images.githubusercontent.com/83746881/167247352-56a77ac4-2948-47d0-b1f4-f8ccbdab7a3f.png)
