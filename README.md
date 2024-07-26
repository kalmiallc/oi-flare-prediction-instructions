
# Flare Olympics Prediction Showcase

Welcome to Flare Olympics Prediction, an innovative on-chain prediction system utilizing Flare Oracle Data connector to enhance your prediction experience with Olympic sports data.

This showcase was developed in cooperation with:

- Kalmia: https://kalmia.si/
- AF Labs: https://aflabs.si/

This is an open source project.

The complete showcase consists of four repositories:

- [Prediction smart contract](https://github.com/kalmiallc/oi-prediction-smartcontract)
- [Front-end application](https://github.com/kalmiallc/oi-prediction-webapp)
- [Backend application](https://github.com/kalmiallc/oi-prediction-backend) which calls the verification provider API for verification
- [Verification server](https://github.com/kalmiallc/oi-match-attestation-server)

The complete guide can be found [here](https://github.com/kalmiallc/oi-flare-prediction-instructions)

If you are interested in own implementation, check the instructions [here](INSTRUCTIONS.md)

## What is Flare Olympics Prediction Showcase?

**Note**: This application is intended for testing purposes only. There is no real business value behind.

Flare Olympics Prediction Showcase is a decentralized sports prediction application designed specifically for the Olympics. Users can place predictions on various team sports events with simple outcomes: win, lose, or draw. This open-source project showcases the powerful capabilities of Flare's advanced features, ensuring that sports results are directly reflected on the blockchain for secure and transparent predictions.

## Key Features

- **User-Friendly Interface**: The frontend is designed for ease of use, allowing you to deposit funds, place predictions, and withdraw winnings efficiently using your wallet credentials.
- **Flare Data Connector**: This application leverages the Flare Data Connector to fetch Olympic match results from Web2 sources and relay them to the blockchain. The data is verified by Flare's attestation providers, ensuring accuracy and reliability.
- **Full dApp Integration**: Seamlessly integrates with smart contracts for a decentralized prediction experience, handling all interactions securely on-chain.
- **Dynamic Prediction Multipliers**: The prediction logic uses dynamic multipliers to ensure fair and balanced payouts based on the pool of predictions.

## How It Works

1. **Place Prediction**: Use your wallet to deposit funds and place prediction on Olympic events.
2. **Data Verification**: The Flare Data Connector fetches and verifies match results from multiple online sources, processed with the help of OpenAI.
3. **Secure Payouts**: Verified results are used by the smart contract to manage payouts, ensuring transparency and security.

Key points:

- Predictions can be placed using the OI tokens. Every user can get 500 OI tokens per day. 
- Predictions can be placed until the match starts. No predictions are allowed once the match has begun.
- The maximum prediction is 10% of the pool size.
- Predictions can be claimed after the final results are finalized, which is expected to be approximately 2 hours after the match's expected end time.
- If the match is canceled, the invested funds can be withdrawn 14 days after the match start time (only supported by the contract).

## Components

To fully set up and run the Flare Olympics Prediction system, the following components need to be in place:

- **Prediction Smart Contract**: Manages all prediction logic and interactions.
- **Front-End Application**: User interface for placing predictions and managing funds.
- **Backend Application**: Calls provider API for verification.
- **Verification Server**: Ensures the integrity of match results data.

## Prediction Logic

The prediction logic operates on dynamic multipliers. Users purchase multiplied amounts (prediction amounts multiplied by the win multiplier). When a prediction is placed, the multiplied amount is stored, guaranteeing the claim amount will be paid when the event concludes.

All multiplied predictions for each game are placed in a prediction pool. The sum of amounts for each choice cannot exceed the total predictions in the pool.

The multiplier is calculated each time a user places a prediction. The number of predictions against the complete pool defines the multiplier factor. The more predictions placed on one choice, the lower the multiplier factor for that choice, and the higher the multiplier factors for other choices.

An initial pool and factors need to be set by the administrator, along with the initial pool of tokens. Each prediction can only be 1/10 of the pool size.

## Flare Data Connector - Results

The results of each match are provided using the [Flare Data Connector](https://flare.network/dataconnector/). The documentation for the connector can be found [here](https://docs.flare.network/tech/state-connector/).

The project provides its own attestation type, the `Match result` attestation type. This attestation type defines how data can be verified by the attestation providers. To identify the match, data is mathed against date,sport,gender and teams.

This attestation is specific to one event (Olympic games) but can be easily extended to other team sports.

A verifier server is implemented for the defined `Match result` attestation type. For this attestation type, the verifier server calls a Web2 API, which returns the match results. If the data aligns with the expected results, it is considered valid. The verifier server is used by the attestation provider. If the verification passes, the data is passed to a voting round and then included in the Merkle tree, which is use to pass the data to the contract.

More developer oriented documentation can be found [here](https://github.com/flare-foundation/songbird-state-connector-protocol/blob/main/README.md)

Flare Olympics Prediction is compatible with both the Coston and Songbird networks, showcasing its flexibility and interoperability.

By utilizing the Flare Data Connector, Flare Olympics Prediction demonstrates how decentralized applications can effectively use external data to provide a seamless and trustworthy prediction experience on the blockchain.


## License

This project is licensed under the MIT License - see the [LICENSE.md](LICENSE.md) file for details.

