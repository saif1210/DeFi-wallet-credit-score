# Wallet Score 

This analysis is based on the credit scoring of wallets interacting with the Aave V2 protocol. The scoring model assigns a value between 0 and 1000, where a higher score indicates more reliable and responsible behavior.

# Score Distribution


<img width="870" height="554" alt="Screenshot 2025-07-19 135600" src="https://github.com/user-attachments/assets/b1788325-eb16-475d-aad5-824eae6f6bfa" />

The majority of wallets lie in the 400–600 range, indicating a typical mix of activity. A small portion exhibit extremely risky or highly trustworthy behavior.

# Behavior of Wallets

## Lower Score Range (0–300)

Wallets in this range tend to show:

     Low number of transactions
     One-time or bot-like patterns (e.g., deposit + immediate redeem)
     High liquidation flags
     No repayments
     Low borrow-to-deposit ratio
     Typically non-serious or possibly exploitative usage
     
These users are assigned low scores to reflect poor or untrustworthy activity.

## Higher Score Range (700–1000)

Wallets in this range show:

      Consistent transactions over time
      High repay ratios
      Balanced borrow and deposit behavior
      No liquidations
      High activity scores (more interactions and amount)
      
These users are likely long-term, responsible participants in the protocol.

