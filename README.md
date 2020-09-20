# Lifestyle advices based on the user transaction data

> Solution produced during "Advice Hackathon" by Tinkoff as part of the "Hack Lab" course in Skotech, September 18-20, 2020
>
> Team PEPEtoners: [Ilya Borovik](https://github.com/ilya16), [Vladislav Kniazev](https://github.com/Vladoskn), [Vanessa Skliarova](https://github.com/Vanessik), [Bulat Khabibullin](https://github.com/MrWag2), and [Zakhar Pichugin](https://github.com/zakharpichugin)

## Solution

The solution is a lifestyle advices system which suggests a user a certain lifestyle (e.g. `healthy food`, `social Life`, `responsible consumption`, etc.) based on user transaction data in the previous months and user demographic profile.

* The model trained on the transaction data learns to predict the categories in which a user is most likely to make transaction in the following months. 
* The model bases its predictions both on transaction-based data (`merchant_type`, `transaction_type_desc`, `category`, `financial_account_type_cd`, `day` (of month), `weekday`) and user profile information (`gender_cd`, `age`, `marital_status_desc`, `children_cnt`, `region_flg`)
* The predicted probability distribution over can be used to trigger lifestyle advices to a user and monitor the performance of a user (if he/she follows advices or not)
* Over the time, with new transactions, the system may update the user profile and issue new advices to the user.

The business side of the solution is shortly presented in the [video](https://youtu.be/LjEsjwgG4ps).

## Files
* [baseline_improved.ipynb](baseline_improved.ipynb)
  * Improved baseline solution including feature enfineering and model training 
* [category_recommendation.ipynb](category_recommendation.ipynb)
  * The same solution pipeline used to predict 36 categories instead of 458 merchant types
* [demo.ipynb](demo.ipynb)
  * Demonstration of how advices work.
  * Demo limitation: precomputed category recommendations for users. In the real system, the model accepts user transaction history and issues advice recommnedations directly.
* [category_scores.csv](category_scores.csv)
  * Precomputed with a trained model category recommendations for each user, used in the demo
* [category_mappings.json](category_mappings.json)
  * Dictionary map between categories and ids
  
## Baseline improvements
* Fixed bug with mappings (`<UNK>` token index)
* Transactions sorted by date for each party
* Features:
  * Transaction-based: `merchant_type`, `transaction_type_desc`, `category`, `financial_account_type_cd`, `day` (of month), `weekday` 
  * User profile: `gender_cd`, `age`, `marital_status_desc`, `children_cnt`, `region_flg`
* Tuning the `TransformerEncoder` model
