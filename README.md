# Tokenized Real Estate Smart Contract

This smart contract implements a tokenized real estate model, allowing property owners to register properties and distribute fractional ownership through shares. Investors can purchase, sell, and receive dividends based on their share ownership.

## Features

- **Property Registration:** Property owners can register properties with essential details, setting a value and tokenizing it into shares.
- **Investor Authorization:** Property owners can authorize investors to participate in the property’s share trading. Only authorized investors can buy shares.
- **Share Purchase and Sale:** Authorized investors can buy or sell shares of a registered property.
- **Dividend Distribution:** Property owners can distribute rental income as dividends to investors proportional to their shareholding.

## Getting Started

### Prerequisites

- Clarity language and development environment (e.g., [Clarinet](https://github.com/hirosystems/clarinet)) for deploying and testing Clarity smart contracts on the Stacks blockchain.

### Contract Structure

- **Data Variables:**
  - `property-counter`: A counter to generate unique IDs for properties.
- **Data Maps:**
  - `properties`: Stores details of each property, including the owner, total shares, share price, and a list of authorized investors.
  - `investors`: Stores each investor’s share balance and authorization status for each property.
- **Event Emitters:** Used to log key events, such as property registration, share purchase/sale, and dividend distribution.

### Functions

#### Public Functions

1. **`register-property`**
   - Registers a new property.
   - Parameters: 
     - `property-value`: The property’s market value.
     - `total-shares`: Total shares issued for the property.
     - `share-price`: Price per share.
   - Returns: The unique property ID.

2. **`authorize-investor`**
   - Authorizes an investor to participate in the property’s share market.
   - Parameters:
     - `property-id`: The unique ID of the property.
     - `investor-wallet`: The investor's principal address.
   - Only the property owner can authorize investors.
   
3. **`buy-shares`**
   - Allows authorized investors to buy fractional shares of a property.
   - Parameters:
     - `property-id`: The property to buy shares from.
     - `shares`: The number of shares to purchase.
   - Investors must have sufficient STX balance for the purchase.

4. **`sell-shares`**
   - Allows investors to sell fractional shares back to the property owner.
   - Parameters:
     - `property-id`: The property to sell shares of.
     - `shares`: The number of shares to sell.

5. **`distribute-dividend`**
   - Distributes rental income as dividends to investors.
   - Parameters:
     - `property-id`: The property ID for which dividends are distributed.
     - `investor-wallet`: The investor’s principal address.
     - `total-income`: Total income to be distributed as dividends.
   - Only the property owner can distribute dividends.

#### Private Functions

- **`get-property`**: Retrieves property details by property ID.
- **`get-investor`**: Retrieves investor details (share balance and authorization) for a specific property.
- **`is-owner`**: Checks if the sender is the owner of the property.

### Error Codes

- `u400`: Invalid input (e.g., zero values for properties or shares).
- `u401`: Unauthorized operation (e.g., non-owner attempting restricted actions).
- `u402`: Unauthorized investor attempting a purchase.
- `u403`: Investor record not found.
- `u404`: Property not found.
- `u405`: Investor already authorized.
- `u406`: Maximum number of authorized investors (50) exceeded.

## Usage Example

To register a property:

```clarity
(register-property u1000000 u100 u100)
```

To authorize an investor:

```clarity
(authorize-investor u1 'SP3FBR2AGKDF9ZT9JZG59QBM01WWT0D3WJ3B5RB9V)
```

To buy shares:

```clarity
(buy-shares u1 u10)
```

To sell shares:

```clarity
(sell-shares u1 u5)
```

To distribute dividends:

```clarity
(distribute-dividend u1 'SP3FBR2AGKDF9ZT9JZG59QBM01WWT0D3WJ3B5RB9V u500)
```

### Events

The contract emits structured print events to log important actions, including `property-registered`, `shares-purchased`, `shares-sold`, and `dividends-distributed`.

## License

This project is open-source and licensed under the MIT License.