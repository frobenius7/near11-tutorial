# near11-tutorial - NEAR Command Line Interface 101 

This is small tutorial about know
In this maunal i will show you some usdeful examples of near CLI

## Prerequisite (what you need to do before start)
1.Basic experience of using command line (terminal) interface on Mac\Linux\powershell

2.NEAR account (we will use testnet) 

for more information refer to https://docs.near.org/docs/develop/basics/create-account

3.NEAR CLI installeed 

for more information refer to https://docs.near.org/docs/tools/near-cli#setup


# First step - Login 

To use the near CLI you need to login via your account.

You can do it by typing in the following command in your terminal 

`near login`

You will be redirected to NEAR Wallet requesting full access to your account. (WEB Browser)
you should select which account you would like an access key to.

In case of success you will see something like this:
>Logged in as [ vetal.testnet ] with public key ..... successfully

# Second step - setting up alias  

To follow instuctions from this tutorial in a more simple way(just copy\paste commands) we will set a "alias" for your account ID. Replace YOUR_ACCOUNT_NAME with the account name you just logged in in step one with including the .testnet (or .near for mainnet):

`export ID=YOUR_ACCOUNT_NAME`

to check if everything is OK you can type
`echo $ID`
then you will see something like this with your name
>echo $ID

>vetal.testnet

# Third step - creating a sub-account 

Sub-accounts is useful for testing smart contracts or other cool things with NEAR using the same login. 

It is like subdomains within main domain in WWW.

Lets name our sub account `cool-sub-account` 

we will use `near create-account` command with 2 additional arugemnts 

`--masterAccount` for the name of our main account

`--initialBalance` for the setting up initial balance of our sub account - by default it sends 100 NEAR, but we don't want to waste so much of beautiful NEAR Tokens =)

`near create-account cool-sub-account.$ID --masterAccount $ID --initialBalance 10`

In case of success you will see somtething like this
>Account cool-sub-account.vetal.testnet for network "testnet" was created.

let's check this acc balance by using command `near status`

`near status cool-sub-account.$ID`

you will see somtething like this
>Account cool-sub-account.vetal.testnet
{
  amount: '10000000000000000000000000',
  locked: '0',
  code_hash: '11111111111111111111111111111111',
  storage_usage: 182,
  storage_paid_at: 0,
  block_height: 73612275,
  block_hash: 'LCENzNiJNgjAASxqfajWZNi2QT6RRuXnRdgBKsBuViv',
  formattedAmount: '10'
}

cool! we have 10 of Near on this account (see `formattedAmount` parameter 

# Fourth step - transferring some NEAR tokens from one account to another 

Lets transfer 5 NEAR tokens from subaccount to main account!

We will use `send` command` with 3 arguments 

`senderID` (who will send tokens) 

`reciver` (who will recieve tokens)

`amount` (amount of NEAR tokens to transfer)

lets try this and send some tokens:
`near send cool-sub-account.$ID $ID 5`

you will see (if you have enogugh balance)
>Sending 5 NEAR to vetal.testnet from cool-sub-account.vetal.testnet
Transaction Id 2pizpfyC5ocj4mesSKmw3saQ3N4vtfyHdgoQC38pWP9c

so if we repeat command `near status cool-sub-account.$ID` we will see that only 5 tokens left..
>Account cool-sub-account.vetal.testnet
{
  amount: '4999955363487500000000000',
  locked: '0',
  code_hash: '11111111111111111111111111111111',
  storage_usage: 182,
  storage_paid_at: 0,
  block_height: 73613119,
  block_hash: '35NiQvwAWzXgzhEgUgh5fh7ZCrUEApHQEhgsMS8UY9yd',
  formattedAmount: '4.9999553634875'
}

# Fifth step - deleting a sub-account

Now let's do the "cleanup" and delete this sub-account (and transfer all remaining balances to main account)
We can do this using `near delete` command with following parameters

`accountID` - account to delete

`beneficaryID` - who will get tokens from deleted account

so lets go!
'near delete cool-sub-account.$ID $ID'
bye-bye sub-account! 
>Deleting account. Account id: cool-sub-account.vetal.testnet, node: https://rpc.testnet.near.org, helper: https://helper.testnet.near.org, beneficiary: vetal.testnet
Transaction Id GzqHyjz7hD9vBaDWUQNJtzCNg1D3QtKdxTqWR4MRBYWa
To see the transaction in the transaction explorer, please open this url in your browser
https://explorer.testnet.near.org/transactions/GzqHyjz7hD9vBaDWUQNJtzCNg1D3QtKdxTqWR4MRBYWa
Account cool-sub-account.vetal.testnet for network "testnet" was deleted

# Thats all for today! =)
