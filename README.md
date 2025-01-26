## Overview
This project implements a vault program on the Solana blockchain using the Anchor framework. The vault allows users to deposit and withdraw SOL tokens securely, as well as initialize and close their vault accounts. The program utilizes Program Derived Addresses (PDAs) for secure account management.

## Table of Contents
- [Installation](#installation)
- [Project Structure](#project-structure)
- [Program Logic](#program-logic)
  - [Initialization](#initialization)
  - [Deposit](#deposit)
  - [Withdraw](#withdraw)
  - [Close](#close)
- [Testing](#testing)
- [Usage](#usage)
- [Error Handling](#error-handling)
- [Contributing](#contributing)
- [License](#license)

## Installation
1. Clone the repository:
   ```bash
   git clone https://github.com/yourusername/solana-vault-program.git
   cd solana-vault-program
   ```

2. Install the required dependencies:
   ```bash
   anchor build
   ```

3. Ensure your Solana wallet is set up and funded on the devnet.

## Project Structure
The project consists of several key files:

| File                  | Description                                                   |
|-----------------------|---------------------------------------------------------------|
| `lib.rs`              | Contains the main logic of the vault program, including methods for initialization, deposits, withdrawals, and closing accounts. |
| `solana_anchor.ts`    | Contains tests for the vault program using the Anchor testing framework. |

## Program Logic

### Initialization
The `initialize` function sets up a new vault account for a user. It creates a state account that holds the vault's metadata.

```rust
pub fn initialize(ctx: Context<Initialize>) -> Result<()> {
    ctx.accounts.initialize(&ctx.bumps)?;
    Ok(())
}
```

### Deposit
The `deposit` function allows users to deposit SOL into their vault. It transfers an amount from the user's account to the vault's account.

```rust
pub fn deposit(ctx: Context<Payment>, amount: u64) -> Result<()> {
    ctx.accounts.deposit(amount)?;
    Ok(())
}
```

### Withdraw
The `withdraw` function enables users to withdraw SOL from their vault back to their account.

```rust
pub fn withdraw(ctx: Context<Payment>, amount: u64) -> Result<()> {
    ctx.accounts.withdraw(amount)?;
    Ok(())
}
```

### Close
The `close` function allows users to close their vault account and transfer any remaining SOL back to their wallet.

```rust
pub fn close(ctx: Context<Close>) -> Result<()> {
    ctx.accounts.close()?;
    Ok(())
}
```

## Testing
To run tests for the vault program, execute the following command:

```bash
anchor test
```

The test file `solana_anchor.ts` contains a basic structure for testing the program's functionality. You can expand this file with additional test cases as needed.

## Usage
1. **Deploy the Program**: Deploy your program to the Solana devnet using:
   ```bash
   anchor deploy --provider.cluster devnet
   ```

2. **Interact with the Program**: You can interact with your deployed program using client-side scripts or through a frontend application that connects to Solana.

3. **Example Commands**:
   - Initialize a vault:
     ```javascript
     const tx = await program.methods.initialize().rpc();
     console.log("Your transaction signature", tx);
     ```
   - Deposit funds:
     ```javascript
     const tx = await program.methods.deposit(new anchor.BN(amount)).rpc();
     console.log("Deposit transaction signature", tx);
     ```

## License
This project is licensed under the MIT License - see the LICENSE file for details.
