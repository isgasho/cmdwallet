
![Hacash-banner](https://github.com/AsherManangan/cmdwallet/blob/master/screenshots/Capture.PNG)
Hacash command line wallet usage tutorial
===
The command line wallet is an offline tool. You can use it on a desktop computer that is not connected to the Internet to create accounts,
construct transfer transactions, and so on.

This tool is absolutely safe, because it will not transmit your password or private key on the Internet, everything is occurs in "local" operation.

Because the local command line wallet is not connected to the Internet, it does not support balance query and check. If you need to check the 
balance of an address, you can check on the [online wallet](explorer.hacashpool.com). Since the operation of checking the balance does not
involve a password or private key at all. 


This tutorial will provide the most detailed tutorial for people who do not understand computer technology, and will teach you step by step to 
achieve operations such as creating an address, constructing a transfer transaction, and submitting a transfer transaction.

Ready to work
===
You need to go to [hacash.org](hacash.org) to download the pre-compiled software, and download the corresponding version of the software 
according to your operating system category (Windows or Ubuntu). Then decompress the downloaded ZIP files, then enter the decompressed directory, and then run them (double-click to run under windows, Ubuntu needs to press the right mouse button in the program directory, select "open in terminal", and enter).

Tip: If you can't run a command line program under Ubuntu, please refer to this [tutorial](https://zhidao.baidu.com/question/501887268.html) .
### Start

After the software runs, you will see the following in the window:

```shell script
Welcome to Hacash tool shell, you can:
--------
passwd ${XXX} ${XXX} | prikey ${0xAB123D...} | newkey | accounts | update | log
--------
gentx sendcash ${FROM_ADDRESS} ${TO_ADDRESS} ${AMOUNT} ${FEE} | loadtx ${0xAB123D...} | txs
--------
sendtx $TXHASH $IP:PORT
--------
exit, quit
--------
The use time hold on 2020/08/10 15:32:12, enter'update' change to now
Continue to enter anything:
>

```

This means that the tool has run successfully. Now you only need to input the specified command to complete operations such as creating an account and constructing a transaction.

It's very simple, let's take it step by step:

#### 1. Create an account address by password

Enter `passwd mypassword123456` in the window:
```shell script
Continue to enter anything:
>passwd mypassword123456
```
Then press the Enter key, and you will see the following printed content:

```shell script
>passwd mypassword123456
Loaded your account 
  private key: 0x9f33a504208cfabc1066f04a1592703465775a89d3fc59bcba54538a354330a9 
  address: 1Nk6Vcq4gZM6hJPhjtJYYWHmXRF8wtD7F5
```
Among them, `1Nk6Vcq4gZM6hJPhjtJYYWHmXRF8wtD7F5` is the corresponding account address generated by your password `mypassword123456`. A password corresponds to a unique address, which can be used to collect money or collect mining rewards, etc.

You need to create passwords that are as complex as possible, but not forgotten, and that only you know. If your password is too simple and may be guessed by hackers, or if you leak your password, the coins in your account will be transferred away by others and will never be retrieved.

#### 2. Randomly generate an account

If you don't want to record the password, but are used to randomly generating a private key and corresponding account like Bitcoin, you can enter the `newkey` command:

```shell script
>newkey
```
You will see the following output

```shell script
>newkey
Loaded your account
  private key: 0xecf9549e4a6fa172c2d331fa84c0d72b4e06217ff80bf213c9de284cb7c62218
  address: 1Hd1LabwkyFvsZu5MravwR7KBdKripLLDi
```
`0xecf9549e4a6fa172c2d331fa84c0d72b4e06217ff80bf213c9de284cb7c62218` is the randomly generated private key, `1Hd1LabwkyFvsZu5MravwR7KBdKripLLDi` is the account address. Be sure to back up the private key.

#### 3. Login account

By entering `passwd` or `newkey`, `1Nk6Vcq4gZM6hJPhjtJYYWHmXRF8wtD7F5` and `1Hd1LabwkyFvsZu5MravwR7KBdKripLLDi` two accounts have been recorded in the tool (or called login), the transaction can be transferred from the two addresses during the operation of the tool .

If it is not the first time to open and run this tool, but you have a backup private key, you can log in to the account with the private key by entering the `prikey` command. For example, your private key is `0xecf9549e4a6fa172c2d331fa84c0d72b4e06217ff80bf213c9de284cb7c62218`, then enter it on the command line :
```shell script
>prikey 0xecf9549e4a6fa172c2d331fa84c0d72b4e06217ff80bf213c9de284cb7c62218
```
You can see the print:
```shell script
>prikey 0xecf9549e4a6fa172c2d331fa84c0d72b4e06217ff80bf213c9de284cb7c62218
Loaded your account 
  private key: 0xecf9549e4a6fa172c2d331fa84c0d72b4e06217ff80bf213c9de284cb7c62218
  address: 1Hd1LabwkyFvsZu5MravwR7KBdKripLLDi
```
At this time, `1Hd1LabwkyFvsZu5MravwR7KBdKripLLDi` is recorded in this tool again, and you can construct a transaction for transferring coins from this address.

In other words, you must know the password or private key of an account, and record it into this tool through the `passwd` or `prikey` command, in order to construct a valid transfer transaction.

Moreover, for account security, this tool will not save your password or private key on a certain disk location. Every time you run this tool, you need to enter your password or private key again to log in to your account.

#### 4. Construct a transfer transaction

To construct a transfer transaction, you need to enter four contents: 1. Payment account address, 2. Receiving account address, 3. Payment amount, 4. Handling fee

For example, the address `1Nk6Vcq4gZM6hJPhjtJYYWHmXRF8wtD7F5` needs to transfer 200 HACs to the address `1Hd1LabwkyFvsZu5MravwR7KBdKripLLDi` and set the handling fee to 0.0001 HAC at the same time, then enter the following command:

```shell script
>gentx sendcash 1Nk6Vcq4gZM6hJPhjtJYYWHmXRF8wtD7F5 1Hd1LabwkyFvsZu5MravwR7KBdKripLLDi HAC2:250 HAC1:244
```

Among them, `HAC2:250` means the transfer amount is 200 pieces, and `HAC1:244` means that the transaction fee is 0.0001 pieces. You can see after pressing enter:

```shell script
>gentx sendcash 1Nk6Vcq4gZM6hJPhjtJYYWHmXRF8wtD7F5 1Hd1LabwkyFvsZu5MravwR7KBdKripLLDi HAC2:250 HAC1:244
transaction create success! 
hash: <9eb1d626393a702766892ddea3e91e2022cb9870ea20e766a76401948e15916d>, hash_with_fee: <4f32b5ae2b2f10d60c190d904bcb54939f09f702f2d246fa82dc57772c2a8273>
body length 159 bytes, hex body is:
-------- TRANSACTION BODY START --------
02005f30f7fc00ee811d0d3efe16c1583cfe35af3bbf080771ec7af401010001000100b65144da73d6063bae8cb8e2fd615223a01a2564fa010200010315af4b3de7ad55bf56198ffaea71fbabb3d98d8a5d6d4cb5933a9574de4096b5504a39427b2adbfdc4de12382a0c28de08e29a553328cc25c2d2256026a62a24779f3543de731892f9b1ce815761e407878e18a0d4e8a2869fd53a969e731d830000
-------- TRANSACTION BODY END --------
```
Successfully constructed a sum transfer transaction, the transaction is a hash `9eb1d626393a702766892ddea3e91e2022cb9870ea20e766a76401948e15916d`, trading as` 02005f30f7fc00ee811d0d3efe16c1583cfe35af3bbf080771ec7af401010001000100b65144da73d6063bae8cb8e2fd615223a01a2564fa010200010315af4b3de7ad55bf56198ffaea71fbabb3d98d8a5d6d4cb5933a9574de4096b5504a39427b2adbfdc4de12382a0c28de08e29a553328cc25c2d2256026a62a24779f3543de731892f9b1ce815761e407878e18a0d4e8a2869fd53a969e731d830000` content

However, the transaction at this time still only exists locally, and there is no broadcast blockchain main network to package and confirm. You need to copy the transaction content `9eb1d626.......31d830000` to [Online Wallet](https://wallet.hacash.org/) to submit.

Submitting the constructed transaction to the online wallet is the same as checking the balance, it is also safe, because the transaction content is the signed data, which does not contain your password or private key.

Open the online wallet, find the Send transaction item, copy the copied content, and click "Send Tx" to submit the constructed transfer transaction to the Hacash mainnet:

![](https://raw.githubusercontent.com/hacash/cmdwallet/master/help/sendtx_online.png)

We see that an error is returned at this time: `Send failed: Transaction Add to MemTxPool error: address 1Nk6Vcq4gZM6hJPhjtJYYWHmXRF8wtD7F5 balance ㄜ0:0 not enough, need ㄜ2:250.` Because the address we just created in `1Nk6Vcq4gZMwtW7WJFXRF` is the address we just created. There are no coins (the balance is 0). The transfer can be successful only after purchasing or accepting gifts, or obtaining coins through mining.
