```python
"""

		# check if the base fee is correct
		if INITIAL_FORK_BLOCK_NUMBER == block.number:
			expected_base_fee_per_gas = INITIAL_BASE_FEE
		elif parent_gas_used == parent_gas_target:
			expected_base_fee_per_gas = parent_base_fee_per_gas
		elif parent_gas_used > parent_gas_target:
			gas_used_delta = parent_gas_used - parent_gas_target
			base_fee_per_gas_delta = max(parent_base_fee_per_gas * gas_used_delta // parent_gas_target // BASE_FEE_MAX_CHANGE_DENOMINATOR, 1)
			expected_base_fee_per_gas = parent_base_fee_per_gas + base_fee_per_gas_delta
		else:
"""


INITIAL_BASE_FEE = 1000000000 ## 1 gwei
ELASTICITY_MULTIPLIER = 2
BASE_FEE_MAX_CHANGE_DENOMINATOR = 8

GAS_TARGET  = 15e6
GAS_USED = 30e6
GAS_LIMIT = 30e6

MINUTES_TO_DOS = 30
SECONDS_PER_BLOCK = 12
BLOCKS_TO_DOS = MINUTES_TO_DOS  * 60 / SECONDS_PER_BLOCK

def main():
    blocks_dossed = 0
    fee = INITIAL_BASE_FEE
    total_paid = 0
    while (blocks_dossed <= BLOCKS_TO_DOS):
      gas_used_delta = GAS_USED - GAS_TARGET
      base_fee_per_gas_delta = max(fee * gas_used_delta // GAS_TARGET // BASE_FEE_MAX_CHANGE_DENOMINATOR, 1)
      expected_base_fee_per_gas = fee + base_fee_per_gas_delta
      fee = expected_base_fee_per_gas
      total_paid += fee * GAS_USED
      blocks_dossed += 1
    
    print("blocks_dossed", blocks_dossed)
    print("fee", fee)
    print("total_paid", total_paid)



main()
```
