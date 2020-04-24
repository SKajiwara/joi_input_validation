# joi_input_validation
Joi is a very popular user input validation library on npm. Weekly Downloads are over 2 millions. It is managed by Hapi.js team. Joi allows you to create blueprints or schemas for JavaScript objects to ensure validation of key information.
## Installation
```
  $ npm i joi
```
## Import
```
  const Joi = require('joi') / import Joi from 'joi' 
```
## Making a schema
```
  const schema = Joi.object().keys({
    username: Joi.string().alphanum().min(3).max(30).required(),
    password: Joi.string().regex(/^[a-zA-Z0-9]{3,30}$/),
    access_token: [Joi.string(), Joi.number()],
    birthyear: Joi.number().integer().min(1900).max(2013),
    email: Joi.string().email({ minDomainAtoms: 2 })
  }).with('username', 'birthyear').without('password', 'access_token')
```
## Validation process
```
  const result = Joi.validate({ username: 'abc', birthyear: 1994 }, schema)
  // result.error === null - valid input 

  // You can also call a callback
  Joi.validate({ username: 'abc', birthyear: 1994 }, schema, (err, value) => { })
  // OR
  const {error, value} = Joi.validate({ a: 'a string' }, schema) and use error or value. 
```
## Methods
```
  .string()         - Must be String
  .email()          - Must be a valid email
  .regex(/^/d{3})   - Must be a format of ___ XXX-XXX-XXXX=/^\d{3}-\d{3}-\d{4}$/
  .required()       - Cannot be undefined
  .date()           - Must have a valid date
  .date().iso()     - Must have a ISO-8601 date
  .max('1-1-2004')  - Must have dates before ____
  
```

## Advanced
```
  // The schema can be an object
  const schema = Joi.string().min(10);
  
  // Without require this returns true
  Joi.validate(undefined, Joi.string()) 
  // To require input, there are two options
  Joi.validate(undefined, Joi.string().required())
  // or
  Joi.validate(undefined, Joi.string(), /* options */ { presence: "required" })
  
  // Joi type of any data type
  const any = Joi.any()
  
```
