# Structural Pullback Backtest
Rule based structural bullish pullback strategy backtested on 15-min OHLC data.

This project implements and backtests a rule-based structural pullback trading strategy using 15-minute OHLC market data.  
The objective of the project was to analyse market behaviour, develop a clean trading idea, convert it into explicit rules, and evaluate the idea through a Python backtesting framework.

The project focuses on clear thinking and transparent implementation rather than complex indicator stacking.


## Dataset

The strategy is tested on an anonymised OHLC dataset containing approximately **28,000 observations of 15-minute candles**.

Each observation contains the following fields:

timestamp, open, high, low, close

The dataset spans multiple years of market behaviour and includes both sideways and trending regimes.


## Strategy Idea

From the dataset analysis, distinct periods of **bullish structural behaviour** were observed where prices show a persistent upward bias with periodic pullbacks.

The core hypothesis of the strategy is:

During a bullish structural regime, short-term pullbacks often create favourable entry opportunities before the broader upward structure resumes.

Therefore the strategy focuses on:

• Identifying a **bullish market regime**  
• Detecting **short-term pullbacks (local lows)** within that regime  
• Entering trades during these pullbacks  
• Exiting when the bullish structure weakens or momentum fades

Rather than trading across all market conditions, the strategy activates **only during bullish regimes** identified in the dataset.


## Trading Logic

### Market Condition

Trades are taken only when the market exhibits **structural bullish behaviour**.

A bullish regime is defined as the price remaining above a long-term moving average, capturing the overall upward bias of the market while allowing temporary pullbacks.


### Entry Rule

A trade is entered when a **confirmed local low** forms during a bullish regime.

A local low represents a short-term pullback where:

• the price approaches a recent minimum  
• the price subsequently shows an upward response within a short window

This ensures that entries occur during pullbacks rather than at random price levels.


### Exit Rules

Two exit conditions are used.

**Exit if trade goes wrong**

If price shows structural weakness and breaks below recent support levels, the trade is exited to limit losses.

**Exit if trade goes right**

If price moves upward after entry but begins to show loss of momentum, the position is closed to lock profits.


## Backtesting Framework

The strategy is implemented in Python using:

• pandas  
• numpy  
• matplotlib  

Trades are executed on **15-minute candles using close-to-close prices**.

Execution assumptions:

• Only one trade is active at a time  
• A new trade is entered only after the previous trade has been closed  
• No leverage, slippage, or transaction costs are assumed


## Results

Backtesting across the dataset produced the following results:

Total Return: **14.69%**  
Sharpe Ratio: **0.053**  
Maximum Drawdown: **-3.9%**  
Total Trades: **1944**

These results illustrate how the structural pullback logic behaves across different market regimes within the dataset.


## Repository Structure


structural-pullback-backtest/

data_set/
    train_data1.csv

backtester/
    backtester.ipynb

report/
    Algo Trading Report.pdf

trade_log/
    trade_log.csv

rough_work/
    ROUGH WORK_ALGO STRATEGY.pdf



## Project Components

**Report**

Detailed explanation of the dataset analysis, ideation process, strategy design, and backtest results.

**Backtester**

Python notebook implementing the trading rules and generating performance metrics.

**Trade Log**

Complete log of trades generated during the backtest.

**Rough Work**

Initial handwritten analysis and observations that led to the development of the strategy.
