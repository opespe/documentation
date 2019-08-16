# Access Node Reference Configuration and Deployment

## Description: 

**Access Node** : Receives a “JSON Web Token” (JWT), from a Personal Node (PN),  uses it to create a “JSON Web Signature JSON Serialization” (JWS-JS) tally, and sends it Batching Service (BS). 

## Generating JWK-Formatted Keys

Two private keys were generated during account creation that control the Access Node's OPES Blockchain account: the `Community Node Active Private Key` and the `Access Node Work Private Key`. Note that in some cases, these may be the same keys.

The `Access Node Work Private Key` must be translated into the JWK format to be consumed by the Access Node Reference Service. 

That JWK will then be used for the value of the `OPES_ACCESSNODE_JWK` Environment Variable.

### Prerequisites 
- [Docker](https://www.docker.com)

### Key Generation Process

1. Identify the `Access Node Work Private Key` 
   - Note: Remember that Public Keys begin with "OPES", Private Keys do not
2. Identify the owning Community Node's OPES Blockchain Name
   - Note: This name was provided during account creation. 
   - If you do not know this name, [contact Support](mailto:support@opes.one) to retrieve it
3. Run the following commands:
   - Replace `<ACCESS_WORK_PK>` with the `Access Node Work Private Key` 
      - Note: As applicable to your system, escape any `"` characters  (e.g. by placing a leading `\`, `"` -> `\"`)
   - Replace `<COMMUNITY_NODE_NAME>` with the identified Community Node Blockchain Name

   ```
    docker pull opes-key-tools:latest
    docker run --name=<COMMUNITY_NODE_NAME> --private_key=<ACCESS_WORK_PK>
   ```

4. Record the output JWK.
   - Note: This JWK contains your private key! Treat it with the same security as your original private key.  
    
    Example Output
   ```
    -----------------------------------
    Generated JWK:
    { kty: 'EC',
    crv: 'P-256K',
    kid: 'opestestcn01',
    x: '3ioQd8oGyYWabjZJZnXSCgc+nqvlNhp7fgy+AwfyTro=',
    y: 'BQRuA6BM83PRjDfZFa3oIM3z8H1qGabtmxo+jIgZ/50=',
    d: 'GW4RWhBUvttpZLdjD2u5k2g3WIsKtlH0iSmbJZ9jR40=' }

    {"kty":"EC","crv":"P-256K","kid":"opestestcn01","x":"3ioQd8oGyYWabjZJZnXSCgc+nqvlNhp7fgy+AwfyTro=","y":"BQRuA6BM83PRjDfZFa3oIM3z8H1qGabtmxo+jIgZ/50=","d":"GW4RWhBUvttpZLdjD2u5k2g3WIsKtlH0iSmbJZ9jR40="}

    -----------------------------------
   ```

## Helm Deployment

Deploying an Access Node can be accomplished through the use of Helm and the [Access Node Helm Chart](https://github.com/opespe/helm-charts/tree/master/charts/accessnode). Read and follow the instructions in that repository to deploy an Access Node.
