---
layout:
  title:
    visible: true
  description:
    visible: true
  tableOfContents:
    visible: true
  outline:
    visible: false
  pagination:
    visible: false
---

# Validator Key Management

Running a VeChainThor validator node requires careful management of cryptographic keys. This guide covers the essential aspects of key management, including generation, backup, recovery, and the relationship between validator keys and staking operations.

## Overview

The Thor node uses a **master key system** for validator operations. This master key is an ECDSA private key that serves as your validator's unique identity for block signing and consensus participation. The master key's corresponding public address is what gets registered in the staking contract and identifies your validator on the network.

## Key Components and File Locations

### Key Files
- **Master Key**: `~/.org.vechain.thor/master.key` (or `$CONFIG_DIR/master.key`)


## Master Key Management Commands

### 1. Display Master Key Address

```bash
bin/thor master-key
```

This command shows the public address corresponding to your master key. If no key exists, it automatically generates one.

### 2. Export Master Key (Backup)

```bash
bin/thor master-key --export > keystore.json
```

This exports your master key as an encrypted JSON keystore file. You'll be prompted for a passphrase to encrypt the export. **Always backup your keys before going live.**

### 3. Import Master Key (Restore)

```bash
cat keystore.json | bin/thor master-key --import
```

This imports a master key from an encrypted JSON keystore file. You'll need the passphrase used during export.

### 4. Use Key from Standard Input

```bash
bin/thor --master-key-stdin --network main
```

This allows you to provide the master key directly via stdin rather than using the stored file, useful for automated deployments or enhanced security setups.

## Key Generation Process

When you first run a Thor node, the key generation happens automatically:

1. **Load Attempt**: First tries to load existing key from `~/.org.vechain.thor/master.key`
2. **Generate New**: If no key exists, generates a new ECDSA private key using `crypto.GenerateKey()`
3. **Save**: Automatically saves the new key to the file system using `crypto.SaveECDSA()`

## Creating New Keys After Node Exit

If you need to create new keys (e.g., after losing access, security concerns, or wanting fresh credentials for a new staking period):

```bash
# Backup existing master key
mv ~/.org.vechain.thor/master.key ~/.org.vechain.thor/master.key.old

# Generate a new key automatically
# Will output public key 
bin/thor master-key
```

## Staking and Key Relationship

For validator staking, you need to understand two distinct key components:

### Two Key Components
1. **Endorser Address**: The account that deposits VET (can be any address with sufficient VET)
2. **Validator Address**: The master key public address from your Thor node

### Staking Parameters
- **Caller**: Endorser public address (the account depositing the VET)
- **Validator**: Master key public address (from `bin/thor master-key`)
- **Period**: Lock period in blocks (60480/129600/259200 for 7/15/30 days)
- **Value**: Amount of VET to stake (minimum 25M VET for validators)

### Staking Workflow
1. Generate/obtain master key: `bin/thor master-key`
2. Ensure node is fully synced: `bin/thor --network main --skip-logs`
3. Use the master key address as the "Validator" parameter in staking contract
4. Use your VET-holding account as the "Caller/Endorser" address
5. Execute staking transaction with proper parameters

## Security Best Practices

### File Permissions and Backup
```bash
# Ensure key file has restricted permissions
chmod 600 ~/.org.vechain.thor/master.key

# Export keys immediately after generation
bin/thor master-key --export > backup-keystore.json
```

### Key Security Guidelines
- **Store backups securely** offline in multiple locations
- **Test recovery process** with backups before going live
- **Use strong passphrases** for encrypted exports
- **Separate concerns**: Use different addresses for staking (endorser) and validation (master key)
- **Regular backups**: Export keys after any changes or before major updates
- **Monitor key usage**: Track validator address activity on block explorers

## Recovery Scenarios

### Lost Master Key
If you lose your master key:
1. You'll need to generate a new key (loses previous validator identity)
2. Re-stake with the new master key address
3. Previous stake remains locked to old address until maturity
4. Update any monitoring or management systems with new validator address

### Node Migration
When moving to a new server:
1. **Export** master key from old node: `bin/thor master-key --export > migration-keystore.json`
2. **Import** on new node: `cat migration-keystore.json | bin/thor master-key --import`
3. **Verify** address matches: `bin/thor master-key`
4. **Test** node operation before decommissioning old node

### Configuration Directory Issues
- **Default location**: `~/.org.vechain.thor/` on Linux/macOS
- **Override with**: `--config-dir` flag
- **Ensure proper permissions** on directory and files
- **Verify path accessibility** before starting production operations

## Advanced Key Management

### Key Rotation for New Staking Periods
1. **Generate new master key** before current stake period ends
2. **Test new key** with node operation
3. **Backup both keys** until transition is complete
4. **Re-stake with new key** when ready
5. **Decommission old key** after stake maturity

### Multiple Validator Setup
Each validator node requires:
- Unique master key
- Separate configuration directory
- Distinct network ports
- Individual staking transactions

## Troubleshooting

### Common Issues and Solutions
```bash
# Key file not found or permission denied
ls -la ~/.org.vechain.thor/master.key
chmod 600 ~/.org.vechain.thor/master.key
chown $USER:$USER ~/.org.vechain.thor/master.key
```

**Import/Export Issues**: Verify JSON format, check passphrase accuracy, ensure sufficient disk space

## Summary

Proper key management is crucial for validator operations on VeChainThor. Your master key address becomes your validator identity on the network, so always backup keys before going live and plan key management operations carefully during staking transitions or node migrations.

---

### Technical Reference
For developers, the key management functionality is implemented in:
- Key loading/generation: `cmd/thor/utils.go:loadOrGeneratePrivateKey()` (line 116)
- Master key path resolution: `cmd/thor/utils.go:masterKeyPath()` (line 429)
- Master key actions: `cmd/thor/main.go:masterKeyAction()` (line 518)