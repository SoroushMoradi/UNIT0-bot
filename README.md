# UNIT0-bot


#
>Faucet link: [UNIT0-Faucet](https://faucet-testnet.unit0.dev/)  
>Dashboard : [UNIT0](https://app.units.network/?referral=0x07c9A81d0C430d29076f055f142539507eb19700) 
#

**Install Requirements**
```
sudo apt update
sudo apt install nodejs npm
```
**verify Installation:**
```
node --version
npm --version
```

**create a new directory for your project and navigate to it:**  
```
mkdir unit0-automation
cd unit0-automation
```
**Initialize a new Node.js project:**  
```npm init -y```

**Install the required dependencies(Ethers):**  
```npm install ethers```

**Create a new file named automate_transactions.js:**  
```touch automate_transactions.js```

**Open automate_transactions.js file:**  
```nano automate_transactions.js```

Copy and paste the following code into the file:   
>  replace your private key with "your-private-key-here" 
> replace the address that you want send transaction with "recipient_address_here"
```
const ethers = require('ethers');

// Configuration for connecting to Unit0 testnet
const provider = new ethers.JsonRpcProvider('https://rpc-testnet.unit0.dev');

// Your account's private key - replace this with your actual private key
const privateKey = 'your_private_key_here';
const wallet = new ethers.Wallet(privateKey, provider);

// Function to send a transaction
async function sendTransaction(to, value) {
    const tx = {
        to: to,
        value: ethers.parseEther(value.toString())
    };

    const signedTx = await wallet.sendTransaction(tx);
    console.log(`Transaction sent: ${signedTx.hash}`);
    return signedTx.wait();
}

// Delay function
function delay(ms) {
    return new Promise(resolve => setTimeout(resolve, ms));
}

// Function to get a random delay between 10 to 15 seconds
function getRandomDelay() {
    return Math.floor(Math.random() * (3000 - 5000 + 1) + 10000);
}

// Function to automate transactions
async function automateTransactions(count, to, value) {
    for (let i = 0; i < count; i++) {
        console.log(`Sending transaction ${i + 1} of ${count}`);
        try {
            const receipt = await sendTransaction(to, value);
            console.log(`Transaction confirmed in block ${receipt.blockNumber}`);
            
            if (i < count - 1) {  // Don't delay after the last transaction
                const delayMs = getRandomDelay();
                console.log(`Waiting for ${delayMs / 1000} seconds before next transaction...`);
                await delay(delayMs);
            }
        } catch (error) {
            console.error(`Error in transaction ${i + 1}:`, error);
        }
    }
}

// Execute the automation function
automateTransactions(500, "recipient_address_here", 0.00001)
    .then(() => console.log("All transactions completed"))
    .catch(error => console.error("Error in automation:", error));
```
> CRL + X then Y then Enter

**Modify the package.json file to add a start script:**  
```npm pkg set scripts.start="node automate_transactions.js"```  
**and finally start :**  
```npm start```

> This script ajust to execute 500 trx if you want to change the number of transactions
> you can do this :
**open the file:**
```nano automate_transactions.js```

Edit the number of transactions(500) to any number you want:  
__Done__.  

**follow**:  
My [X](https://x.com/sormorEth)   
My [Medium](https://medium.com/@sormor)
