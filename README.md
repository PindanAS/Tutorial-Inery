# Tutorial-Inery
## Prerequisite

### Instal curl
```
sudo apt-get install curl
```
### NodeJS & NPM
```
curl -fsSL https://deb.nodesource.com/setup_19.x | sudo -E bash - &&\
sudo apt-get install -y nodejs
```
### Clone repository
```
git clone https://github.com/inery-blockchain/inery-testnet-faucet-tasks
```


## How to run?

**1. Change directory to `aprameth`**

```
cd inery-testnet-faucet-tasks/aprameth
```

**2. Install dependencies**

```
npm install
```

**3. Go to ineryjs directory**
```
cd node_modules/ineryjs
```

**4. Create .env & .env-sample**
```
touch .env
```
```
touch .env-sample
```

Edit .env & .env-sample
```
nano .env
```

Fill with this
```
INERY_ACCOUNT="your_inery_account"
PRIVATE_KEY="your_private_key"
NODE_URL="http://your_node_url:8888"
```

**5. Copy**
```
cp .env-sample .env
```


**6. Back to apramet directory and run this script**
```
cd ../..
```

**7. Edit solution.mjs**
```
nano solution.mjs
```

Delete All and change with this
```
import { Api, JsonRpc, JsSignatureProvider } from 'ineryjs/dist/index.js';

const url = 'Your_VPS_URL:8888';

const json_rpc = new JsonRpc(url);
const private_key = 'YOUR_PRIVATE_KEY';
export const actor = 'YOUR_NAME';

export const account = 'YOUR_NAME';
const signature = new JsSignatureProvider([private_key]);

export const api = new Api({
	rpc: json_rpc,
	signatureProvider: signature
})

async function create(id, user, data){
    try{
        const tx = await api.transact({
            actions:[
                {
                    account,
                    name:"create",
                    authorization:[
                        {
                            actor,
                            permission:"active"
                        }
                    ],
                    data:{
                        id, user, data
                    }
                }
            ]
        },{broadcast:true,sign:true})

	console.log("=======================================================================")
        console.log("===================== CREATE transaction details ======================")
        console.log("=======================================================================")
        console.log(tx, "\n")
        console.log("Response from contract :", tx.processed.action_traces[0].console)
        console.log("\n")
    }catch(error){
        console.log(error)
    }
}

async function read(id){
    try{
        const tx = await api.transact({
            actions:[
                {
                    account,
                    name:"read",
                    authorization:[
                        {
                            actor,
                            permission:"active"
                        }
                    ],
                    data:{
                        id
                    }
                }
            ]
        },{broadcast:true,sign:true})
        
        console.log("=======================================================================")
        console.log("===================== READ transaction details ========================")
        console.log("=======================================================================")
        console.log(tx, "\n")
        console.log("Response from contract :", tx.processed.action_traces[0].console)
        console.log("\n")
    }catch(error){
        console.log(error)
    }
}

async function update(id, data){
    try{
        const tx = await api.transact({
            actions:[
                {
                    account,
                    name:"update",
                    authorization:[
                        {
                            actor,
                            permission:"active"
                        }
                    ],
                    data:{
                        id, data
                    }
                }
            ]
        },{broadcast:true,sign:true})

        
        console.log("=======================================================================")
        console.log("===================== UPDATE transaction details ======================")
        console.log("=======================================================================")
        console.log(tx, "\n")
        console.log("Response from contract :", tx.processed.action_traces[0].console)
        console.log("\n")
    }catch(error){
        console.log(error)
    }
}

async function destroy(id){
    try{
        const tx = await api.transact({
            actions:[
                {
                    account,
                    name:"destroy",
                    authorization:[
                        {
                            actor,
                            permission:"active"
                        }
                    ],
                    data:{
                        id
                    }
                }
            ]
        },{broadcast:true,sign:true})

        
        console.log("=======================================================================")
        console.log("===================== DESTROY transaction details =====================")
        console.log("=======================================================================")
        console.log(tx, "\n")
        console.log("Response from contract :", tx.processed.action_traces[0].console)
        console.log("\n")
    }catch(error){
        console.log(error)
    }
}


async function main(id, user, data){
    await create(id, user, data)
    await read(id)
    await update(id, data)
    await destroy(id)
}

main(1, account, "CRUD Transaction via JSON RPC")
```
Exit CTRL+X Y ENTER

**8. Run this command**
```
npm run solution
```
