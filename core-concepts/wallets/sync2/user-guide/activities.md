# Activities

<figure><img src="../../../../.gitbook/assets/activities.36116c16 (1).png" alt=""><figcaption></figcaption></figure>

## Activities status <a href="#activities-status" id="activities-status"></a>

### Ongoing <a href="#ongoing" id="ongoing"></a>

* **Sending** : Signed content is awaiting to be processed and not being packed into a block.
* **Confirming** : Transaction is packed into a block and can be "View" on the blockchain but required 12 blocks to confirm.

{% hint style="info" %}
* Unstable connection to the transaction pool may cause the transactions to fail. Sync2 will automatically retry the transaction request until it expires. Once expired, Sync2 will update the status to "expired".
* Transaction required 12 blocks to be confirmed.
{% endhint %}

### Completed <a href="#completed" id="completed"></a>

* **Confirmed**: Transaction has been confirmed more than 12 blocks or signed a certificate.
* **Expired**: The transaction reached the limit of expiration or the VTHO is not enough to compute the transaction.
* **Reverted**: Several reasons may cause the transaction to revert.

{% hint style="info" %}
* Reverted transaction will deduct the VTHO due to vm(virtual machine) computed
* All the signed transactions/certificates are **stored in local**, therefore, it only shows the transaction/content which you signed on the device.
{% endhint %}

## View On explorer (Transaction Only) <a href="#view-on-explorer" id="view-on-explorer"></a>

1. Click the transaction to expand the details
2. Click <img src="../../../../.gitbook/assets/Screenshot 2023-08-17 at 16.55.38.png" alt="" data-size="line"> to check on [explorer](https://explore.vechain.org/)

## Copy TxID (Transaction Only) <a href="#copy-txid" id="copy-txid"></a>

1. Click the transaction to expand the details
2. Click <img src="../../../../.gitbook/assets/Screenshot 2023-08-17 at 16.55.33.png" alt="" data-size="line"> to copy the transaction ID

## Link to dApp <a href="#link-to-dapp" id="link-to-dapp"></a>

1. Click the transaction to expand the details
2. Click <img src="../../../../.gitbook/assets/Screenshot 2023-08-17 at 16.56.29.png" alt="" data-size="line"> to direct to the link which dApps provided

## View signed content (Certificate Only) <a href="#view-signed-content" id="view-signed-content"></a>

1. Click the certificate to check the details
2. Click ![](https://docs.vechain.org/assets/img/message.759cf5c9.svg) to check original signed content
