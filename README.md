
# Setting Up OIBetShowcase
Follow these steps to set up OIBetShowcase:

### 1. Deploy the OIToken Contract
Run the script: scripts/deployOIToken. This contract will be used for placing bets and taking profits.

### 2. Deploy the OIBetShowcase Contract
Run the script: scripts/deployBetContract. Before deploying this contract, ensure you correctly set the following addresses:

- OI Token Address: Address of the OIToken contract deployed in step 1.
- Match Result Verification Address:
    - Coston: 0xAa6Cf267D26121D4176413D80e0e851558aa6736
    - Songbird: 0x97C72b91F953cC6142ebA598fa376B80fbACA1C2

### 3. Approve Bet Contract as Spender
Before adding events, approve the bet contract to spend the deployer's OI tokens.

### 4. Add Events to the Contract
Use the script script/createSportEvents to add events with the following parameters:

- string title: Example: "Men's Group Phase - Group A - Australia vs Spain"
- string teams: Example: "Australia,Spain"
- uint256 startTime: Example: 1721980800
- uint8 gender: Example: 0
- uint8 sport: Example: 0 (Refer to the Sports struct in the OIBetShowcase contract)
- string[] choices: Example: ["Australia", "Spain", "Draw"]
- uint32[] initialVotes: Example: [150, 100, 300]
- uint256 initialPool: Example: 100000000000000000000 (100 OI tokens)
- bytes32 _uid: Generated via the generateUID function in OIBetShowcase

### 5. Place Bets
Bets can be placed on any game that has not started yet. Once the game begins, betting is closed.

### 6. Request Match Attestation
After the game concludes, the backend API requests an attestation for the finished match. The attestation request's body includes:

- uint256 date: Timestamp of game start
- uint32 sport: Sport ID
- uint8 gender: Gender ID
- string teams: Example: "Australia,Spain"

### 7. Retrieve Attestation Result
Wait 4-5 minutes for the attestation result. If ready, the attestation proof is available on-chain in the state connector. The backend API retrieves this proof from the Flare API and passes it to the OIBetShowcase contract via the finalizeMatch function.

### 8. Finalize Match
The finalizeMatch function verifies the attestation proof, generates a UID from the request body data, and identifies the corresponding event. If the proof is valid and the event is found, the winner is set.

### 9. Claim Winnings
Users who bet on the winning option can claim their winnings once the winner is set.

### 10. Handle Cancelled or Postponed Matches
For cancelled or postponed matches, authorized addresses can call the cancelSportEvent function. Users who bet on such matches can get a refund of their invested amount using the refund function.