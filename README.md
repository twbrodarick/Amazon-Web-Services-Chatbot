# RoboAdvisor 

## Description

* This bot was built to provide users a recommended investment portfolio based on desired risk levels. 
* The portfolio consists of broad stock market (SPY) and bond market proxies weighted according to risk level. 
    1. A higher weighting to **stocks** will be recommended by RoboAdvisor as user risk tolerance inputted is *increased*.
    2. A higher weighting to **bonds** will be recommended by RoboAdvisor as user risk tolerance inputted is *decreased*.

## Tools/Packages Used

* Amazon Web Services
     1. Amazon Lex (Bot build and Intent and Slot creation)
     2. Lambda (code for validation of user input and returning portfolio recommendations)
     
* Xbox Game Bar (Video Demonstration)
     

## Bot Components

### RecommendPortfolio Intent - Utterances

* Seven phrases indicating a need for retirement investment advice are required to engage the bot. They are:
    1. I want to save money for my retirement
    2. I'm ​`{age}​` and I would like to invest for my retirement
    3. I'm `​{age}​` and I want to invest for my retirement
    4. I want the best option to invest for my retirement
    5. I'm worried about my retirement
    6. I want to invest for my retirement
    7. I would like to invest for my retirement

### RecommendPortfolio Intent - Slots

* This bot uses four slots, three using built-in types and one custom slot named `riskLevel`. 


| Name             | Slot Type            | Prompt                                                                    |
| ---------------- | -------------------- | ------------------------------------------------------------------------- |
| firstName        | AMAZON.US_FIRST_NAME | Thank you for trusting on me to help, could you please give me your name? |
| age              | AMAZON.NUMBER        | How old are you?                                                          |
| investmentAmount | AMAZON.NUMBER        | How much do you want to invest?                                           |

The `riskLevel` custom slot is used to retrieve the risk level the user is willing to take on the investment portfolio as follows:

* **Name:** riskLevel
* **Prompt:** What level of investment risk would you like to take?
* **Maximum number of retries:** 2
* **Prompt response cards:** 4

The response cards for the `riskLevel` slot are:

| Card 1                              | Card 2                              |
| ----------------------------------- | ----------------------------------- |
| ![Card 1 sample](Images/card1.png)  | ![Card 2 sample](Images/card2.png)  |

| Card 3                              | Card 4                              |
| ----------------------------------- | ----------------------------------- |
| ![Card 3 sample](Images/card3.png)  | ![Card 4 sample](Images/card4.png)  |

### RecommendPortfolio Intent - Confirmation Prompts

* **Confirm:** Thanks, now I will look for the best investment portfolio for you.
* **Cancel:** I will be pleased to assist you in the future.


### Lambda Function

* Lambda and Test Events were created to achieve the following:

##### User Input Validation

* User `age` should be greater than zero and less than 65.
* the `investment_amount` should be equal to or greater than USD 5,000.
* Violations of these parameters will prompt the user to input valid responses.

##### Investment Portfolio Recommendation

Once the intent is fulfilled, the bot will produce an investment recommendation based on the selected risk level as follows:

* **None:** "100% bonds (AGG), 0% equities (SPY)"
* **Very Low:** "80% bonds (AGG), 20% equities (SPY)"
* **Low:** "60% bonds (AGG), 40% equities (SPY)"
* **Medium:** "40% bonds (AGG), 60% equities (SPY)"
* **High:** "20% bonds (AGG), 80% equities (SPY)"
* **Very High:** "0% bonds (AGG), 100% equities (SPY)"


### RoboAdvisor Files

* ZIP file of RoboAdvisor bot via Amazon Lex platform
* lambda_function.py (Lambda code)
* Bot Demo video
* Text files of 4 error tests used to configure 'recommendPortfolio' lambda function correctly
* PNG files of 4 portfolio recommendations used on response cards

