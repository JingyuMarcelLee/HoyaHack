# HoyaHack Team 15: Bored Hack Yacht Club

## Track: Gear Track Bronze Tier Project - Option 2
For every NFT sale / transaction, there could be a royalty bonus associated with it. We ask you to extend the NFT interface to allow assigning royalty amount to NFT and implement corresponding functionality.

## Project Title: Royalty NFT Smart Contract
We introduced functions below to the original example provided by Gear Technologies. 


### royalty()
```rust    fn royalty(&mut self, token_id: U256, price: u64) {
        if !self.token.exists(token_id) {
            panic!("NonFungibleToken: Token does not exist");
        }
        let multiplier = *self.royalty_rate.get(&token_id).unwrap_or(&5);
        msg::reply(
            Event::Royalty {
                amount: price*multiplier/100,
                origin: *self.origin_by_id.get(&token_id).unwrap_or(&ZERO_ID),
            },
            0,
            0,
        );
```
The royalty() function takes in token_id and the price as its parameter to calculate the amount of royalty given to the original creator of the token. Once passed in, price is multiplied with a rate defined by assignroyalty() function below. If the rate has not been assigned, a default rate of 5 is multiplied to the price. Returns the amount and origin, which is also the receipient of the royalty, as a reply to the message. 

### assignroyalty()
```rust     fn assignroyalty(&mut self, token_id: U256, rate: u64) {
        if !self.token.exists(token_id) {
            panic!("NonFungibleToken: Token does not exist");
        }
        msg::reply(
            Event::AssignRoyalty {
                token_id,
                recipient: *self.origin_by_id.get(&token_id).unwrap_or(&ZERO_ID),
            },
            0,
            0,
        );
        self.royalty_rate.insert(self.token_id, rate);
    }
 ```
 The assignroyalty() function takes in token_id and the rate as its parameter and assign this rate with token_id as the key into a BTreeMap called royalty_rate. This way, each NFT token may have a different rate with one another. 
