#Project Title: Aave Wallet Credit Scoring System

This project evaluates individual wallets interacting with the Aave V2 protocol by assigning them a credit score ranging from 0 to 1000. 
The scoring mechanism is built on behavioral analysis of transaction-level data—such as deposits, borrowings, repayments, redemptions, and liquidations. 
By identifying responsible versus risky financial actions, the system categorizes wallets into different creditworthiness tiers.

#Overview

Using raw transaction data extracted in JSON format from the Aave V2 decentralized finance (DeFi) platform, this model assesses the financial reliability of each wallet. 
The goal is to quantify trustworthiness based on usage behavior, rewarding consistent repayments and penalizing signs of over-leverage or liquidation.

#Problem Statement

You are provided with sample raw, transaction-level data from the Aave V2 protocol. Each record corresponds to a wallet interacting through actions such as:

    deposit
    borrow
    repay
    redeemunderlying
    liquidationcall

The goal is to develop a model that scores each wallet between 0 (risky/irresponsible) and 1000 (safe/responsible) based on their transaction behavior.

#Data Cleaning

 
The raw transaction data obtained from the Aave V2 protocol was well-structured, with no missing values in critical fields such as wallet address, transaction type, or timestamp.

However, during the feature engineering stage, some derived metrics introduced potential issues. Specifically:

       repay_ratio = total repays / total borrows

       redeem_ratio = total redeems / total deposits

       borrow_deposit_ratio = total borrows / total deposits

These formulas could result in NaN values when the denominator was zero (e.g., no borrow or deposit activity for a wallet).

To maintain the integrity of the scoring process:

    Division-by-zero scenarios were proactively managed using conditional logic.

    For instance, if a wallet had no borrows, its repay_ratio was defaulted to 0.

    Similarly, if no deposits were found, the redeem_ratio was set to 0.

Additionally, wallets exhibiting extremely low or suspicious activity patterns (e.g., fewer than 3 total transactions, potentially bots) were placed in the lowest score bracket to reflect their limited or unreliable participation.

As a result of these cleaning steps, the final dataset used for scoring was free of null values and ready for reliable analysis.

#Feature Engineering

For each wallet, we compute:

##Basic Activity Features:
     ‘total_tx`: Total number of transactions
      total_amount: Sum of all transaction amounts
      deposits, borrows, repays, redeems, liquidations: Count of each action type
			
##Behavior-Based Ratios:
       repay_ratio = repays / (borrows + 1)
       borrow_deposit_ratio = borrows / (deposits + 1)
       redeem_ratio = redeems / (deposits + 1)
			 
##Risk Flags:
       liquidation_flag = 1 if wallet had any liquidationcall, else 0

#Scoring Logic

Each wallet is assigned a raw score using: raw_score = ( 0.25 * total_tx + 0.25 * total_amount + 0.15 * repay_ratio + 0.15 * (1 - liquidation_flag) + 0.10 * borrow_deposit_ratio + 0.10 * (1 - redeem_ratio) )

Then scaled using MinMaxScaler to bring the final score in the range 0 to 1000.

#Score Distribution

Wallet scores are binned into the following ranges:

     (0–100]
     (100–200]
     (200–300]
     (300–400]
     (400–500]
     (500–600]
     (600–700]
     (700–800]
     (800–900]
     (900–1000]

Score Distribution Graph

#How to Run

##Requirements

    Python 3.8+
    pandas, numpy, matplotlib, scikit-learn
	 
		 
		 
		
