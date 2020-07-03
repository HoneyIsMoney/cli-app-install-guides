# Install Redemptions


> - A line break after a command for eg. `dao new $f`, this means you must create an environment variable, you can stores these in the block provided
> - Commands without line breaks can be run as pasted into the terminal together and run synchronously

Three permissions need to be created for the Redemptions app to function properly

* `REDEEM_ROLE`
* `ADD_TOKEN_ROLE`
* `REMOVE_TOKEN_ROLE`

The Redemptions app must also have the `TRANSFER_ROLE` permission on Vault and the `BURN_ROLE` permission on the Token Manager.

**NOTE** if `TRANSFER_ROLE` and `BURN_ROLE` are not already set you must use `acl create`


<br>

### Envoronment Variables 

```bash
f="--env aragon:rinkeby"
ANY_ADDRESS=0xffffffffffffffffffffffffffffffffffffffff
dao=
vault=
tokenManager=
voting=
redemptions="NEW_REDEMPTIONS_ADDRESS"
```

<br>

### Commands


```bash
aragon dao install $dao redemptions.aragonpm.eth --app-init-args $vault $tokenManager ["'Redemable_Token_Address1', 'Redemable_Token_Address2'"]

dao acl create $dao $redemptions REDEEM_ROLE $ANY_ADDRESS $voting $f
dao acl create $dao $redemptions ADD_TOKEN_ROLE $voting $voting $f
dao acl create $dao $redemptions REMOVE_TOKEN_ROLE $token $voting $f
dao acl grant $dao $vault TRANSFER_ROLE $redemptions $f
dao acl grant $dao $tokenManager BURN_ROLE $redemptions $f
```