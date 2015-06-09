# opreturnio
Analytics on top of op_return data from the bitcoin blockchain

# Preparation
## Bitcoin SQL DB Node Setup
- create AWS EC2 instance
- sudo apt-get update
- sudo apt-get install postgresql postgresql-contrib
- sudo -i -u postgres
- wget http://dumps.webbtc.com/bitcoin/bitcoin_2015-06-08.sql.gz
- psql echo "create database bitcoin" | psql
- zcat bitcoin_YYYY-MM-DD.sql.gz | psql bitcoin

wait 8-10 hours

## Queries

Get count of bitccoin transactions with OP_RETURN in output

>bitcoin=\# SELECT count(tx_id) from txout where encode(pk_script,'hex') LIKE '6a%';

Alter table

>ALTER TABLE txout ADD pk_script_string text;

Update table

> UPDATE txout SET pk_script_string = encode(pk_script,'hex');
