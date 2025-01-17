![alt text](img/works_with_ynab.png "Works with YNAB!")

# Random Reward for YNAB
A script that uses an existing YNAB budget and the power of intermittent reinforcement to incentivize you to complete tasks. It uses the YNAB API to stochastically transfer money to a fun money category you set every time you finish a task. 

## Prerequisites
Random Reward for YNAB (RRY) requires the following Python libraries for functionality:

* [Requests](https://requests.readthedocs.io/en/master/)
* [Arrow](https://arrow.readthedocs.io/en/stable/)

Ensure that these are installed before proceeding.

## Installation and Setup
First, you need to download a copy of RRY onto your computer. This can be done in a number of ways. You can clone the repo onto your local machine by using the command below:

```shell
$ git clone https://github.com/andromedateevens/random_reward_for_ynab && cd random_reward_for_ynab
```

You can also download the project as a zip file. To do this, find the green button labelled Code, then click on "Download ZIP"

![alt text](img/download_zip.png "Download as zip")

Once you have downloaded the project, you will need to edit `parameters.json` to correspond to your YNAB setup. If you open that file you will see the following:

```shell
{
    "token": "Put Token Here",
    "budget_name": "My Budget",
    "budget_id": null,
    "category_from_name": "Reward Money",
    "category_from_id": null,
    "category_to_name": "Fun Money",
    "category_to_id": null,
    "amount": 1.0,
    "random_threshold": 0.5
}
```

We will go through each of these parameters in turn. First of all you will need a security token, which allows RRY to communicate with your YNAB account. You can use [this guide from YNAB](https://api.youneedabudget.com/#personal-access-tokens) to create a token. Copy the token to your clipboard and replace "Put Token Here" with it, keeping the quotation marks. IMPORTANT NOTE: Do not share your token with anyone. Use it only with your local copy of RRY.

Besides the token, the remaining paramters are largely self-explanatory. Budget and category IDs should be left as null, as they will be assigned by `setup.py`; if for some reason you want to enter them manually you may, but this is not recommended. Budget and category names must match exactly, including spaces and capitalization. `category_from` refers to the category you wish to transfer money out of, and `category_to` refers to the category you wish to transfer money into. `amount` is the amount of money in dollars that should be transferred. `random_threshold` is the probablity that money will be transferred each time you run RRY. The default value of 0.5 corresponds to a 50% chance for transfer each time; 0.1 would correspond to 10%, and so on.

Once you have set the parameters to refelct your YNAB setup, run `setup.py` using the following command:

```shell
~/.../random_reward_for_ynab$ python setup.py
```

Assuming `setup.py` does not encounter an error, you are now ready to begin random rewards!

## Usage
The idea behind RRY is that intermittent reinforcement is more effective than consistent reinforcement; if you recieve an award every time you complete a task you will complete that task as often as you want the reward (assuming the task is easy). However, if you recieve a reward a random percentage of the time that you complete a task, you will be more likely to complete the task due to the unpredictibility of the reward. With that in mind, you should run RRY when you complete a task using the following command:

```shell
~/.../random_reward_for_ynab$ python random_reward.py
```

RRY will then generate a random number and transfer money into your designated account if that number is greater than `random_threshold`. Enjoy your intermittent reinforcement!