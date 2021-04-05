---
title: YouBank
tags: smart-contracts, documentation
---

# Code

[`YouBank.sol`](https://github.com/ixc-software/CRAD-DeFi/blob/master/v2.0/poolRegistry/contracts/YouBank.sol)

# Address 
// Where can I find this info for the current contract?

`UniswapV2Factory` is deployed at `0x5C69bEe701ef814a2B6a3EDD4B1652CB9cc5aA6f` on the Ethereum [mainnet](https://etherscan.io/address/0x5C69bEe701ef814a2B6a3EDD4B1652CB9cc5aA6f), and the [Ropsten](https://ropsten.etherscan.io/address/0x5C69bEe701ef814a2B6a3EDD4B1652CB9cc5aA6f), [Rinkeby](https://rinkeby.etherscan.io/address/0x5C69bEe701ef814a2B6a3EDD4B1652CB9cc5aA6f), [Görli](https://goerli.etherscan.io/address/0x5C69bEe701ef814a2B6a3EDD4B1652CB9cc5aA6f), and [Kovan](https://kovan.etherscan.io/address/0x5C69bEe701ef814a2B6a3EDD4B1652CB9cc5aA6f) testnets. It was built from commit [8160750](https://github.com/Uniswap/uniswap-v2-core/tree/816075049f811f1b061bca81d5d040b96f4c07eb).

# Overview

The `YouBank` contract is derived from `TeamRole` and `IRoleModel` contracts.

# Events

## CreatePool

```solidity
event CreatePool(address pool);
```

Emitted each time a new investment pool is created via [createPool](#createpool). Uses the address of the contract that creates the Investment Pool.

* `pool`: The address Investment Pool. See [Pools](https://uniswap.org/docs/v2/core-concepts/pools/) for details.

## AddPool

```solidity
event AddPool(address pool);
```

Emitted each time a new investment pool is added via [addPool](#addpool).

* `pool`: The address Investment Pool.

## UpdatePool

```solidity
event UpdatePool(address pool);
```

Emitted each time an existing investment pool is updated via [createPool](#createpool).

* `pool`: The address Investment Pool.

## DepositTokenToPool

```solidity
event DepositTokenToPool(address pool, uint256 amount);
```

Emitted each time a deposit token is set for Investment Pool via [depositTokenToPool](#deposittokentopool).

* `pool`: The address Investment Pool.
* `amount` - amount of deposit tokens.

## WithdrawToStartupTeam

```solidity
event WithdrawToStartupTeam(address pool, uint256 amount);
```

Emitted each time a main network coin (ETH,BNB) is withdrawn from Investment pool to `STARTUP_TEAM` via [withdrawToStartupTeam](#withdrawtostartupteam). 

* `pool`: The address Investment Pool.
* `amount`: Amount of withdraw main network coin (ETH,BNB).

## WithdrawLPartner

```solidity
event WithdrawLPartner(address pool, address lPartner, bool result);
```

Emitted each time an investment pool is returned via [withdrawLPartner](#withdrawlpartner).

* `pool`: The address Investment Pool.
* `lPartner`: Address to confirm the request.

## DepositToPool

```solidity
event DepositToPool(address sender, uint256 amount);
```

Emitted each time a main network coin (Eth, BNB) is deposited for Investment Pool via [depositToPool](#deposittopool).

## ReturnsFromStartupTeam 

```solidity
event ReturnsFromStartupTeam(address sender, uint256 amount);
```

Emitted each time a main network coin (ETH,BNB) is returned to investment pool from team via [returnsFromStartupTeam](#returnsfromstartupteam).

## SetPoolValues

```solidity
event SetPoolValues(address pool,uint256 poolValueUSD, uint256 poolValue, string proofOfValue, bool result);
```

Emitted each time the Investigation Pool values are set up via [setPoolValues](#setpoolvalues).

* `pool`: The address Investment Pool.

## DepositInvestmentInTokensToPool

```solidity
event DepositInvestmentInTokensToPool(address pool, uint256 amount, address token);
```

Emitted each time an investment is deposited in tokens for Investment Pool via [depositInvestmentInTokensToPool](#depositinvestmentintokenstopool).

* `pool`: The address Investment Pool.

## WithdrawInTokensToStartupTeam

```solidity
event WithdrawInTokensToStartupTeam(address pool, uint256 amount, address token);
```

Emitted each time a main network coin (ETH,BNB) is withdrawn from Investment pool `STARTUP_TEAM` via [withdrawInTokensToStartupTeam](#withdrawintokenstostartupteam).

* `pool`: The address Investment Pool.

## ReturnsInTokensFromTeam

```solidity
event ReturnsInTokensFromTeam(address pool, uint256 amount, address token);
```
Emitted each time tokens (BUSD,USDT) are returned to investment pool from team via [returnsInTokensFromTeam](#returnsintokensfromteam).

* `pool`: The address Investment Pool.

## ClaimFreeTokens

```solidity
event ClaimFreeTokens(address pool, uint256 amount, address investor, bool result);
```

Emitted each time the ubank tokens are claimed from via [claimFreeTokens](#claimfreetokens).

* `pool`: The address Investment Pool.


# Management Pool Functions

## createPool

```solidity
function createPool(string memory name, uint256 lockPeriod, uint256 depositFixedFee, uint256 referralDepositFee, uint256 anualPrecent, uint256 penaltyEarlyWithdraw, address superAdmin, address gPartner, address lPartner, address startupTeam) public onlyTeam returns (bool);
```

Creates new Investment Pool. Returns a boolean that indicates if the operation was successful.

 * `name`: name
 * `lockPeriod`: The blocking period of assets.
 * `depositFixedFee`: A main network coin (ETH,BNB) deposit commission LPartner.
 * `referralDepositFee`: Referral commission.
 * `anualPrecent`: The annual percentage of tokens.
 * `superAdmin`: The address that has privileges `SUPER_ADMIN_ROLE`.
 * `gPartner`: The address that has privileges `GENERAL_PARTNER_ROLE`.
 * `lPartner`: The address that has privileges `LIMITED_PARTNER_ROLE`.
 * `startupTeam`: The address that has privileges `TEAM_ROLE`.

## addPool

```solidity
function addPool(address poolAddress) public onlyTeam returns (bool);
```

Adds a new smart contract Investment Pool. Returns a boolean that indicates if the operation was successful.

* `poolAddress`: The address Investment Pool.

## updatePool

```solidity
unction updatePool(address pool, string memory name, bool publicPool, address token, uint256 locked, uint256 depositFixedFee, uint256 referralDepositFee, uint256 anualPrecent, uint256 penaltyEarlyWithdraw) public onlyTeam returns (bool); 
```

Updates a smart contract Investment Pool. Returns a boolean that indicates if the operation was successful.

* `token`: The address token contract.
* `locked`: The address to query the wager of.
* `depositFixedFee`: Commission from the deposit Limited Partner.
* `referralDepositFee`: Commission from the deposit if the limited partner has a referral.
* `anualPrecent`: The annual percentage of tokens.
* `penaltyEarlyWithdraw` The penalty for early withdraw.
     
## setPriceToken

```solidity
function setPriceToken(address pool, uint256 rate) external onlyTeam returns (bool);
```

Sets price token for One. (POOL REGISTRY). Returns a boolean that indicates if the operation was successful.

* `rate`: Sets a new price token to Wei.


# Asset Manage Team Functions

## depositTokenToPool

```solidity
function depositTokenToPool(address pool, uint256 amount) public returns (bool);
```

Sets a deposit token for Investment Pool. Returns a boolean that indicates if the operation was successful.

* `pool`: The address Investment Pool.
* `amount`: Amount of deposit tokens.

## withdrawToStartupTeam

```solidity
function withdrawToStartupTeam(address pool, uint256 amount) public returns (bool);
```

 Withdraws a main network coin (ETH,BNB) from Investment pool to STARTUP_TEAM. Returns A boolean that indicates if the operation was successful.

* `pool`: The address Investment Pool.
* `amount`: Amount of withdraw main network coin (ETH,BNB).
     
## requestStartupTeam

```solidity
function requestStartupTeam(bool withdraw, address pool, uint256 maxValue) public returns (bool);
```

Creates a request to deposit token or withdraw main network coin (ETH,BNB). Return A boolean that indicates if the operation was successful.
     
* `withdraw`: Boolean value to indicate the type of request.
* `pool`: The address Investment Pool.
* `maxValue`: Maximum possible deposit.

## approveReqStartupTeam

```solidity
function approveReqStartupTeam(address pool, address team) public returns (bool);
```

Approves a request to deposit token or withdraw main network coin (ETH,BNB). Returns a boolean that indicates if the operation was successful.

* `pool`: The address Investment Pool.
* `team`: Address to confirm the token deposit.

## disapproveReqStartupTeam

```solidity
function disapproveReqStartupTeam(address pool, address team) public returns (bool);
```

Disapproves a request to deposit a token or withdraw main network coin (ETH,BNB). Returns a boolean that indicates if the operation was successful.

* `pool`: The address Investment Pool.
* `team`: Address to disapprove the token deposit.

## lockStartupTeam

```solidity
function lockStartupTeam(address pool, address team) public returns (bool);
```

Locks a deposit or withdraw main network coin (ETH,BNB) for startup team address. Returns a boolean that indicates if the operation was successful.

* `pool`: The address Investment Pool.
* `team`: Address to lock token deposit or withdraw main network coin (ETH,BNB).

## unlockStartupTeam

```solidity
function unlockStartupTeam(address pool, address team) public returns (bool);
```

Unlocks a deposit or withdraw main network coin (ETH,BNB) for startup team address. Returns A boolean that indicates if the operation was successful.

* `pool`: The address Investment Pool.
* `team`: Address to unlock token deposit or withdraw main network coin (ETH,BNB).

## getDepositPool

```solidity
function getDepositPool(address pool, address owner, uint256 index) public view returns (uint256 amount, uint256 time, uint256 lock_period, bool refund_authorize, uint256 amountWithdrawal, uint256 lenghtDeposit, address investedToken);
```

Retrieves information about the user who made a deposit ETH. 

* `pool`: The address Investment Pool.
* `owner`: The address investor pool.
* `index`: The owner's deposit index.

## getPerformedOperationsTeamStartup

```solidity
 function getPerformedOperationsTeamStartup(address pool, address owner, uint256 index) public view returns (address token, uint256 amountToken, uint256 withdrawAmount, uint256 time);
```

Retrieves information about the user who made a depositToken or withdraw main network coin (ETH,BNB).

* `pool`: The address Investment Pool.
* `owner`: The address investor pool.
* `index`: The owner's deposit index.

## getRequestsTeam

```solidity
function getRequestsTeam(address pool) public view returns (address[] memory);
```

Retrieves all addresses that made a requests for a token deposit or withdraw.

* `pool`: The address Investment Pool.

## getApprovalReqTeam

```solidity
function getApprovalReqTeam(address pool) public view returns (address[] memory);
```

Get all addresses that made a approve for a token deposit or withdraw.

* `pool`: The address Investment Pool.

## getRequestTeamAddress

```solidity
function getRequestTeamAddress(address pool, address team) public view returns (bool lock, uint256 maxValueToken, uint256 madeValueToken, uint256 maxValue, uint256 madeValue);
```
Get request information for team address.

* `pool`: The address Investment Pool.
* `team`: The address team account.

## getApproveTeamAddress

```solidity
function getApproveTeamAddress(address pool, address team) public view returns (bool lock, uint256 maxValueToken, uint256 madeValueToken, uint256 maxValue, uint256 madeValue);
```

Gets approve information for team address.

* `pool`: The address Investment Pool.
* `team`: The address team account.


# Referral Functions

## setReferral

```solidity
function setReferral(address pool, address lPartner, address referral) public returns (bool);
```

Adds a referral LPartner. Returns A boolean that indicates if the operation was successful.
     
* `pool`: The address Investment Pool.
* `lPartner`: Address to confirm the request.
* `referral`: The address referral LPartner.

## getReferral

```solidity
function getReferral(address pool, address lPartner) public view returns (address);
```

Gets address referal for LPartner.

* `pool`: The address Investment Pool.
* `lPartner`: Address to confirm the request.

# Returnes Investment Functions 

## requestReturnInvestmentLpartner

```solidity
function requestReturnInvestmentLpartner(address pool, uint256 index, uint256 amount, address token) public returns (bool);
```

Creates a request for a return investment Limited partner. Returns a boolean that indicates if the operation was successful.

* `pool`: The address Investment Pool contract.
* `index`: Investment index.
* `amount`: Investment amount.


## approveReturnInvestmentLpartner

```solidity
function approveReturnInvestmentLpartner(address pool, address lPartner) public returns (bool);
```

Approves of a request for return investment. Returns a boolean that indicates if the operation was successful.

* `pool`: The address Investment Pool contract.
* `lPartner`: Address to confirm the request.


## withdrawLPartner

```solidity
function withdrawLPartner(address pool) public returns (bool);
```

Withdraws an investment pool. Indicates if the operation was successful.

* `pool`: The address Investment Pool contract.


## disapproveReturnInvestmentLpartner

```solidity
function disapproveReturnInvestmentLpartner(address pool, address lPartner) public returns (bool);
```
 
Disapproves of a request for return investment. Returns a boolean that indicates if the operation was successful.

* `pool`: The address Investment Pool contract.
* `lPartner`: Address to confirm the request.

## getAddrRequestsReturnInvesLpartner

```solidity
function getAddrRequestsReturnInvesLpartner(address pool) public view returns (address[] memory);
```

Retrieves all requests.

* `pool`: An address investment pool contract.


## getRequestsReturnInvestLpartner

```solidity
function getRequestsReturnInvestLpartner(address pool, address lPartner) public view returns (uint256[] memory);
```

Retrieves all requests of current LPartner.

* `pool`: address investment pool contract.
* `lPartner`: address limited parner role.

## getInvestedFunds

```solidity
function getInvestedFunds(address token) public view returns (uint256);
```

Retrieves the invested funds.

* `token`: address for asstet (address(0) for ETH/BNB).


## getReturnedFunds

```solidity
function getReturnedFunds(address token) public view returns (uint256);
```

Retrieves the returned Funds.

* `token`: address for asset (address(0) for ETH/BNB).

## feesMulitpier

```solidity
function feesMulitpier(address sender) public view returns (uint256)
```

## depositToPool

```solidity
function depositToPool(address payable pool) public payable returns (bool);
```

Deposites the main network coin (ETH,BNB) for Investment Pool. Returnes a boolean that indicates if the operation was successful.

* `pool`: The address Investment Pool.

## returnsFromStartupTeam

```solidity
function returnsFromStartupTeam(address payable pool) public payable returns (bool);
```

Returns main network coin (ETH,BNB) to investment pool from team. Indicates if the operation was successful.

* `pool`: The address Investment Pool.

## activateDepositToPool

```solidity
function activateDepositToPool(address pool) public onlyTeam returns (bool);
```

Allows main network coin (ETH,BNB) deposit to investment pool. Returns a boolean that indicates if the operation was successful.

* `pool` The address Investment Pool.


## disactivateDepositToPool

```solidity
function disactivateDepositToPool(address pool) public onlyTeam returns (bool)
```

Disallows main network coin (ETH,BNB) deposit to investment pool. Returns a boolean that indicates if the operation was successful.

* `pool`: The address Investment Pool.


## grantRoleInvestmentPool

```solidity
function grantRoleInvestmentPool(address pool, bytes32 role, address account) public returns (bool);
```

Grants role to account. Returns A boolean that indicates if the operation was successful.

* `pool`: The address Investment Pool.
* `role`: Role account.
* `account`: The address for grant role.


## revokeRoleInvestmentPool

```solidity
function revokeRoleInvestmentPool(address pool, bytes32 role, address account) public returns (bool);
```

Revokes role to account. Returns boolean that indicates if the operation was successful.

* `pool`: The address Investment Pool.
* `role`: Role account.
* `account`: The address for grant role.


## setAddressCreatorInvestPool

```solidity
function setAddressCreatorInvestPool(address creatorContract) public onlyTeam returns (bool);
```

Sets the address of the contract creating Investment Pools. Returns a boolean that indicates if the operation was successful.
     
* `creatorContract`: The address creator pool.

## setAssetManageTeamContract

```solidity
function setAssetManageTeamContract(IAssetsManageTeam addrContract) public onlyTeam returns (bool);
```

Sets address `assetManageTeam` contract. Returns a boolean that indicates if the operation was successful.

* `addrContract`: The address AssetManageTeam contract.


## setReturnInvestmentLpartner

```solidity
function setReturnInvestmentLpartner(IReturnInvestmentLpartner addrContract) public onlyTeam returns (bool);
```

Sets address `ReturnInvestmentLpartner` contract. Returns a boolean that indicates if the operation was successful.
     
* `addrContract`: The address ReturnInvestmentLpartner contract.
     

## setOracleContract

```solidity
function setOracleContract(IOracle _oracle) public onlyTeam returns (bool);
```

Sets address `Oracle` contract. Returns a boolean that indicates if the operation was successful.

* `_oracle`: The address Oracle contract.
    

## getPools

```solidity
function getPools() public view returns (address[] memory);
```

Retrieves all Investment Pool addresses.

## getInfoPool

```solidity
function getInfoPool(address pool) public view returns (string memory name, bool isPublicPool, address token, uint256 locked);
```

Retrieves information about the Investment Pool.

* `pool`: The address Investment Pool.

## getInfoPoolFees

```solidity
function getInfoPoolFees(address pool) public view returns (uint256 rate, uint256 depositFixedFee, uint256 referralDepositFee, uint256 anualPrecent, uint256 penaltyEarlyWithdraw, uint256 totalInvestLpartner, uint256 premiumFee);
```

Retrieves information about the Investment Pool.

* `pool`: The address Investment Pool.

## getAssetManageTeamContract

```solidity
function getAssetManageTeamContract() public view returns (IAssetsManageTeam);
```

Retrieves address TokenRequestContract.

## getReturnInvesmentLpartner

```solidity
function getReturnInvesmentLpartner() public view returns (IReturnInvestmentLpartner);
```

Retrieves address TokenRequestContract.

## getOracleContract

```solidity
function getOracleContract() public view returns (IOracle);
```

Retrieves address OracleContract.

## getAddressesRolesPool

```solidity
function getAddressesRolesPool(address pool, bytes32 role) public view returns (address[] memory);
```
Retrieves all addresses for role.
     
* `pool`: The address Investment Pool.
* `role`: Role accounts.

## getAddressCreatorInvestPool

```solidity
function getAddressCreatorInvestPool() public view returns (address);
```

Retrieves address contract creator Invest pool.

## getPoolValues

```solidity
function getPoolValues(address pool) public view returns (uint256 poolValueUSD, uint256 poolValue, string memory proofOfValue, uint256 poolValuesTotal, uint256 poolValuesUSDTotal);
```

Retrieves Investigation Pool values.

* `pool`: The address Investment Pool.


## setPoolValues

```solidity
function setPoolValues(address pool, uint256 poolValueUSD, uint256 poolValue, string memory proofOfValue) public returns (bool);
```

Sets the Investigation Pool values.

* `pool`: The address Investment Pool.
* `poolValueUSD`: Investment Pool Value (USD).

## depositInvestmentInTokensToPool 

```solidity
function depositInvestmentInTokensToPool(address pool, uint256 amount, address token) public returns (bool);
```

Deposits an investment in tokens for Investment Pool. Returns a boolean that indicates if the operation was successful.

* `pool`: The address Investment Pool.
* `amount`: Amount of deposit tokens.
* `token`: address of deposited tokens.

## withdrawInTokensToStartupTeam

```solidity
function withdrawInTokensToStartupTeam(address pool,address token, uint256 amount) public returns (bool);
```

Withdraws a main network coin (ETH,BNB) from Investment pool `STARTUP_TEAM`. Returns a boolean that indicates if the operation was successful.

* `pool`: The address Investment Pool.
* `amount`: Amount of withdraw main network coin (ETH,BNB).


## requestTokensWithdwawalFromStartup

```solidity
function requestTokensWithdwawalFromStartup(address pool, address token, uint256 maxValue) public returns (bool);
```

Creates a request to withdraw any tokens (BUSD/USDT e.t.c) from Investigation Pool. Returns a boolean that indicates if the operation was successful.

* `pool`: The address Investment Pool.
* `token`: The address of token.
* `maxValue`: Maximum possible deposit.

##approveTokensWithdwawalFromStartup

```solidity
function approveTokensWithdwawalFromStartup(address pool, address token, address team) public returns (bool);
```

Creates a request to withdraw any tokens (BUSD/USDT etc.) from pool. Returns a boolean that indicates if the operation was successful.

* `pool`: The address Investment Pool.
* `token`: The address of token.
* `team`: The address of team.

## returnsInTokensFromTeam

```solidity
function returnsInTokensFromTeam(address payable pool,address token, uint256 amount) public returns (bool);
```

Returns tokens (BUSD,USDT) to investment pool from team. Rreturns a boolean that indicates if the operation was successful.

* `pool`: The address Investment Pool.

## withdrawSuperAdmin

```solidity
function withdrawSuperAdmin(address pool, address token, uint256 amount) public returns (bool);
```

Withdraws `SuperAdmin` investment pool. Returns a boolean that indicates if the operation was successful.

* `pool`: The address Investment Pool contract.
* `token`: The address token contract.
* `amount`: Amount of tokens.

##getCustomPrice

```solidity
function getCustomPrice(address aggregator) public view returns (uint256);
```

Retrieves address `TokenRequestContract`.

## claimFreeTokens

```solidity
function claimFreeTokens(address pool) public returns (bool);
```

Claims ubank tokens from. Returns a boolean that indicates if the operation was successful.

* `pool`: The address Investment Pool contract.



# Interface

# ABI

