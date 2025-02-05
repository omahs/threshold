---
description: Use a config file to store client configuration.
---

# Config File

Application configuration can be stored in a file and passed to the application with the `--config` flag.

Example:

```
./keep-client --config /path/to/your/config.toml start
```

Configuration files in formats TOML, YAML and JSON are supported.

Sample configuration file:

{% code overflow="wrap" %}
```toml
# This is a sample TOML configuration file for the Keep client.

[ethereum]
URL = "ws://127.0.0.1:8546"
KeyFile = "/Users/someuser/ethereum/data/keystore/UTC--2018-03-11T01-37-33.202765887Z--AAAAAAAAAAAAAAAAAAAAAAAAAAAAAA8AAAAAAAAA"

# Uncomment to override the defaults for transaction status monitoring.

# MiningCheckInterval is the interval in which transaction
# mining status is checked. If the transaction is not mined within this
# time, the gas price is increased and transaction is resubmitted.
#
# MiningCheckInterval = 60  # 60 sec (default value)

# MaxGasFeeCap specifies the maximum gas fee cap the client is
# willing to pay for the transaction to be mined. The offered transaction
# gas cost can not be higher than the max gas fee cap value. If the maximum
# allowed gas fee cap is reached, no further resubmission attempts are
# performed. This property should be set only for Ethereum. In case of
# legacy non-EIP-1559 transactions, this field works in the same way as
# `MaxGasPrice` property.
#
# MaxGasFeeCap = "500 Gwei" # 500 Gwei (default value)

# Uncomment to enable Ethereum node rate limiting. Both properties can be
# used together or separately.
#
# RequestsPerSecondLimit sets the maximum average number of requests
# per second which can be executed against the Ethereum node.
# All types of Ethereum node requests are rate-limited,
# including view function calls.
#
# RequestsPerSecondLimit = 150

# ConcurrencyLimit sets the maximum number of concurrent requests which
# can be executed against the Ethereum node at the same time.
# This limit affects all types of Ethereum node requests,
# including view function calls.
#
# ConcurrencyLimit = 30

# BalanceAlertThreshold defines a minimum value of the operator's account
# balance below which the client will start reporting errors in logs.
# A value can be provided in `wei`, `Gwei` or `ether`, e.g. `7.5 ether`,
# `7500000000 Gwei`.
#
# BalanceAlertThreshold = "0.5 ether" # 0.5 ether (default value)

[network]
Bootstrap = false
Peers = [
	"/ip4/127.0.0.1/tcp/3919/ipfs/16Uiu2HAmFRJtCWfdXhZEZHWb4tUpH1QMMgzH1oiamCfUuK6NgqWX",
]
Port = 3920

# Uncomment to override the node's default addresses announced in the network
# AnnouncedAddresses = ["/dns4/example.com/tcp/3919", "/ip4/80.70.60.50/tcp/3919"]

# Uncomment to enable courtesy message dissemination for topics this node is
# not subscribed to. Messages will be forwarded to peers for the duration
# specified as a value in seconds.
# Message dissemination is disabled by default and should be enabled only
# on selected bootstrap nodes. It is not a good idea to enable dissemination
# on non-bootstrap node as it may clutter communication and eventually lead
# to blacklisting the node. The maximum allowed value is 90 seconds.
#
# DisseminationTime = 90

[storage]
Dir = "/my/secure/location"

# ClientInfo exposes metrics and diagnostics modules.
# 
# Metrics collects and exposes information useful for external monitoring tools usually
# operating on time series data.
# All values exposed by metrics module are quantifiable or countable.
#
# The following metrics are available:
# - connected peers count
# - connected bootstraps count
# - eth client connectivity status
# 
# Diagnostics module exposes the following information:
# - list of connected peers along with their network id and ethereum operator address
# - information about the client's network id and ethereum operator address
[clientInfo]
Port = 9601
# NetworkMetricsTick = 60
# EthereumMetricsTick = 600

# Uncomment to overwrite default values for TBTC config.
#
# [tbtc]
# PreParamsPoolSize = 3000
# PreParamsGenerationTimeout = "2m"
# PreParamsGenerationDelay = "10s"
# PreParamsGenerationConcurrency = 1
# KeyGenConcurrency = 1

# Developer options to work with locally deployed contracts
#
# [developer]
# TokenStakingAddress = "0xBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBB"
# RandomBeaconAddress = "0xBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBB"
# WalletRegistryAddress = "0xBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBB"
# BridgeAddress = "0xBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBB"
```
{% endcode %}

