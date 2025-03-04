# Eigen Service
* PKCS
* Transaction History

## Test
`yarn test`

## Usage

### Launch Server
```
forever start ./src/app.js  # or `yarn start` for dev
```

### PKCS
Simple local public key cache service on sqlite, with ecies inside.

```

#query
curl -XGET -H "Content-Type:application/json"  --url "localhost:3000/store?digest=1"

#query all
curl -XGET -H "Content-Type:application/json"  --url "localhost:3000/stores"

# add
curl -XPOST -H "Content-Type:application/json"  --url "localhost:3000/store" -d '{"digest":"1", "public_key":"pk"}'
```
### Transaction History

```
#query
curl -XGET -H "Content-Type:application/json"  --url "localhost:3000/txh?txid=1"
#search all
curl -XGET -H "Content-Type:application/json"  --url "localhost:3000/txhs?action=search&from=0x1"
#add
curl -XPOST -H "Content-Type:application/json"  --url "localhost:3000/txh" -d '{"txid": "1", "from": "0x1", "to": "0x1", "type":0}'
#update
curl -XPUT -H "Content-Type:application/json"  --url "localhost:3000/txh/{txid}" -d '{"status": 1, "sub_txid": "2121"}'
```

## Deployment in production

### Build
```
docker build -t ieigen/service:v1 .
```

### Run
```
docker run --name=eigen-service -d ieigen/service:v1  -p 3000:3000
```

