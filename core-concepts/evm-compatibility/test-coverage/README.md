# Test Coverage

The tables below provide a summary and detailed information in relation to the number of tests performed, the count of passing tests and the count of failing tests.

To summarise, VeChain is fully compatible with OpenZeppelin contracts (with v5 being the latest version tested), and the main differences encountered are related to Hardhat:
- The `chainId` in VeChain is the genesis block ID of each network
- Custom [Hardhat RPC methods](https://hardhat.org/hardhat-network/docs/reference#special-testing/debugging-methods) like `evm_increaseTime` or `evm_mine` depend on the actual Hardhat VeChain plugin (so differences might be expected in this regard).

You can find detailed analysis of the coverage categories in the pages to follow.

## OpenZeppelin v5

### Summary

<table><thead><tr><th width="271">Category</th><th width="394">Short Description</th><th>Failures</th></tr></thead><tbody><tr><td>Set base URI</td><td>URI was not set in the ERC721 and ERC721Enumerable test cases, causing 6 tests to remain pending. Since these tests focus on compatibility, URI validation is not essential. </td><td>0</td></tr></tbody></table>

### Detail

<table><thead>
<tr><th width="306">Contract Name</th><th>Pass</th><th>Fail</th><th>Total</th><th data-hidden>Test Coverage</th></tr></thead>
<tbody>
<tr><td><strong>Total</strong></td><td><strong>2611</strong></td><td><strong>0</strong></td><td><strong>2617</strong></td><td></td></tr>
<tr><td>AccessControl</td><td>30</td><td>0</td><td>30</td><td></td></tr>
<tr><td>Ownable</td><td>8</td><td>0</td><td>8</td><td></td></tr>
<tr><td>Ownable2Step</td><td>6</td><td>0</td><td>6</td><td></td></tr>
<tr><td>AccessControlDefaultAdminRules</td><td>56</td><td>0</td><td>56</td><td></td></tr>
<tr><td>AccessControlEnumerable</td><td>36</td><td>0</td><td>36</td><td></td></tr>
<tr><td>AccessManaged</td><td>8</td><td>0</td><td>8</td><td></td></tr>
<tr><td>AccessManager</td><td>113</td><td>0</td><td>113</td><td></td></tr>
<tr><td>AuthorityUtils</td><td>4</td><td>0</td><td>4</td><td></td></tr>
<tr><td>VestingWallet</td><td>2</td><td>0</td><td>2</td><td></td></tr>
<tr><td>Governor</td><td>136</td><td>0</td><td>136</td><td></td></tr>
<tr><td>GovernorERC721</td><td>2</td><td>0</td><td>2</td><td></td></tr>
<tr><td>GovernorPreventLateQuorum</td><td>5</td><td>0</td><td>5</td><td></td></tr>
<tr><td>GovernorStorage</td><td>3</td><td>0</td><td>3</td><td></td></tr>
<tr><td>GovernorTimelockAccess</td><td>3</td><td>0</td><td>3</td><td></td></tr>
<tr><td>GovernorTimelockCompound</td><td>8</td><td>0</td><td>8</td><td></td></tr>
<tr><td>GovernorTimelockControl</td><td>12</td><td>0</td><td>12</td><td></td></tr>
<tr><td>GovernorVotesQuorumFraction</td><td>4</td><td>0</td><td>4</td><td></td></tr>
<tr><td>GovernorWithParams</td><td>7</td><td>0</td><td>7</td><td></td></tr>
<tr><td>Votes</td><td>44</td><td>0</td><td>44</td><td></td></tr>
<tr><td>ERC2771Context</td><td>11</td><td>0</td><td>11</td><td></td></tr>
<tr><td>ERC2771Forwarder</td><td>36</td><td>0</td><td>36</td><td></td></tr>
<tr><td>Clones</td><td>30</td><td>0</td><td>30</td><td></td></tr>
<tr><td>ERC1967Proxy</td><td>19</td><td>0</td><td>19</td><td></td></tr>
<tr><td>BeaconProxy</td><td>6</td><td>0</td><td>6</td><td></td></tr>
<tr><td>UpgradeableBeacon</td><td>6</td><td>0</td><td>6</td><td></td></tr>
<tr><td>ProxyAdmin</td><td>5</td><td>0</td><td>5</td><td></td></tr>
<tr><td>TransparentUpgradeableProxy</td><td>19</td><td>0</td><td>19</td><td></td></tr>
<tr><td>Initializable</td><td>29</td><td>0</td><td>29</td><td></td></tr>
<tr><td>UUPSupgradeable</td><td>8</td><td>0</td><td>8</td><td></td></tr>
<tr><td>ERC721</td><td>375</td><td>0</td><td>378</td><td></td></tr>
<tr><td>ERC721Enumerable</td><td>397</td><td>0</td><td>400</td><td></td></tr>
<tr><td>ERC721Wrapper</td><td>18</td><td>0</td><td>18</td><td></td></tr>
<tr><td>ERC721Holder</td><td>1</td><td>0</td><td>1</td><td></td></tr>
<tr><td>ERC721Burnable</td><td>5</td><td>0</td><td>5</td><td></td></tr>
<tr><td>ERC721Consecutive</td><td>34</td><td>0</td><td>34</td><td></td></tr>
<tr><td>ERC721Pausable</td><td>9</td><td>0</td><td>9</td><td></td></tr>
<tr><td>ERC721Royalty</td><td>16</td><td>0</td><td>16</td><td></td></tr>
<tr><td>ERC721URIStorage</td><td>17</td><td>0</td><td>17</td><td></td></tr>
<tr><td>ERC721Votes</td><td>23</td><td>0</td><td>23</td><td></td></tr>
<tr><td>ERC721Holder</td><td>1</td><td>0</td><td>1</td><td></td></tr>
<tr><td>ERC1155</td><td>89</td><td>0</td><td>89</td><td></td></tr>
<tr><td>ERC1155Burnable</td><td>6</td><td>0</td><td>6</td><td></td></tr>
<tr><td>ERC1155Pausable</td><td>11</td><td>0</td><td>11</td><td></td></tr>
<tr><td>ERC1155Supply</td><td>4</td><td>0</td><td>4</td><td></td></tr>
<tr><td>ERC1155URIStorage</td><td>4</td><td>0</td><td>4</td><td></td></tr>
<tr><td>ERC1155Holder</td><td>7</td><td>0</td><td>7</td><td></td></tr>
<tr><td>Address</td><td>7</td><td>0</td><td>7</td><td></td></tr>
<tr><td>Address</td><td>29</td><td>0</td><td>29</td><td></td></tr>
<tr><td>Arrays</td><td>20</td><td>0</td><td>20</td><td></td></tr>
<tr><td>Base64</td><td>5</td><td>0</td><td>5</td><td></td></tr>
<tr><td>Context</td><td>4</td><td>0</td><td>4</td><td></td></tr>
<tr><td>Create2</td><td>8</td><td>0</td><td>8</td><td></td></tr>
<tr><td>Multicall</td><td>4</td><td>0</td><td>4</td><td></td></tr>
<tr><td>Nonces</td><td>6</td><td>0</td><td>6</td><td></td></tr>
<tr><td>Pausable</td><td>11</td><td>0</td><td>11</td><td></td></tr>
<tr><td>ReentrancyGuard</td><td>6</td><td>0</td><td>6</td><td></td></tr>
<tr><td>ShortStrings</td><td>14</td><td>0</td><td>14</td><td></td></tr>
<tr><td>StorageSlot</td><td>24</td><td>0</td><td>24</td><td></td></tr>
<tr><td>Strings</td><td>71</td><td>0</td><td>71</td><td></td></tr>
<tr><td>ECDSA</td><td>14</td><td>0</td><td>14</td><td></td></tr>
<tr><td>EIP712</td><td>13</td><td>0</td><td>13</td><td></td></tr>
<tr><td>MerkleProof</td><td>10</td><td>0</td><td>10</td><td></td></tr>
<tr><td>MessageHashUtils</td><td>4</td><td>0</td><td>4</td><td></td></tr>
<tr><td>ERC165</td><td>5</td><td>0</td><td>5</td><td></td></tr>
<tr><td>ERC165Checker</td><td>40</td><td>0</td><td>40</td><td></td></tr>
<tr><td>Math</td><td>44</td><td>0</td><td>44</td><td></td></tr>
<tr><td>SafeCast</td><td>444</td><td>0</td><td>444</td><td></td></tr>
<tr><td>SignedMath</td><td>12</td><td>0</td><td>12</td><td></td></tr>
<tr><td>BitMap</td><td>10</td><td>0</td><td>10</td><td></td></tr>
<tr><td>Checkpoints</td><td>33</td><td>0</td><td>33</td><td></td></tr>
<tr><td>DoubleEndedQueue</td><td>9</td><td>0</td><td>9</td><td></td></tr>
<tr><td>EnumerableMap</td><td>60</td><td>0</td><td>60</td><td></td></tr>
<tr><td>EnumerableSet</td><td>24</td><td>0</td><td>24</td><td></td></tr>
<tr><td>Time</td><td>7</td><td>0</td><td>7</td><td></td></tr>
</tbody></table>

## OpenZeppelin v4

### Summary

<table><thead><tr><th width="305">Category</th><th width="359">Short Description</th><th>Failures</th></tr></thead><tbody><tr><td>Justifiable</td><td>Failures that result from the inherent design differences between VeChain and Ethereum.</td><td>73</td></tr><tr><td>Contract Address Prediction</td><td>See <a href="https://github.com/vechain/vechain-docs/blob/main/core-concepts/evm-compatibility/test-coverage/broken-reference/README.md">here</a>.</td><td>14</td></tr><tr><td>Failures in Constructor</td><td>Contract fails in constructor, resulting in failure to be deployed.</td><td>7</td></tr><tr><td>Full, with eth_sign implementation</td><td>See <a href="https://github.com/vechain/vechain-docs/blob/main/core-concepts/evm-compatibility/test-coverage/broken-reference/README.md">here</a>.</td><td>4</td></tr><tr><td>Full, with test changes</td><td>Some test modifications had to be added for the tests to pass.</td><td>3</td></tr><tr><td>BadBeaconProxy Address 0x1</td><td>See <a href="https://github.com/vechain/vechain-docs/blob/main/core-concepts/evm-compatibility/test-coverage/broken-reference/README.md">here</a>.</td><td>1</td></tr></tbody></table>

### Detail

<table><thead><tr><th width="305">Contract Name</th><th>Pass</th><th>Fail</th><th>Total</th><th data-hidden>Test Coverage</th><th data-hidden>Hardhat Total Tests</th></tr></thead><tbody><tr><td><strong>Total</strong></td><td><strong>2324</strong></td><td><strong>102</strong></td><td><strong>2426</strong></td><td></td><td><strong>2667</strong></td></tr><tr><td>ERC1967Proxy</td><td>25</td><td>3</td><td>28</td><td></td><td>28</td></tr><tr><td>TransparentUpgradeableProxy</td><td>58</td><td>3</td><td>61</td><td></td><td>61</td></tr><tr><td>BeaconProxy</td><td>7</td><td>2</td><td>9</td><td></td><td>9</td></tr><tr><td>GovernorTimelockCompound</td><td>7</td><td>12</td><td>19</td><td></td><td>19</td></tr><tr><td>GovernorCompatibilityBravo</td><td>7</td><td>2</td><td>9</td><td></td><td>9</td></tr><tr><td>TimelockController</td><td>27</td><td>15</td><td>42</td><td></td><td>48</td></tr><tr><td>CrossChainEnabled</td><td>4</td><td>9</td><td>13</td><td></td><td>15</td></tr><tr><td>GovernorTimelockControl</td><td>12</td><td>9</td><td>21</td><td></td><td>21</td></tr><tr><td>AccessControl</td><td>50</td><td>4</td><td>54</td><td></td><td>80</td></tr><tr><td>MinimalForwarder</td><td>12</td><td>4</td><td>16</td><td></td><td>15</td></tr><tr><td>TokenTimelock</td><td>3</td><td>4</td><td>7</td><td></td><td>7</td></tr><tr><td>VestingWallet</td><td>2</td><td>4</td><td>6</td><td></td><td>6</td></tr><tr><td>ERC721Enumerable</td><td>233</td><td>3</td><td>236</td><td></td><td>236</td></tr><tr><td>DoubleEndedQueue</td><td>7</td><td>2</td><td>9</td><td></td><td>9</td></tr><tr><td>ERC2771Context</td><td>5</td><td>2</td><td>7</td><td></td><td>7</td></tr><tr><td>ERC721</td><td>211</td><td>2</td><td>213</td><td></td><td>213</td></tr><tr><td>Governor</td><td>42</td><td>2</td><td>44</td><td></td><td>44</td></tr><tr><td>Checkpoints</td><td>22</td><td>1</td><td>23</td><td></td><td>23</td></tr><tr><td>ERC1155</td><td>83</td><td>1</td><td>84</td><td></td><td>84</td></tr><tr><td>ERC1155Holder</td><td>4</td><td>1</td><td>5</td><td></td><td>5</td></tr><tr><td>ERC1155PresetMinterPauser</td><td>16</td><td>1</td><td>17</td><td></td><td>17</td></tr><tr><td>ERC165</td><td>2</td><td>1</td><td>3</td><td></td><td>3</td></tr><tr><td>ERC165Storage</td><td>4</td><td>1</td><td>5</td><td></td><td>5</td></tr><tr><td>ERC20Votes</td><td>28</td><td>1</td><td>29</td><td></td><td>29</td></tr><tr><td>ERC20VotesComp</td><td>27</td><td>1</td><td>28</td><td></td><td>28</td></tr><tr><td>ERC721PresetMinterPauserAutoId</td><td>15</td><td>1</td><td>16</td><td></td><td>16</td></tr><tr><td>ERC721Royalty</td><td>13</td><td>1</td><td>14</td><td></td><td>14</td></tr><tr><td>GovernorWithParams</td><td>3</td><td>1</td><td>4</td><td></td><td>4</td></tr><tr><td>MerkleProof</td><td>8</td><td>1</td><td>9</td><td></td><td>9</td></tr><tr><td>TimersTimestamp</td><td>4</td><td>1</td><td>5</td><td></td><td>5</td></tr><tr><td>ECDSA</td><td>14</td><td>3</td><td>17</td><td></td><td>17</td></tr><tr><td>SignatureChecker (ERC1271)</td><td>1</td><td>1</td><td>1</td><td></td><td>7</td></tr><tr><td>ERC1820Implementer</td><td>1</td><td>1</td><td>1</td><td></td><td>6</td></tr><tr><td>ERC777</td><td>1</td><td>1</td><td>1</td><td></td><td>193</td></tr><tr><td>ERC777PresetFixedSupply</td><td>1</td><td>1</td><td>1</td><td></td><td>6</td></tr><tr><td>Address</td><td>29</td><td>0</td><td>29</td><td></td><td>29</td></tr><tr><td>Arrays</td><td>15</td><td>0</td><td>15</td><td></td><td>15</td></tr><tr><td>BitMap</td><td>10</td><td>0</td><td>10</td><td></td><td>10</td></tr><tr><td>Clones</td><td>30</td><td>0</td><td>30</td><td></td><td>30</td></tr><tr><td>ConditionalEscrow</td><td>11</td><td>0</td><td>11</td><td></td><td>11</td></tr><tr><td>Context</td><td>4</td><td>0</td><td>4</td><td></td><td>4</td></tr><tr><td>Counters</td><td>8</td><td>0</td><td>8</td><td></td><td>8</td></tr><tr><td>Create2</td><td>8</td><td>0</td><td>8</td><td></td><td>8</td></tr><tr><td>EIP712</td><td>2</td><td>0</td><td>2</td><td></td><td>2</td></tr><tr><td>EnumerableMap</td><td>70</td><td>0</td><td>70</td><td></td><td>70</td></tr><tr><td>EnumerableSet</td><td>20</td><td>0</td><td>24</td><td></td><td>24</td></tr><tr><td>ERC1155Burnable</td><td>6</td><td>0</td><td>6</td><td></td><td>6</td></tr><tr><td>ERC1155Pausable</td><td>11</td><td>0</td><td>11</td><td></td><td>11</td></tr><tr><td>ERC1155Supply</td><td>10</td><td>0</td><td>10</td><td></td><td>10</td></tr><tr><td>ERC1155URIStorage</td><td>4</td><td>0</td><td>4</td><td></td><td>4</td></tr><tr><td>ERC165Checker</td><td>40</td><td>0</td><td>40</td><td></td><td>40</td></tr><tr><td>ERC20</td><td>118</td><td>0</td><td>118</td><td></td><td>118</td></tr><tr><td>ERC20Burnable</td><td>13</td><td>0</td><td>13</td><td></td><td>13</td></tr><tr><td>ERC20Capped</td><td>5</td><td>0</td><td>5</td><td></td><td>5</td></tr><tr><td>ERC20FlashMint</td><td>12</td><td>0</td><td>12</td><td></td><td>12</td></tr><tr><td>ERC20Pausable</td><td>12</td><td>0</td><td>12</td><td></td><td>12</td></tr><tr><td>ERC20Permit</td><td>6</td><td>0</td><td>6</td><td></td><td>6</td></tr><tr><td>ERC20PresetFixedSupply</td><td>4</td><td>0</td><td>4</td><td></td><td>4</td></tr><tr><td>ERC20PresetMinterPauser</td><td>12</td><td>0</td><td>12</td><td></td><td>12</td></tr><tr><td>ERC20Snapshot</td><td>14</td><td>0</td><td>14</td><td></td><td>14</td></tr><tr><td>ERC4626</td><td>25</td><td>0</td><td>25</td><td></td><td>25</td></tr><tr><td>ERC721Burnable</td><td>4</td><td>0</td><td>4</td><td></td><td>4</td></tr><tr><td>ERC721Consecutive</td><td>13</td><td>0</td><td>13</td><td></td><td>13</td></tr><tr><td>ERC721Holder</td><td>1</td><td>0</td><td>1</td><td></td><td>1</td></tr><tr><td>ERC721Pausable</td><td>10</td><td>0</td><td>10</td><td></td><td>10</td></tr><tr><td>ERC721URIStorage</td><td>10</td><td>0</td><td>10</td><td></td><td>10</td></tr><tr><td>ERC721Votes</td><td>26</td><td>0</td><td>26</td><td></td><td>26</td></tr><tr><td>Escrow</td><td>10</td><td>0</td><td>10</td><td></td><td>10</td></tr><tr><td>GovernorComp</td><td>2</td><td>0</td><td>2</td><td></td><td>2</td></tr><tr><td>GovernorERC721Mock</td><td>2</td><td>0</td><td>2</td><td></td><td>2</td></tr><tr><td>GovernorPreventLateQuorum</td><td>5</td><td>0</td><td>5</td><td></td><td>5</td></tr><tr><td>GovernorVotesQuorumFraction</td><td>6</td><td>0</td><td>6</td><td></td><td>6</td></tr><tr><td>Initializable</td><td>29</td><td>0</td><td>29</td><td></td><td>29</td></tr><tr><td>Math</td><td>25</td><td>0</td><td>25</td><td></td><td>25</td></tr><tr><td>MulticallToken</td><td>4</td><td>0</td><td>4</td><td></td><td>4</td></tr><tr><td>Ownable</td><td>6</td><td>0</td><td>6</td><td></td><td>6</td></tr><tr><td>Ownable2Step</td><td>5</td><td>0</td><td>5</td><td></td><td>5</td></tr><tr><td>Pausable</td><td>11</td><td>0</td><td>11</td><td></td><td>11</td></tr><tr><td>PaymentSplitter</td><td>20</td><td>0</td><td>20</td><td></td><td>20</td></tr><tr><td>ProxyAdmin</td><td>12</td><td>0</td><td>12</td><td></td><td>12</td></tr><tr><td>PullPayment</td><td>4</td><td>0</td><td>4</td><td></td><td>4</td></tr><tr><td>ReentrancyGuard</td><td>6</td><td>0</td><td>6</td><td></td><td>6</td></tr><tr><td>RefundEscrow</td><td>17</td><td>0</td><td>17</td><td></td><td>17</td></tr><tr><td>SafeCast</td><td>444</td><td>0</td><td>444</td><td></td><td>444</td></tr><tr><td>SafeERC20</td><td>35</td><td>0</td><td>35</td><td></td><td>35</td></tr><tr><td>SafeMath</td><td>48</td><td>0</td><td>48</td><td></td><td>48</td></tr><tr><td>SignedMath</td><td>12</td><td>0</td><td>12</td><td></td><td>12</td></tr><tr><td>SignedSafeMath</td><td>17</td><td>0</td><td>17</td><td></td><td>17</td></tr><tr><td>StorageSlot</td><td>12</td><td>0</td><td>12</td><td></td><td>12</td></tr><tr><td>Strings</td><td>31</td><td>0</td><td>31</td><td></td><td>31</td></tr><tr><td>TimersBlockNumber</td><td>5</td><td>0</td><td>5</td><td></td><td>5</td></tr><tr><td>UpgradeableBeacon</td><td>5</td><td>0</td><td>5</td><td></td><td>5</td></tr><tr><td>UUPSUpgradeable</td><td>6</td><td>0</td><td>6</td><td></td><td>6</td></tr><tr><td>Votes</td><td>23</td><td>0</td><td>23</td><td></td><td>23</td></tr></tbody></table>