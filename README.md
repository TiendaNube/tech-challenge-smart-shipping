# Tech Challenge - Smart Shipping

## The challenge
Shipping costs are expensive. Our team is working to validate a business concept to offer better options of shipping for our merchants and their consumers.
Your challenge is to build a PoC and validate the usability of our business concept.

## Functional requirements
- We want a RESTful API that given different shipping options from our external API , is able to recommend the same shipping options ordered by the best combination of cost and time.

## Technical requirements
- Write down unit tests for the main logic

- The response must have the shipping option fields:
```code
name: required, text
type: required, text
cost: required, decimal
estimated_days: required, numeric
```

### Considerations
- If there’s no shipping options available, the response should be an empty list;
- You can use our external API v1/shipping_options endpoint in your implementation. <strong>Note: our external API returns a random response for each request.</strong>
- You must use the [acceptance criteria](#acceptance-criteria) to write down unit tests, mocking the shipping options and asserting the expected response. 

## Acceptance Criteria
### Same shipping costs and estimated delivery dates

#### Shipping options:

```json
[{"name":"Option 1","type":"Delivery","cost":10,"estimated_days":3},
{"name":"Option 2","type":"Custom","cost":10,"estimated_days":3},
{"name":"Option 3","type":"Pickup","cost":10,"estimated_days":3}]
 ```

#### Expected response:

```json
[{"name":"Option 1","type":"Delivery","cost":10,"estimated_days":3},
{"name":"Option 2","type":"Custom","cost":10,"estimated_days":3},
{"name":"Option 3","type":"Pickup","cost":10,"estimated_days":3}]
```


### Same shipping costs, different estimated delivery dates

#### Shipping options:

```json
[{"name":"Option 1","type":"Delivery","cost":10,"estimated_days":5},
{"name":"Option 2","type":"Custom","cost":10,"estimated_days":2},
{"name":"Option 3","type":"Pickup","cost":10,"estimated_days":3}]
```

#### Expected response:

```json
[{"name":"Option 2","type":"Custom","cost":10,"estimated_days":2},
{"name":"Option 3","type":"Pickup","cost":10,"estimated_days":3},
{"name":"Option 1","type":"Delivery","cost":10,"estimated_days":5}]
```


### Same estimated delivery dates, different shipping costs


#### Shipping options:

```json
[{"name":"Option 1","type":"Delivery","cost":6,"estimated_days":3},
{"name":"Option 2","type":"Custom","cost":5,"estimated_days":3},
{"name":"Option 3","type":"Pickup","cost":10,"estimated_days":3}]
```

#### Expected response:

```json
[{"name":"Option 2","type":"Custom","cost":5,"estimated_days":3},
{"name":"Option 1","type":"Delivery","cost":6,"estimated_days":3},
{"name":"Option 3","type":"Pickup","cost":10,"estimated_days":3}]
```


### Both shipping costs and estimated delivery dates are different

#### Shipping options:

```json
[{"name":"Option 4","type":"Delivery","cost":10,"estimated_days":3},
{"name":"Option 1","type":"Delivery","cost":10,"estimated_days":5},
{"name":"Option 2","type":"Custom","cost":5,"estimated_days":4},
{"name":"Option 3","type":"Pickup","cost":7,"estimated_days":1}]
```

#### Expected response:

```json
[{"name":"Option 2","type":"Custom","cost":5,"estimated_days":4},
{"name":"Option 3","type":"Pickup","cost":7,"estimated_days":1},
{"name":"Option 4","type":"Delivery","cost":10,"estimated_days":3},
{"name":"Option 1","type":"Delivery","cost":10,"estimated_days":5}]
```

### No shipping options available

#### Shipping options:
```json
[]
```

#### Expected response:
```json
[]


