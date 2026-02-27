# Constant Sum AMM (Anchor)

Build a constant sum AMM.
Liquidity providers deposit token A and token B.
Traders can swap token A or B for the other token at 1 to 1 exchange rate.

# Tool version
anchor-cli 0.32.1
solana-cli 3.1.6

# Update program id
```shell
anchor keys sync
```

# Implement [`init_pool`]
- Check `fee` <= `constants::MAX_POOL_FEE`
- Check `mint_a.decimals` == `mint_b.decimals`
- Store Pool state

# Implement [`add_liquidity`]
- Calculate user shares to mint
- Transfer `amount_a` from user into `pool_a`
- Transfer `amount_b` from user into `pool_b`
- Mint shares to user's associated token account (`payer_liquidity`)

# Implement [`remove_liquidity`]
- Calculate the amount of token a and b to withdraw
- Check `amount_a` >= `min_amount_a`
- Check `amount_b` >= `min_amount_b`
- Burn user's shares
- Transfer `amount_a` from pool to `payer_a` (user's associated token account for token a)
- Transfer `amount_b` from pool to `payer_b` (user's associated token account for token b)

# Implement [`swap`]
- Calculate amount out with fee
- Check `amount_out` >= `min_amount_out`
- Transfer token in from user to pool
- Transfer token out from pool to user

# Build

```shell
anchor build
```

# Test
```shell
anchor test
```

