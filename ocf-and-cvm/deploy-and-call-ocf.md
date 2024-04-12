# Deploy and Call OCF

## **Deploy OCF**

```json
{
	"p": "ocf",
	"v": "0.1",
	"op": "deploy",
	"name": "func_name",
	"func": "fn valid_if(params: &[String]) -> bool { return true; }"
}
```

* `p`&`op`: the same way they are used in BRC-20.
* `v`: version
* `name`: name of OCF
* `func`: define a OCF function
  * must be in the format of `fn valid_if(para: &[String]) -> bool {...exp}`.
  * the length of `params` can not exceed 10 and `params` only support the `&[String]` type.
  * `...exp` can only contain one expression. The current version only supports the use of operators, if branching statements and the system functions mentioned below, and does not support looping statements.
  * For more details about the syntax of OCF, see "Basic OCF Syntax" section.

## **Call OCF**

```json
{
	"p": "ocf",
	"op": "call",
	"name": "func_name",
	"params": ["a"]
}
```

* `params`: parameters passed to the function are an array of strings.
