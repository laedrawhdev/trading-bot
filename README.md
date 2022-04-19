# trading stock-bot
trading bot developed
name: Unit Tests

on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]

jobs:
  build:

    runs-on: ubuntu-latest

    steps:
    - uses: actions/checkout@v2
    - name: Set up Python 3.9
      uses: actions/setup-python@v2
      with:
        python-version: 3.9
    - name: Find typos with codespell
      uses: codespell-project/actions-codespell@master
      with:
        ignore_words_list: hist
        skip: "*.json,./tests/unit_tests/responses"
    - uses: actions/cache@v2
      with:
        path: ${{ env.pythonLocation }}
        key: ${{ env.pythonLocation }}-${{ hashFiles('requirements.txt') }}
    - name: Install dependencies
      run: |
        python -m pip install --upgrade pip
        pip install flake8 pytest mock pytest-mock
        if [ -f requirements.txt ]; then pip install -r requirements.txt; fi
    - name: Lint with flake8
      run: |
      . Close 6/10 put option positions once price of stock/share has reached $0.20 below signal candle's closing price
take profit 2. Close 2/10 put option positions once price of stock/share has reached $0.35 below signal candle's closing price
        # stop the build if there are Python syntax errors or undefined names
        flake8 . --count --select=E9,F63,F7,F82 --show-source --statistics
        # exit-zero treats all errors as warnings. The GitHub editor is 127 chars wide
        flake8 . --count --exit-zero --max-complexity=10 --max-line-length=127 --statistics
    - name: Test with pytest
      run: |
        pytest tests/unit_tests
