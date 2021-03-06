# mortgage-rates-service
API for Canadian Bank Mortgage Rates

## Design

1. Restful end-point using Node.js with express.js, restify, or hapi 
1. Hosting will be on AWS Lambda and API Gateway
1. All logs to stdout using console.log, console.error and etc. to be captured by CloudWatch Logs automatically

## Sample Request #1

```
GET /
```
## Sample Response #1

```
{
  "mortgages": [
    {
      "provider": "Canadian Lender",
      "rates": [
        {
          "type": "5-years-fixed",
          "rate": 2.45,
          "comment": "Prime - 1.25"
        },
        {
          "type": "3-years-fixed",
          "rate": 3.34
        },
        ... more rates ...
      ]
    },
    {
      "provider": "Peoples Trust",
      "rates": [
        {
          "type": "5-years-fixed",
          "rate": 2.50,
          "comment": "Prime - 1.20"
        },
        {
          "type": "3-years-fixed",
          "rate": 3.39
        },
        ... more rates ...
      ]
    },
    ... more providers ...
  ]
}
```

## Sample Request #2

```
GET /Canadian%20Lender
```
## Sample Response #2

```
{
  "mortgages": [
    {
      "provider": "Canadian Lender",
      "rates": [
        {
          "type": "5-years-fixed",
          "rate": 2.45,
          "comment": "Prime - 1.25"
        },
        {
          "type": "3-years-fixed",
          "rate": 3.34
        },
        ... more rates ...
      ]
    }
  ]
}
```

## Source Data

https://www.ratehub.ca/banks/bank-mortgage-rates loaded and parsed in real-time

## Development Setup

1. Clone the repository
2. Install dependencies from the repository root folder using terminal window: `npm install`
3. To run unit tests from a terminal window: `npm test`

## Deployment

1. Initialize aws-cli: `aws configure`
2. Create lambda: `chmod +x ./aws/*.sh && ./aws/create-lambda.sh mortgage-rate-service`
3. Create api-gateway: 
```bash
sudo python3.6 -m pip install boto3 \
   && python3.6 ./aws/create-api.py mortgage-rate-service
```

## How to contribute

1. Fork the repo
2. Make changes and commit to your own repository
3. Submit a pull request back into this repository
