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
 
## Inspiration

In this world where there are many circulations of fake and unoriginal work, we believe that our smart contract encourages creative thinking and inspires original ideas. 

## What it does

Our smart contract allows the original creator of the NFT to receive a certain % of transaction payment as a type of "**royalty**". Deployed in Gear Technologies' cutting-edge blockchain network, our smart contract allows its users to mint, exchange, and receive a royalty on their NFTs without much effort. 

## How we built it

On top of the standard NFT implementation provided by Gear, we added new features that introduced royalty to the smart contract. The smart contract was written in rust, a highly efficient and versatile programming language. 

## Challenges we ran into

Having little to no prior knowledge of blockchain technology and gear, we had a challenging but rewarding experience at Hoyahacks. We overcame the challenges by attending the workshop provided by Gear and by communicating our challenges to the Gear Mentors. All mentors provided extremely helpful and insightful guidance. 

## Accomplishments that we're proud of

We were able to compile and deploy our smart contract in an existing blockchain. We are especially proud that our smart contract can be used as a template for further development of the NFTs. 

## What we learned

On the technical side, we learned about the abstraction behind blockchain technology and NFTs. We also learned to work with a new language called rust. Most importantly, we learned how to write smart contracts and deploy them to the blockchain network!

## What's next for GEAR - NFT Royalty Payment Smart Contract

We hope to introduce more features to the smart contract.  For instance, we want to add a feature where royalty can be transferred to someone else. Also, we could implement a full-stack marketspace solution to spread the royalty-paying NFTs that are based on our contrast.
